---
title: "Bash Scripting Tryhackme writeup 9336fbf488fb"
platform: Medium
original_file: 2024-08-24_Bash-Scripting-Tryhackme-writeup-9336fbf488fb.md
---

# Bash Scripting Tryhackme writeup 9336fbf488fb

::: {}
# Bash Scripting Tryhackme writeup {#bash-scripting-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Bash Scripting"
:::

::::::: {.section .e-content field="body"}
:::::: {#e64c .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Bash Scripting Tryhackme writeup {#2c38 .graf .graf--h3 .graf--leading .graf--title name="2c38"}

**This is a Writeup of Tryhackme room "Bash Scripting"**

<figure id="a765" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PUxzV8Gt5fSBqb5k.png"
class="graf-image" data-image-id="0*PUxzV8Gt5fSBqb5k.png"
data-width="479" data-height="245" data-is-featured="true" />
</figure>

[https://tryhackme.com/room/bashscripting](https://tryhackme.com/room/bashscripting){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bashscripting"
rel="noopener ugc nofollow noopener" target="_blank"}

**Room link:**
[https://tryhackme.com/room/bashscripting](https://tryhackme.com/room/bashscripting){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bashscripting"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Task 2: Our first simple bash scripts {#877d .graf .graf--h3 .graf-after--p name="877d"}

Ok now that we have had a brief introduction to what bash is and what it
is used for let's jump right into some examples!

First of all let's lay out our structure.

A bash script always starts with the following line of code at the top
of the script.

Image source
[https://carbon.now.sh/](https://carbon.now.sh/){.markup--anchor
.markup--p-anchor data-href="https://carbon.now.sh/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="d1aa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rDpLKDvhnyjrbvrn.png"
class="graf-image" data-image-id="0*rDpLKDvhnyjrbvrn.png"
data-width="662" data-height="236" />
</figure>

This is so your shell (whatever type of it) knows that it needs to run
your file using bash in the terminal.

Lets get into some basic examples.

<figure id="43c4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oDVFy5Y1xX7mx-4z.png"
class="graf-image" data-image-id="0*oDVFy5Y1xX7mx-4z.png"
data-width="796" data-height="308" />
</figure>

This will return the string "Hello World". The command
"`echo`{.markup--code .markup--p-code}" is used to output text to the
screen, the same way as "`print`{.markup--code .markup--p-code}" in
python. I suggest you test this out in your terminal to get to grips
with bash!

You can also perform normal Linux commands inside your bash script and
it will be executed if formatted right. For example we can run the
command "`ls`{.markup--code .markup--p-code}" inside our bash script and
we will see the output when we run the file. So lets make it do this!

<figure id="cafc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dWgkDxk35T5aUAq6.png"
class="graf-image" data-image-id="0*dWgkDxk35T5aUAq6.png"
data-width="780" data-height="452" />
</figure>

Now from here on I am going to assume that you have a basic
understanding of Linux and its commands, if you don't please go make
sure to check out the Linux fundamentals 1 and then come back and try
again.
[**https://tryhackme.com/room/linux1**](https://tryhackme.com/room/linux1){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linux1"
rel="noopener ugc nofollow noopener" target="_blank"}

I'm also not going to include the `#!/bin/bash`{.markup--code
.markup--p-code} at the start of my code snippets otherwise it will take
up a lot of room so be aware that you need it always at the start of
your files!

Now to run our bash script we must first give it executable permissions

`Chmod +x yourfile.sh`{.markup--code .markup--p-code}

And then we run it using `./`{.markup--code .markup--p-code}

<figure id="ec9c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dnvV2s_AbwM-mWYv.png"
class="graf-image" data-image-id="0*dnvV2s_AbwM-mWYv.png"
data-width="875" data-height="320" />
</figure>

Please run this for yourself and see what you get.

We can see it has outputted the results of the commands
"`whoami`{.markup--code .markup--p-code}" and "`id`{.markup--code
.markup--p-code}".

**#1**: What piece of code can we insert at the start of a line to
comment out our code?

> ***Answer: \#***

**#1**: What will the following script output to the screen, echo
"BishBashBosh"

> ***Answer: BishBashBosh***

### Task 3: Variables {#fde4 .graf .graf--h3 .graf-after--blockquote name="fde4"}

Now we are moving onto variables,

in bash these are quite simple and we create them like so:

<figure id="2e5c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*P8nqkopLzjfZ0f9e.png"
class="graf-image" data-image-id="0*P8nqkopLzjfZ0f9e.png"
data-width="502" data-height="236" />
</figure>

Where we give the value of `Jammy`{.markup--code .markup--p-code} and
assign it to the variable `name`{.markup--code .markup--p-code}.

Please note that for variables to work you cannot leave a space between
the variable name, the "**=**" and the value. They cannot have spaces
in.

So how would we now use our variable? Well its also very simple.

We have to add a `$`{.markup--code .markup--p-code} onto front of our
variable name in order to use it.

<figure id="ba22" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3x9e-M2GHlxNgnp_.png"
class="graf-image" data-image-id="0*3x9e-M2GHlxNgnp_.png"
data-width="678" data-height="308" />
</figure>

If we test this out in our own terminal we get something like this:

`$ name="Jammy"`{.markup--code .markup--p-code}

`$ echo $name`{.markup--code .markup--p-code}

`Jammy`{.markup--code .markup--p-code}

This would output "**Jammy**" to the screen.

Variables make it much easier to store data and rather than typing out
the same thing in multiple places we could simply insert our variable
with \$var and then declare that to a certain value making it easier to
fall back on if you do something wrong and need to change it. So how can
we debug our code?

Debugging is a very important part of programming so we should get used
to problem solving and fixing errors as early as possible. And bash has
a few built in features that make our life simple.

When running at the command line you can do:

`bash -x ./file.sh`{.markup--code .markup--p-code}

You can make a simple bash script(now you know some basic syntax) and
make something completely wrong. Then step through your program with
debug mode and see what it looks like when it throws errors!

This tells you which lines are working and which lines are not. If you
want to debug at a certain point you can insert `set -x`{.markup--code
.markup--p-code} into your script and `set +x`{.markup--code
.markup--p-code} to end the section like the following:

<figure id="fa84" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-hoStGQvU0GLm96g.png"
class="graf-image" data-image-id="0*-hoStGQvU0GLm96g.png"
data-width="875" data-height="403" />
</figure>

So lets look at an example. This is our script from earlier being ran
with `bash -x ./example.sh`{.markup--code .markup--p-code}

<figure id="1941" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vrIlzPh6mEQy3sAM.png"
class="graf-image" data-image-id="0*vrIlzPh6mEQy3sAM.png"
data-width="875" data-height="390" />
</figure>

You can see its outputting a **+** for the command and then the output
of what that command executed. If there was an error it would output
a **--- **on that line this makes it easy to spot where you have gone
wrong so you can fix them.

We can also use multiple variables in something like an echo statement.
You aren't just limited to using 1!

<figure id="a528" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eKSCagPN9YabTp-v.png"
class="graf-image" data-image-id="0*eKSCagPN9YabTp-v.png"
data-width="875" data-height="339" />
</figure>

Answer the following questions and use this piece of code to guide you.

<figure id="92b7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cHtjVLszUjFES9r4.png"
class="graf-image" data-image-id="0*cHtjVLszUjFES9r4.png"
data-width="875" data-height="467" />
</figure>

**#1**: What would this code return?

> ***Answer: Jammy is 21 years old***

**#2**: How would you print out the city to the screen?

> ***Answer: echo \$city***

**#3**: How would you print out the country to the screen?

> ***Answer: echo \$country***

### Task 4: Parameters {#c1ef .graf .graf--h3 .graf-after--blockquote name="c1ef"}

We will now look at one of the main features of bash and that's using
parameters.

We will firstly look at parameters specified using the command line when
running the file. These come in many forms but often have the "\$"
prefix because a parameter is still a variable.

Lets start by declaring a parameter that is going to be our first
argument when running our bash script.

<figure id="2758" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1t1sfCLSXutPZxcI.png"
class="graf-image" data-image-id="0*1t1sfCLSXutPZxcI.png"
data-width="646" data-height="308" />
</figure>

We now run our script with `./example.sh Alex`{.markup--code
.markup--p-code}

And sure enough we get returned with "Alex"

So what if we wanted the 2nd argument? Well the process is very simple
and we simply add a `$2`{.markup--code .markup--p-code} instead of
`name=$1`{.markup--code .markup--p-code}

Then run with `./example.sh Alex Tony`{.markup--code .markup--p-code}

What do you think it would return?

And it would return "Tony".

What if we didn't want to supply them like this however, and instead it
would let us type in our name in a more interactive way, we can do this
using `read`{.markup--code .markup--p-code}.

<figure id="d4fe" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*J9ZV_VaM0n7iKs50.png"
class="graf-image" data-image-id="0*J9ZV_VaM0n7iKs50.png"
data-width="875" data-height="440" />
</figure>

This code will hang after its ran, this gives you the opportunity to
type in your name.

<figure id="17cd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uWUtb-HRcUtosIVy.png"
class="graf-image" data-image-id="0*uWUtb-HRcUtosIVy.png"
data-width="762" data-height="452" />
</figure>

And we can see that it worked!

Maybe try making a little biography maker, where you take the name, age,
and job as parameters. Store them inside a variable and then output them
to the screen inside a sentence.

However there is so much more that you can do with parameters and I
advice you to play around with them, after all practice is what makes
you better!

**#1**: How can we get the number of arguments supplied to a script?

> ***Answer: \$#***

**#2**: How can we get the filename of our current script(aka our first
argument)?

