---
layout: post
title: "Printing Atmel AVR Assembly source code in LaTeX"
description: ""
category: "LaTeX"
tags: []
---
{% include JB/setup %}

My current class has assignments in AVR Assembly and I've gotten source code printing of Atmel AVR Assembly working in LaTeX with color highlighting.

Here's how it works:

The [listings](https://en.wikibooks.org/wiki/LaTeX/Source_Code_Listings) module in LaTeX allows for printing of source code for a variety of different languages, but AVR Assembly is not one of them. I needed to go ahead and define the language highlighting myself. Assembly is fairly simple, so I just needed to define keywords for all the instructions and registers.

I found a set of keywords defined by Nils Michelsen online, and edited it so that I could highlight instructions, registers, and directives separately.

[lstlang.sty]({{ BASE_PATH }}/files/lstlang.sty)

This definition goes into the 'lstlang.sty' file within the listings module.

Now, in my tex file, I configured the listings module to use this definition:

{% highlight latex %}
\definecolor{MyDarkGreen}{rgb}{0.0,0.4,0.0} % This is the color used for comments
\lstloadlanguages{AVR}%
\lstset{language=AVR, % AVR 8-bit Assembler
        frame=single, % Single frame around code
        basicstyle=\small\ttfamily, % Use small true type font
        keywordstyle=\color{Blue}\bf, % Instructions in blue, bold
        keywordstyle=[2]\color{Orange}, % Registers and ports in orange
        keywordstyle=[3]\color{Purple}, % Directives in purple
        commentstyle=\usefont{T1}{pcr}{m}{sl}\color{MyDarkGreen}\small,
        tabsize=5, % 5 spaces per tab
        numbers=left, % Line numbers on left
        firstnumber=1, % Line numbers start with line 1
        numberstyle=\tiny\color{Blue}, % Line numbers are blue and small
        stepnumber=5 % Line numbers go in steps of 5
        }

% Creates a new command to include an asm script,
% the first parameter is the filename of the program (without .asm),
% the second parameter is the caption
\newcommand{\avrasm}[2]{
\begin{itemize}
\item[]\lstinputlisting[caption=#2,label=#1]{#1.asm}
\end{itemize}
}
{% endhighlight %}

Now, I can just place a main.asm file in the same directory, and call it with `\avrasm{main}{comment}`. The output looks like this:

![AVR ASM listings example]({{ BASE_PATH }}/images/avrasm.png)
