---
title: "CC  Radare2 Tryhackme Writeup 41f05bb590e6"
platform: Medium
original_file: 2024-08-22_CC--Radare2-Tryhackme-Writeup-41f05bb590e6.md
---

# CC  Radare2 Tryhackme Writeup 41f05bb590e6

::: {}
# CC: Radare2 Tryhackme Writeup {#cc-radare2-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "CC: Radare2"
:::

::::::: {.section .e-content field="body"}
:::::: {#451a .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### CC: Radare2 Tryhackme Writeup {#0589 .graf .graf--h3 .graf--leading .graf--title name="0589"}

**This is a Writeup of Tryhackme room "CC: Radare2"**

<figure id="e092" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gv-KhcldVkEbiMhF.png"
class="graf-image" data-image-id="0*gv-KhcldVkEbiMhF.png"
data-width="487" data-height="264" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/ccradare2](https://tryhackme.com/room/ccradare2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/ccradare2"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Task 1: Intro {#c555 .graf .graf--h3 .graf-after--p name="c555"}

This room assumes that you have basic x86 assembly knowledge. If you do
not I highly recommend doing the [**Intro to
x86--64**](https://tryhackme.com/room/introtox8664){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/introtox8664"
rel="noopener ugc nofollow noopener" target="_blank"} room before
completing this done.

This room is also not designed to be a 100% teach everything on radare2.
It is designed to teach you how some of the more common things in
radare2 are used.

The included zip file has all the binaries you will need for this
exercise.

With that out of the way let's get started!

### Task 2: Command Line Options {#9e40 .graf .graf--h3 .graf-after--p name="9e40"}

A quick intro to some of the commonly used command line flags for
radare2, some of these flags will be extremely useful for later tasks.
Include all parts of the flag including the -. All flags can be found in
the help menu

**Q.1:** What flag to you set to analyze the binary upon entering the r2
console (equivalent to running aaa once your inside the console)

> ***Answer: -A***

**Q.2:** How do you enable the debugger?

> ***Answer: -d***

**Q.3:** How do you open the file in write mode?

> ***Answer: -w***

**Q.4:** How do you enter the console without opening a file

> ***Answer: -***

### Task 3: Analyzation {#8bde .graf .graf--h3 .graf-after--blockquote name="8bde"}

Once inside the radare console you have a myriad of options to analyze
your binary. Generally all analyzation commands start with the letter a.
If you want to list all possible commands that can be done with your
starting letter(s) you add a question mark to the end. For example
`a?`{.markup--code .markup--p-code} would output
`ab,aa,ac`{.markup--code .markup--p-code} along with a description on
what each command does.

**Q.1:** What command "Analyzes Everything" (all functions and their
arguments: Same as running with radare with -A)

> ***Answer: aaa***

**Q.2:** What command does basic analysis on functions?

> ***Answer: af***

**Q.3:** How do you list all functions?

> ***Answer: afl***

**Q.4:** How many functions are in the example1 binary?

> ***Answer: 12***

**Q.5:** What is the name of the secret function in the example1 binary?

> ***Answer: secret_func***

### Task 4: Information {#f309 .graf .graf--h3 .graf-after--blockquote name="f309"}

**`i`{.markup--code .markup--p-code .u-paddingRight0
.u-marginRight0}**` `{.markup--code .markup--p-code .u-paddingRight0
.u-marginRight0}is a command that shows general information of the
binary. Like **`a`{.markup--code .markup--p-code}** it has many sub
commands each with varying degrees of specificity.

**Q.1:** What command shows all the information about the file that
you're in?

> ***Answer: ia***

**Q.2:** How do you get every string that is present in the binary?

> ***Answer: izz***

**Q.3:** What if you want the address of the main function?

> ***Answer: im***

**Q.4:** What character do you add to the end of every command to get
the output in JSON format?

> ***Answer: j***

**Q.5:** How do you get the entrypoint of the file?

> ***Answer: ie***

**Q.6:** What is the secret string hidden in the example2 binary?

> ***Answer: goodjob***

### Task 5: Navigating Through Memory {#d430 .graf .graf--h3 .graf-after--blockquote name="d430"}

**-s** is the command that is used to navigate through the memory of
your binary. With it and its variations you can you can get information
about where you are in the binary as well as move to different points in
the binary.

**Note:** For user created functions that aren't main, you will have to
add sym. before them for example sym.user_func

**Q.1:** How do you print out the the current memory address your
located at in the binary?

> ***Answer: s***

**Q.2:** What command do you use to go to a specific point in memory
with the syntax \<command\> \<address\>?

> ***Answer: s***

**Q.3:** What command would you run to go 5 bytes forward?

> ***Answer: s+ 5***

**Q.4:** What about 12 bytes backward?

> ***Answer: s- 12***

**Q.5:** How do you undo the previous seek?

> ***Answer: s-***

**Q.6:** How would go to the memory address of the main function?

> ***Answer: s main***

**Q.7:** What if you wanted to go to the address of the rax register?

> ***Answer: sr rax***

### Task 6: Printing {#3195 .graf .graf--h3 .graf-after--blockquote name="3195"}

`p `{.markup--code .markup--p-code}is a command that shows data in a
myriad of formats. The command is useful for when you want to get
information about what is happening in memory, and get some of the data
that\'s contained in memory as well. With the p command it is also
useful to know about the `@`{.markup--code .markup--p-code} symbol in
radare. The `@`{.markup--code .markup--p-code} symbol is used to specify
that something is an address in memory, for example if you wanted to
specify you were talking about the memory address of the main function
you would use` <command>@main`{.markup--code .markup--p-code}

**Q.1:** How would you print the hex output of where you currently are
in memory?

> ***Answer: px***

**Q.2:** How would you print the disassembly of where you're currently
at in memory?

> ***Answer: pd***

**Q.3:** What if you wanted the disassembly of the main function?

> ***Answer: pd @ main***

**Q.4:** What command prints out the emoji hexdump? (this is not useful
at all I just find it funny)

> ***Answer: pxe***

**Q.5:** What if you decided you were too good for rows and you wanted
the disassembly in column format?

> ***Answer: pC***

**Q.6:** What is the value of the first variable in the main function
for the example 3 binary?

> ***Answer: 1***

**Q.7:** What about the second variable?

> ***Answer: 5***

### Task 7: The Mid-term {#c4e8 .graf .graf--h3 .graf-after--blockquote name="c4e8"}

Congrats on getting to this point, you now know enough to pass the
mid-term exam. The questions in this task will all be related to
commands that were in previous tasks so if you skipped one, I recommend
going back and doing it. As you probably guessed from the file name all
exercises in this task will be done using the midterm binary file.

**Q.1:** How many functions are in the binary?

> ***Answer: 13***

**Q.2:** What is the value of the hidden string?

> ***Answer: you_found_me***

**Q.3:** What is the return value of secret_func()?

> ***Answer: 4***

**Q.4:** What is the value of the first variable set in the main
function(in decimal format)?

> ***Answer: 12***

**Q.5:** What about the second one(also in decimal format)?

> ***Answer: 192***

**Q.6:** What is the next function in memory after the main function?

> ***Answer: midterm_func***

**Q.7:** How do you get a hexdump of four bytes of the memory address
your currently at?

> ***Answer: px 4***

### Task 8: Debugging {#79ad .graf .graf--h3 .graf-after--blockquote name="79ad"}

Recall that in the task "Command Line Options" you learned that the -d
flag has radare enter debug mode. Debug mode allows you to set
breakpoints and offers a lot of options to not only navigate through
your binary, but to analyze the data that goes in and out of the
registers as well.

**Q.1:** How do you set a breakpoint?

**Answer: db**

**Q.2:** What command is used to print out the values of all the
registers?

**Answer: dr**

**Q.3:** How do you run through the program until the program either
ends or you hit the next breakpoint?

**Answer: dc**

**Q.4:** What if you want to step through the binary one line at a time?

**Answer: ds**

**Q.5:** How do you go forth 2 lines in the binary?

**Answer: ds 2**

**Q.6:** How do you list out the indexes and memory addresses of all
breakpoints?

**Answer: dbi**

### Task 9: Visual Mode {#c9e4 .graf .graf--h3 .graf-after--p name="c9e4"}

While visual mode is by no means necessary and won't inherently teach
you anything new about the binary you're currently running. It allows
the assembly to more human readable and provides a lot of options to
enhance the visual appeal of radare and can definitely improve
efficiency. Therefore I would state it's a valuable tool that you should
know how to use. All commands involving visual mode start with
`v`{.markup--code .markup--p-code}

**Q.1:** How do you enter "graph mode" which allows everything to be
organized in nice readable boxes?(A personal favorite of mine. Also note
that the second character is uppercase)

> ***Answer: vV***

**Q.2:** What character do you press to run normal radare commands
inside visual mode?

> ***Answer: :***

**Q.3:** How do you go back to the regular radare shell(leaving visual
mode)?

> ***Answer: q***

**Q.4:** What if you want to step through the binary inside Visual mode?

> ***Answer: s***

**Q.5:** How do you add a comment?

> ***Answer: ;***

### Task 10: Write Mode {#615e .graf .graf--h3 .graf-after--blockquote name="615e"}

Occasionally you might end up in a situation where a task is impossible
to solve with the current instructions. For example take this code

``` {#cfc3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
int val = 4;if(val == 5){printf(“%s”,”You win!”);}
```

You will never be able to get it to print out You win! because under
normal circumstances val will never be set equal to 5. This is where
write mode comes in, it allows you to change instructions so you can get
certain conditions to execute. All commands involving write mode start
with `w`{.markup--code .markup--p-code}

**Q.1:** How do you write a string to the current memory address.

> ***Answer: w***

**Q.2:** What command lists all write changes?

> ***Answer: wc***

**Q.3:** What command modifies an instruction at the current memory
address?

> ***Answer: wa***

### Task 11: The Final Exam {#83da .graf .graf--h3 .graf-after--blockquote name="83da"}

Congratulations on making it to this point. You should now be able to
solve a crackme! Use all the tools you've learned and get that password!
The binary to use for this task is the_final_exam!

**Q.1:** What is the password that outputs the you win! message?

> ***Answer: oekZ_Z_j***

### Promote and Collaborate on Cybersecurity Insights {#4183 .graf .graf--h3 .graf-after--blockquote name="4183"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#3378 .graf .graf--h3 .graf-after--p name="3378"}

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
.h-card} on [August 22, 2024](https://medium.com/p/41f05bb590e6).

[Canonical
link](https://medium.com/@bevijaygupta/cc-radare2-tryhackme-writeup-41f05bb590e6){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