> ***Answer: \$0***

**#3**: How can we get the 4th argument supplied to the script?

> ***Answer: \$4***

**#4**: If a script asks us for input how can we direct our input into a
variable called 'test' using "read"

> ***Answer: read test***

**#5**: What will the output of "echo \$1 \$3" if the script was ran
with "./script.sh hello hola aloha"

> ***Answer: hello aloha***

### Task 5: Arrays {#fc17 .graf .graf--h3 .graf-after--blockquote name="fc17"}

For this module i suggest you follow along in the attackbox or a
standard linux terminal to make it easier to understand.

Arrays are used to store multiple pieces of data in one variable, which
can then be extracted by using an index. Most commonly notated as
`var[index_position]`{.markup--code .markup--p-code}.

Arrays use indexing meaning that each item in an array stands for a
number.

In the array `['car', 'train', 'bike', 'bus']`{.markup--code
.markup--p-code} each item has a corresponding index.

All indexes start at position 0

<figure id="c97a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qcEtTRH4-Dpc3K2J.png"
class="graf-image" data-image-id="0*qcEtTRH4-Dpc3K2J.png"
data-width="696" data-height="248" />
</figure>

Now we have covered this, let's make an array in bash.

The syntax is as follows.

We have the variable name, in our case 'transport'

We then wrap each item in brackets leaving a space between each item.

