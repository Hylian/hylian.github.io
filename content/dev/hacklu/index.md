+++
title="Hack.lu 2014 CTF: Gunslinger Joe's Gold Stash"
date=2014-10-23
transparent=true
+++

```
Category: Reversing 
Points: 200 
Author: cutz 
Description: Silly Gunslinger Joe has learned from his mistakes with his private terminal and now tries to remember passwords. But he's gotten more paranoid and chose to develope an additional method: protect all his private stuff with a secure locking mechanism that no one would be able to figure out! He's so confident with this new method that he even started using it to protect all his precious gold. So … we better steal all of it!
SSH: joes_gold@wildwildweb.fluxfingers.net  PORT: 1415 
PASSWORD: 1gs67uendsx71xmma8    
Note: If your username/password combination is not getting accepted, then the challenge is working as expected.
```

The first thing we see when logging in to the server is that there is a file named FLAG, and an executable named gold_stash. Executing gold_stash prompts us for a username and password. By running `ls -l`, we see that FLAG is readable by root only and setuid is set for gold_stash, meaning it runs as root user. 

{{ resized(img="1.png") }}

Opening the executable up in IDA, we find a very straight-forward program that checks the username and password against two plaintext strings and pops a shell by calling `execve` on `/bin/sh` if the strings match.

Since the username and password are in plaintext, we can just pull them straight out. The username is `Joe` and the password is `omg_joe_is_so_rich`. 

{{ resized(img="2.png") }}

However, using this username/password combination still results in a failed authentication. We notice that in gdb on the challenge server and on a local machine, it does pop a shell as intended.

{{ resized(img="3.png") }}

Looking through the disassembly for gold_stash, we don't notice anything particularly interesting. All the memory is allocated and initialized, and there isn't any way for data to leak in, causing the check to fail.

Thus, we can reason that the thing that is causing the check to fail is external to the executable and unique to the root user on the challenge machine only. The external glibc libraries are a good suspect.

We run `locate joe` in the root folder to find any files with substring `joe`, and find an interesting kernel module called `joe.ko` at `/lib/modules/3.13.0-36-generic/kernel/joe/joe.ko`.

{{ resized(img="4.png") }}

Disassembling the module in IDA confirms that it is relevant to the challenge.

{{ resized(img="5.png") }}

Inside the module, there is a function called `fuqstring` which is very similar to some of the code in the main `joe` function. This function iterates over an array in memory, and for every element, it subtracts 4 and then XOR's it with an element from the array `byte_2DD`. We see that it iterates over 18 elements, which is the length of the password string.

{{ resized(img="6.png") }}

The array `byte_2DD` is the character array `123456789012445678`. So, we just calculate the inverse of `(a ^ (b-4))`, which is `(a ^ b)+4`, for every character in the string.

{{ resized(img="7.png") }}

```
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
```

{{ resized(img="8.png") }}

Using this password pops us a shell, and we can read the file.

{{ resized(img="9.png") }}
