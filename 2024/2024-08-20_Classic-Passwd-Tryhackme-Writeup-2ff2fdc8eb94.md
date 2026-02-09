---
title: "Classic Passwd Tryhackme Writeup 2ff2fdc8eb94"
platform: Medium
original_file: 2024-08-20_Classic-Passwd-Tryhackme-Writeup-2ff2fdc8eb94.md
---

# Classic Passwd Tryhackme Writeup 2ff2fdc8eb94

::: {}
# Classic Passwd Tryhackme Writeup {#classic-passwd-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Classic Passwd"
:::

::::::: {.section .e-content field="body"}
:::::: {#781f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Classic Passwd Tryhackme Writeup {#de19 .graf .graf--h3 .graf--leading .graf--title name="de19"}

**This is a Writeup of Tryhackme room "Classic Passwd"**

<figure id="da9d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1Jjt_r9GDchYT7aJ.png"
class="graf-image" data-image-id="0*1Jjt_r9GDchYT7aJ.png"
data-width="480" data-height="257" data-is-featured="true" />
</figure>

[https://tryhackme.com/room/classicpasswd](https://tryhackme.com/room/classicpasswd){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/classicpasswd"
rel="noopener ugc nofollow noopener" target="_blank"}

**Room link:**
[https://tryhackme.com/room/classicpasswd](https://tryhackme.com/room/classicpasswd){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/classicpasswd"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Method-1 (ltrace) {#fd5e .graf .graf--h3 .graf-after--p name="fd5e"}

Let's do dynamic analysis. Dynamic analysis has to be done in a sandbox
environment. There are some tools pre-installed in Linux that can be
used to display more detailed information.

First, download the executable file. Check the file information using
the following command

<figure id="9b50" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2Ux85EMt9eGFX5zn.png"
class="graf-image" data-image-id="0*2Ux85EMt9eGFX5zn.png"
data-width="875" data-height="143" />
</figure>

We could see that the file is an ELF 64-bit LSB pie executable. Let's
execute the file after providing required permissions.

<figure id="aaf0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dMYgzSreR3EQtNGr.png"
class="graf-image" data-image-id="0*dMYgzSreR3EQtNGr.png"
data-width="350" data-height="223" />
</figure>

After executing we can find that the binary asks for a "username". Try
executing with a random username, it result's in authentication error
means that we need to provide correct username inorder to get the flag.

Now let's use **ltrace,** for dynamic analysis. **ltrace** is a program
that simply runs the specified **command** until it exits. It intercepts
and records the dynamic library calls which are called by the executed
process and the signals which are received by that process. It can also
intercept and print the system calls executed by the program.

We can execute the binary with the following command.

As expected the binary asks for "username" again. Provide a random
username.

<figure id="304d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nIWBndVr5z1-XDgO.png"
class="graf-image" data-image-id="0*nIWBndVr5z1-XDgO.png"
data-width="810" data-height="273" />
</figure>

ltrace logged library functions that the program called and received. It
called "strcmp" function with the correct "username". Now let's use this
"username" to print the flag.

When prompted for username, provide the one that we got using ltrace.

<figure id="b5e5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EzQbEXLaaXd0JBO8.png"
class="graf-image" data-image-id="0*EzQbEXLaaXd0JBO8.png"
data-width="397" data-height="147" />
</figure>

We have got our flag.

### Method-2 (Ghidra) {#a291 .graf .graf--h3 .graf-after--p name="a291"}

Let's use Ghidra to analyse the binary and find the flag.

Decompile the main function using ghidra

Run Ghidra and create new project

<figure id="b0cc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*V4L2GJipAw6OohKz.png"
class="graf-image" data-image-id="0*V4L2GJipAw6OohKz.png"
data-width="629" data-height="515" />
</figure>

select Non-shared project

<figure id="52ed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oQMB-KiIPJ9ET9sK.png"
class="graf-image" data-image-id="0*oQMB-KiIPJ9ET9sK.png"
data-width="789" data-height="589" />
</figure>

create folder and define project name

<figure id="b7db" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OiBuHU-C3qfFzHvU.png"
class="graf-image" data-image-id="0*OiBuHU-C3qfFzHvU.png"
data-width="654" data-height="482" />
</figure>

click on green dragon

<figure id="4d53" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ncL7sDLZvtrxj2mB.png"
class="graf-image" data-image-id="0*ncL7sDLZvtrxj2mB.png"
data-width="784" data-height="371" />
</figure>

<figure id="5e10" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*h2l0PXWsl_GjrZzH.png"
class="graf-image" data-image-id="0*h2l0PXWsl_GjrZzH.png"
data-width="875" data-height="449" />
</figure>

import your file

<figure id="1f92" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0Kg4UNgyzykkmLwM.png"
class="graf-image" data-image-id="0*0Kg4UNgyzykkmLwM.png"
data-width="413" data-height="534" />
</figure>

<figure id="d8eb" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*p-l2knd4okGN-KqW.png"
class="graf-image" data-image-id="0*p-l2knd4okGN-KqW.png"
data-width="742" data-height="566" />
</figure>

<figure id="6ed8" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*eqjQIqHLi6mLJlBr.png"
class="graf-image" data-image-id="0*eqjQIqHLi6mLJlBr.png"
data-width="497" data-height="275" />
</figure>

<figure id="6d1c" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*vqUekveL4kJhSHSW.png"
class="graf-image" data-image-id="0*vqUekveL4kJhSHSW.png"
data-width="579" data-height="141" />
</figure>

<figure id="c36b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*jkTNCDerdC_F2IL_.png"
class="graf-image" data-image-id="0*jkTNCDerdC_F2IL_.png"
data-width="692" data-height="554" />
</figure>

Now to windows tab and select function option

<figure id="3213" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MIKJwUAcPTpAZI9X.png"
class="graf-image" data-image-id="0*MIKJwUAcPTpAZI9X.png"
data-width="875" data-height="480" />
</figure>

Now look for main function

<figure id="4257" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bKz-lh-Ao8wSjn6-.png"
class="graf-image" data-image-id="0*bKz-lh-Ao8wSjn6-.png"
data-width="639" data-height="538" />
</figure>

Decompile the main function

<figure id="59b4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*m7U0hh9-E636dcDo.png"
class="graf-image" data-image-id="0*m7U0hh9-E636dcDo.png"
data-width="711" data-height="522" />
</figure>

We could see that main function calls for two functions;

1.  [vuln]{#71b4}
2.  [gfl]{#0833}

Let's decompile and check this two functions

After decompiling function "vuln" it doesn't give anything interesting.
So I went on analysing function "gfl"

<figure id="ee4e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*m1WW2tdU0DbFRAmq.png"
class="graf-image" data-image-id="0*m1WW2tdU0DbFRAmq.png"
data-width="379" data-height="501" />
</figure>

0x6\*\*\*\*\*,2\*\*\*

Look's like we have our flag in hexadecimal. Let's convert them into
integer.

We can use online tools like
[rapidtables](https://www.rapidtables.com/convert/number/hex-to-decimal.html){.markup--anchor
.markup--p-anchor
data-href="https://www.rapidtables.com/convert/number/hex-to-decimal.html"
rel="noopener ugc nofollow noopener" target="_blank"} to convert
hexadecimal into it's corresponding integer values or we can use our
terminal to convert hexadecimal into integer using the following
commands

<figure id="264a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sxwbk2OVjGvJeiIA.png"
class="graf-image" data-image-id="0*sxwbk2OVjGvJeiIA.png"
data-width="273" data-height="225" />
</figure>

and finally this is your **flag** after combined both values

THM{6\*\*\*\*\*\*8\*\*\*}

### Method-3 (Radare2 OR r2) {#3c31 .graf .graf--h3 .graf-after--p name="3c31"}

For this challenge i used
[**radare2**](https://github.com/radareorg/radare2){.markup--anchor
.markup--p-anchor data-href="https://github.com/radareorg/radare2"
rel="noopener ugc nofollow noopener" target="_blank"} to reverse
engineer the binary.

We start by load radare2 and run the challenge file in debug mode

``` {#3c70 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
r2 -d Challenge.Challenge
```

Afterwards we auto-analyze the binary to discover the strings and
functions by running **`aaa`{.markup--code .markup--p-code}**

<figure id="dfad" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gL6G_b_J27Wm3_Q4.png"
class="graf-image" data-image-id="0*gL6G_b_J27Wm3_Q4.png"
data-width="679" data-height="371" />
</figure>

Now that we have analyzed the binary, we run `afl`{.markup--code
.markup--p-code} to view the functions, which will list many functions.
However we can start from the main function

<figure id="24a1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*w9P0by3_1I6sNPSc.png"
class="graf-image" data-image-id="0*w9P0by3_1I6sNPSc.png"
data-width="778" data-height="476" />
</figure>

By running `s main`{.markup--code .markup--p-code} we can navigate to
the main function henceforth print the dissassembly by running
`pdf`{.markup--code .markup--p-code}

<figure id="46b2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JpSb0HIfTGwT2cT-.png"
class="graf-image" data-image-id="0*JpSb0HIfTGwT2cT-.png"
data-width="637" data-height="300" />
</figure>

From the main function we see that it is calling two functions
`vuln`{.markup--code .markup--p-code} and `gfl`{.markup--code
.markup--p-code}

*Note: Your memory addresses will not be same*\
We can see two interesting functions. `sym.vuln`{.markup--code
.markup--p-code} and `sym.gfl`{.markup--code .markup--p-code}. We can
analyse them the same way `pdf @sym.vuln`{.markup--code .markup--p-code}
and `pdf @sym.gfl`{.markup--code .markup--p-code}. Lets do that!

<figure id="6bf2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sWJaTyAW47mFM5iX.png"
class="graf-image" data-image-id="0*sWJaTyAW47mFM5iX.png"
data-width="875" data-height="548" />
</figure>

Nice! We can all see the flag, right? Well dont get too excited, look
back at `sym.main`{.markup--code .markup--p-code} the code execution has
to get there, we cant just make the instruction pointer jump over here.
Oh, and all those arrows, dont worry, its a for loop.

<figure id="b094" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3eh7Y5KJC1dCbBRM.png"
class="graf-image" data-image-id="0*3eh7Y5KJC1dCbBRM.png"
data-width="665" data-height="370" />
</figure>

These are local variables. We can view the state of their memory (at
runtime only) by using `px @rbp-ADDRESS`{.markup--code .markup--p-code}
so to view var_2c0h we would do `px @rbp-0x2c0`{.markup--code
.markup--p-code}.

<figure id="1063" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PmhZ3NkH3bZWv0PA.png"
class="graf-image" data-image-id="0*PmhZ3NkH3bZWv0PA.png"
data-width="875" data-height="489" />
</figure>

<figure id="80e0" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*q3_EH16Q3bBlp1k5.png"
class="graf-image" data-image-id="0*q3_EH16Q3bBlp1k5.png"
data-width="875" data-height="317" />
</figure>

<figure id="cd6e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*y06X569IyLrzqOfG.png"
class="graf-image" data-image-id="0*y06X569IyLrzqOfG.png"
data-width="778" data-height="617" />
</figure>

<figure id="8aa5" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*PVXDlvHZNDGLbIWC.png"
class="graf-image" data-image-id="0*PVXDlvHZNDGLbIWC.png"
data-width="398" data-height="129" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#6152 .graf .graf--h3 .graf-after--figure name="6152"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#2ae0 .graf .graf--h3 .graf-after--p name="2ae0"}

[Vijay
Gupta](https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2"
rel="noopener" target="_blank"} is a cybersecurity enthusiast with
several years of experience in cyber security, [cyber crime forensics
investigation](https://play.google.com/store/books/details?id=VRz7EAAAQBAJ){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/details?id=VRz7EAAAQBAJ"
rel="noopener ugc nofollow noopener" target="_blank"}, and security
awareness training in schools and colleges. With a passion for
safeguarding digital environments and educating others about
cybersecurity best practices, Vijay has dedicated his career to
promoting cyber safety and resilience. Stay connected with Vijay Gupta
on various social media platforms and professional networks to access
valuable insights and stay updated on the latest cybersecurity trends.
:::
::::
::::::
:::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [August 20, 2024](https://medium.com/p/2ff2fdc8eb94).

[Canonical
link](https://medium.com/@bevijaygupta/classic-passwd-tryhackme-writeup-2ff2fdc8eb94){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