`transport=('car' 'train' 'bike' 'bus')`{.markup--code .markup--p-code}

We can then echo out all the elements in our array like this:

`echo "${transport[@]}"`{.markup--code .markup--p-code}

You can try this in your own terminal and see what it outputs.

Where the "@" means all arguments, and the \[\] wrapped around it
specifies its index.

So what if we wanted to print out the item `train`{.markup--code
.markup--p-code}.

We would simply type:

`echo "${transport[1]}"`{.markup--code .markup--p-code}

because the train is at index position 1.

The last thing we will cover is if we want to change an element, or
delete it. If we wanted to remove an element we would use the
`unset`{.markup--code .markup--p-code} utility.

`unset transport[1]`{.markup--code .markup--p-code}

This now removes the `train`{.markup--code .markup--p-code} item, if we
wanted to we could echo it back out and see that it is indeed gone,

Now lets set it to something else. We can do:

`transport[1]='trainride'`{.markup--code .markup--p-code}

If we echo the array then we get:

`car trainride bike bus`{.markup--code .markup--p-code}

So we successfully managed to swap out an element in our array!

As a little side project try building on your previosu project of a
biography maker, include arrays so that you can store multiple names and
multiple facts about the person. Then in the next module we can expand
even further.

Given the array please answer the following questions

`cars=('honda' 'audi' 'bmw' 'tesla')`{.markup--code .markup--p-code}

**#1**: What would be the command to print audi to the screen using
indexing.

> ***Answer: echo "\${cars\[1\]}"***

**#2**: If we wanted to remove tesla from the array how would we do so?

> ***Answer: unset cars\[3\]***

**#3**: How could we insert a new value called toyota to replace tesla?

> ***Answer: cars\[3\]="toyota"***

### Task 6: Conditionals {#7a9f .graf .graf--h3 .graf-after--blockquote name="7a9f"}

