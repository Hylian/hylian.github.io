---
layout: post
title: "Hack.lu 2014 CTF Write Up: Gunslinger Joe's Gold Stash"
description: ""
category: "hack.lu"
tags: [ctf]
---
{% include JB/setup %}

<blockquote>
Category: Reversing 
<br />
Points: 200 
<br />
Author: cutz 
<br />
Description: Silly Gunslinger Joe has learned from his mistakes with his private terminal and now tries to remember passwords. But he's gotten more paranoid and chose to develope an additional method: protect all his private stuff with a secure locking mechanism that no one would be able to figure out! He's so confident with this new method that he even started using it to protect all his precious gold. So … we better steal all of it!
<br />
SSH: joes_gold@wildwildweb.fluxfingers.net  PORT: 1415 
<br />
PASSWORD: 1gs67uendsx71xmma8    
<br />
Note: If your username/password combination is not getting accepted, then the challenge is working as expected.
</blockquote>

The first thing we see when logging in to the server is that there is a file named FLAG, and an executable named gold_stash. Executing gold_stash prompts us for a username and password. By running ```ls -l```, we see that FLAG is readable by root only and setuid is set for gold_stash, meaning it runs as root user. 

![ls -l]({{ BASE_PATH }}/images/joe/1.png)

Opening the executable up in IDA, we find a very straight-forward program that checks the username and password against two plaintext strings and pops a shell by calling execve on /bin/sh if the strings match.

Since the username and password are in plaintext, we can just pull them straight out. The username is "Joe" and the password is "omg_joe_is_so_rich". 

![gold_stash disassembly]({{ BASE_PATH }}/images/joe/2.png)


However, using this username/password combination still results in a failed authentication. We notice that in gdb on the challenge server and on a local machine, it does pop a shell as intended.

![failed login]({{ BASE_PATH }}/images/joe/3.png)

Looking through the disassembly for gold_stash, we don't notice anything particularly interesting. All the memory is allocated and initialized, and there isn't any way for data to leak in, causing the check to fail.

Thus, we can reason that the thing that is causing the check to fail is external to the executable and unique to the root user on the challenge machine only. The external glibc libraries are a good suspect.

We run "locate joe" in the root folder to find any files with substring "joe", and find an interesting kernel module called "joe.ko" at /lib/modules/3.13.0-36-generic/kernel/joe/joe.ko.

![locate joe]({{ BASE_PATH }}/images/joe/4.png)

Disassembling the module in IDA confirms that it is relevant to the problem.

![joe disassembly]({{ BASE_PATH }}/images/joe/5.png)

Inside the module, there is a function called "fuqstring" which is very similar to some of the code in the main "joe" function. This function iterates over an array in memory, and for every element, it subtracts 4 and then XOR's it with an element from the array byte_2DD. We see that it iterates over 18 elements, which is the length of the password string.

![fuqstring]({{ BASE_PATH }}/images/joe/6.png)

The array byte_2DD is the character array "123456789012445678". So, we just calculate the inverse of (a ^ (b-4)), which is (a ^ b)+4, for every character in the string. I wrote a simple C program for this purpose.

![fuqstring]({{ BASE_PATH }}/images/joe/7.png)

{% highlight C %}
#include <stdio.h>

void main()
{
    char* a;
    char* b;

    a = "123456789012445678";
    b = "omg_joe_is_so_rich";

    for(int i = 0; i < 18; i++)
        printf("%c", (a[i] ^ b[i])+4);

    printf("\n");
}
{% endhighlight %}

![xor output]({{ BASE_PATH }}/images/joe/8.png)

Using this password pops us a shell, and we can read the file.

![success]({{ BASE_PATH }}/images/joe/9.png)