[https://i.ibb.co/k2DgyGg/carbon-19.pnghttps://i.ibb.co/k2DgyGg/carbon-19.pngWhen](https://i.ibb.co/k2DgyGg/carbon-19.pnghttps://i.ibb.co/k2DgyGg/carbon-19.pngWhen){.markup--anchor
.markup--p-anchor
data-href="https://i.ibb.co/k2DgyGg/carbon-19.pnghttps://i.ibb.co/k2DgyGg/carbon-19.pngWhen"
rel="noopener ugc nofollow noopener" target="_blank"} we talk about
conditionals it means that a certain piece of code relies on a condition
being met, this is often determined with relational operators, such as
equal to, greater than, and less than.

We will make a simple "if" statement to check if a variable is equal to
a value, we will also make a script that checks if a file exists and
that it is writeable, if it is we will write a message to that file, if
not writeable it will delete it and make a new one. A Lot of new things
will be taught here so pay attention.

First we will discuss the basic syntax of an if statement.

All if statements look like so:

<figure id="377b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9dH7u1A8g1pHFyul.png"
class="graf-image" data-image-id="0*9dH7u1A8g1pHFyul.png"
data-width="875" data-height="440" />
</figure>

Lets look at an example:

<figure id="481c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cE6HS3zHge9Z3aZ8.png"
class="graf-image" data-image-id="0*cE6HS3zHge9Z3aZ8.png"
data-width="875" data-height="430" />
</figure>

If statements always use a pair of brackets and in the case of the \[\]
we need to leave a space on both sides of the text(the bash syntax). We
also always need to end the if statement with `fi`{.markup--code
.markup--p-code}

Here a variable is being declared as 10 and in the top line of the if
statement the variable \$count is being compared to the integer 10.

If they are equal then it outputs **true**, if its false it outputs
**false**. As we know 10 is equal to 10 so it outputs true.

The **-eq** is one way of doing this, you could also use "**=**"

<figure id="764e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*StwLUClqP1wXWlA2.png"
class="graf-image" data-image-id="0*StwLUClqP1wXWlA2.png"
data-width="875" data-height="335" />
</figure>

\^\^\^\^\^ These are some examples.

So now let's use this to make a little script that compares an input(a
parameter) and checks it against a value to check if it's true or not. A
guessing game if you will.

<figure id="c437" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LBVlf5aAQY8AH8ZQ.png"
class="graf-image" data-image-id="0*LBVlf5aAQY8AH8ZQ.png"
data-width="875" data-height="522" />
</figure>

Now let's test this in our terminal.

`# ./example.sh guessme`{.markup--code .markup--p-code}

`"They are equal"`{.markup--code .markup--p-code}

`# ./example.sh hi`{.markup--code .markup--p-code}

`"They are not equal"`{.markup--code .markup--p-code}

And we can see that it works!

Feel free to play around with these and try making different
combinations and using different operators.

Now lets create another script where we will use 2 conditions
simultaneously and coming back to a concept we learnt in the first
lesson.

Lets begin.

We want to make a script that we will perform on a file given by a
**parameter**.

We then check if it exists and if it has **write** permissions. If it
has write perms then we echo "**hello**" to it. If it is either
non-accessible or doesn't exist we will create the file and echo "hello"
to it. Lets begin!

<figure id="e28a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rnNsIoT7w-UjB9cf.png"
class="graf-image" data-image-id="0*rnNsIoT7w-UjB9cf.png"
data-width="875" data-height="580" />
</figure>

`─# ./example.sh hello.txt ─# cat hello.txt`{.markup--code
.markup--p-code}

hello

And we can see that it worked!!

The -f checked if the file existed.

The -w checked if the file was writable, without write permissions we
wouldn't be able to output our text into the file.

To finish off our little project from the previous task. You can build
on your script using an if/else statement. Test to see if the age is
under 18, if it is then echo out their name with "You are not elegible
for work" or something along theese lines, if they are over 18 then ask
them for their job, you can do this with `read`{.markup--code
.markup--p-code}

Feel free to add anything you like and make it as complicated as you
wish and good luck with your project!

**#1**: What is the flag to check if we have read access to a file?

> ***Answer: -r***

**#2**: What is the flag to check to see if it's a directory?

> ***Answer: -d***

### Promote and Collaborate on Cybersecurity Insights {#32cd .graf .graf--h3 .graf-after--blockquote name="32cd"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#b57e .graf .graf--h3 .graf-after--p name="b57e"}

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
.h-card} on [August 24, 2024](https://medium.com/p/9336fbf488fb).

[Canonical
link](https://medium.com/@bevijaygupta/bash-scripting-tryhackme-writeup-9336fbf488fb){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
