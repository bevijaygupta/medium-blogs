---
title: "Linux Modules Tryhackme writeup 4f07b9e8561d"
platform: Medium
original_file: 2024-08-21_Linux-Modules-Tryhackme-writeup-4f07b9e8561d.md
---

# Linux Modules Tryhackme writeup 4f07b9e8561d

::: {}
# Linux Modules Tryhackme writeup {#linux-modules-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Linux Modules"
:::

::::::: {.section .e-content field="body"}
:::::: {#bb73 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux Modules Tryhackme writeup {#8429 .graf .graf--h3 .graf--leading .graf--title name="8429"}

**This is a Writeup of Tryhackme room "Linux Modules"**

<figure id="79e0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Yr-33-KnJkA1VbYo.png"
class="graf-image" data-image-id="0*Yr-33-KnJkA1VbYo.png"
data-width="512" data-height="262" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

This room is entirely based on, you can say revision, or may help you
familiarize more with terminal.

Note: This room is purely for familiarizing more with command line (so
no first bloods; Points Only) hence no need to rush, take your time in
doing this room. The hints with the tasks may contain direct answers, so
peek at your own risk.

Just a short intro on what's coming ahead:

- [du]{#2f01}
- [grep, egrep, fgrep]{#a97a}
- [tr]{#558d}
- [awk]{#5c63}
- [sed]{#0fd7}
- [xargs]{#1a6c}
- [curl]{#37c7}
- [wget]{#cd7a}
- [xxd]{#50d0}
- [and some more...]{#40b7}

I created this list so that I could read their documentation 1 by 1, and
this room is to save you from reading all those long man pages where
(while reading) you might not know the exact meanings of the flag used,
as you might just started linux, or may be didn't use it till that
extent to encounter that particular topic. Hope you get the idea...

### Scope of this room {#ba9d .graf .graf--h3 .graf-after--p name="ba9d"}

This room is based on understanding these tools so that they can reduce
our effort while working with the command line. Also, this skill that
you develop will help you manage your terminal sessions efficiently
while working on a pentest or any project.

Just make sure that you're using a linux VM, so that you can get a hands
on if you want to. Or simply start the attackbox(free users can deploy
the attackbox for an hour, which I think is pretty much enough time to
complete this room). I highly recommend to complete the "Linux
Fundamentals" rooms before proceeding further with these topics.

Happy Learning ;)

### Task 2: Mountain du {#499b .graf .graf--h3 .graf-after--p name="499b"}

### About the Beverage {#3de3 .graf .graf--h3 .graf-after--h3 name="3de3"}

Jk, it's not a beverage, `du`{.markup--code .markup--p-code} is a
command in linux (short for disk usage) which helps you identify what
files/directories are consuming how much space. If you run a simple du
command in terminal\...

<figure id="ca09" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*d3zv99eBC7dgD6X9.png"
class="graf-image" data-image-id="0*d3zv99eBC7dgD6X9.png"
data-width="577" data-height="183" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

The folders in their respective folders are listed here with the size
they occupy on the disk. The size here is shown in KB. Note: The files
inside a folder are not shown, only the folders are listed by running du
/\<directory\> command.

### Important flags {#c0ac .graf .graf--h3 .graf-after--p name="c0ac"}

<figure id="0292" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*s58pb6S16CeuBIyb.png"
class="graf-image" data-image-id="0*s58pb6S16CeuBIyb.png"
data-width="875" data-height="252" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

### Examples {#8e1a .graf .graf--h3 .graf-after--p name="8e1a"}

**du -a /home/** will list every file in the /home/ directory with their
sizes in KB.

If there's a lot of output you can surely use grep...

**du -a /home/ \| grep user** will list any file/directory whose name is
containing the string "*user*" in it.

### Final Words {#5994 .graf .graf--h3 .graf-after--p name="5994"}

du command can alternate `ls`{.markup--code .markup--p-code} with the
following flags:

**du --- time -d 1 .**

It won't specify you the user ownership though, so you can use
`stat `{.markup--code .markup--p-code}command on the file you want to
know who is the owner of that particular file

Syntax: **stat**

### Task 3: 0xef {#3f30 .graf .graf--h3 .graf-after--p name="3f30"}

Here we are gonna learn about 2 brothers and their mother i.e. (egrep,
fgrep, and grep).

IMPORTANT: To proceed further with this task, make sure you have
completed the "[**Regular
Expressions**](https://tryhackme.com/room/catregex){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/catregex"
rel="noopener ugc nofollow noopener" target="_blank"}**"** room by
[**concatenate**](https://tryhackme.com/p/concatenate){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/p/concatenate"
rel="noopener ugc nofollow noopener" target="_blank"}**.** This room
will brief you about the regular expressions that can come handy while
working with egrep.

There are a lot of rooms that you must have already done where you used
grep a lot of times, so most of this task will sound familiar to you, or
this is your first attempt on reading about grep, in any case, a 5 min
read won't harm your busy day...

### Introduction {#4807 .graf .graf--h3 .graf-after--p name="4807"}

It is a must known tool to everyone and that's why linux modules won't
be complete without doing a mention of its amazing charisma. This tool,
is what filters the good output we need from the residue. The official
documentation says, The grep filter searches a file for a particular
pattern of characters, and displays all lines that contain that pattern.
The pattern that is searched in the file is referred to as the regular
expression. The pattern is what I am gonna brief you about.

Syntax: **grep "PATTERN" file.txt** will search the file.txt for the
specified "PATTERN" string, if the string is found in the line, the grep
will return the whole line containing the "PATTERN" string.

### The Family Tree {#55f9 .graf .graf--h3 .graf-after--p name="55f9"}

egrep and fgrep are no different from grep(other than 2 flags that can
be used with grep to function as both). In simple words, egrep matches
the regular expressions in a string, and fgrep searches for a fixed
string inside text. Now grep can do both their jobs by using -E and -F
flag, respectively.

In other terms, `grep -E`{.markup--code .markup--p-code} functions same
as `egrep `{.markup--code .markup--p-code}and `grep -F`{.markup--code
.markup--p-code} functions same as `fgrep`{.markup--code
.markup--p-code}.

### Important Flags {#11ce .graf .graf--h3 .graf-after--p name="11ce"}

<figure id="30ac" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*_D78Vt5oLN9IuHqe.png"
class="graf-image" data-image-id="0*_D78Vt5oLN9IuHqe.png"
data-width="875" data-height="386" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You might be wondering the difference between -E and -e flag. I suggest
to understand this as the following:

- [-e flag can be used to specify multiple patterns, with multiple use
  of -e flag( grep -e PATTERN1 -e PATTERN2 -e PATTERN3 file.txt),
  whereas, -E can be used to specify one single pattern(You can't use -E
  multiple times within a single grep statement).]{#39c7}

Other point that you can use to understand the difference is, -e works
on the BREs(Basic Regular Expressions) and -E works on EREs (Extended
Regular Expressions).

- [BREs tend to match a single pattern in a file (Simplest examples can
  be direct words like "sun", "comic")]{#d438}
- [EREs tend to match 2 or more patterns in a file (To select a no of
  words like (sun sunyon sandston) the pattern could be
  "\^s.\*n\$").]{#62ba}

Hope, you get an idea how this works.

Here's a real short note, you might wanna read, on official GNU
documentation: [**Basic vs Extended (GNU Grep
3.5)**](https://www.gnu.org/software/grep/manual/html_node/Basic-vs-Extended.html){.markup--anchor
.markup--p-anchor
data-href="https://www.gnu.org/software/grep/manual/html_node/Basic-vs-Extended.html"
rel="noopener ugc nofollow noopener" target="_blank"}**.** If you didn't
understand much from that paragraph, make sure, you've practiced your
regex well.

**Q.1**: Is there a difference between egrep and fgrep? (Yea/Nay)

> ***Answer: yea***

**Q.2:** Which flag do you use to list out all the lines NOT containing
the 'PATTERN'?

> ***Answer: -v***

Download the above given file and answer the following questions.

**Q.1:** What user did you find in that file?

<figure id="131f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jPVHFVhsxewQmBRz.png"
class="graf-image" data-image-id="0*jPVHFVhsxewQmBRz.png"
data-width="875" data-height="112" />
</figure>

> ***Answer: bobthebuilder***

**Q.2:** What is the password of that user?

<figure id="a9f7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7z8BFOzeiE8VzH87.png"
class="graf-image" data-image-id="0*7z8BFOzeiE8VzH87.png"
data-width="875" data-height="116" />
</figure>

> ***Answer: LinuxIsGawd***

**Q.3:** Can you find the comment that user just left?

<figure id="2e83" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kKIodBLAjr81GMsb.png"
class="graf-image" data-image-id="0*kKIodBLAjr81GMsb.png"
data-width="875" data-height="108" />
</figure>

> ***Answer: fs0ciety***

### Task 4: Did someone said STROPS? {#e1fd .graf .graf--h3 .graf-after--blockquote name="e1fd"}

String Manipulations (STRing OPerationS)

Many people discard this topic in their tutorials/courses, which I
believe is leaving behind the true power of linux and it's terminal
interface. You ever see someone typing a very long command piping their
outputs into some other commands? Well believe me when I say, you can
select a single byte character from a GB long array of string bytes, if
you could master that.

If you're from a programming background you might have used indexing in
arrays, slicing in python, or even grepping in terminal... All are a
means of string manipulations. Especially in bash, we have a TON of
tools to perform a same kind of operation, with different flags or
string patterns specified, but obviously we will be choosing the one,
providing us the shortest and easiest syntax possible.

For strops, we have the following tools that I always keep in my arsenal
and you should too:

- [tr]{#a881}
- [awk]{#cbd9}
- [sed]{#4d04}
- [xargs]{#5d51}

Other commands to be familiar with:

- [sort]{#864b}
- [uniq]{#32f4}

I am gonna walk you through the commands I mentioned above in the
following tasks.

### Task 5: Shall I try morsecode? {#90bb .graf .graf--h3 .graf-after--p name="90bb"}

The answer is no... Translate command(`tr`{.markup--code
.markup--p-code}) doesn\'t translate morse code. A short introduction on
tr command is, it can help you in number of ways, ranging from changing
character cases in a string to replacing characters in a string. It\'s
awesome at it\'s usage. Plus, it\'s the easiest command and a must know
module for quick operations on strings.

Syntax:

``` {#f84d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
tr [flags] [source]/[find]/[select] [destination]/[replace]/[change]
```

This I guess is an appropriate representation of how you can use this
tool. Moreover, we have the following flags offered by this command:

<figure id="70a8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PZQdiDhmqDQyG9fX.png"
class="graf-image" data-image-id="0*PZQdiDhmqDQyG9fX.png"
data-width="875" data-height="201" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You must have noticed the word "set" while reading the flags. Well
that's true... tr command works in sets of character.

Examples

- [If you want to convert every alphabetic character to upper
  case.]{#0c4a}

<figure id="026b" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*dMezyowJ-NoFgmFP.png"
class="graf-image" data-image-id="0*dMezyowJ-NoFgmFP.png"
data-width="622" data-height="225" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Or I am not sure, if you ever used emojis on discord, coz on desktop app
you could use emojis using :keyword:. Similarly, tr allows us to select
a set by these keywords. In that case the output would be same.

`cat file.txt | tr -s '[:lower:]' '[:upper:]'`{.markup--code
.markup--p-code}

There are more of these (interpreted sequences) which you can view, by
just `tr --help`{.markup--code .markup--p-code} command. I am not
including them here, because they are just straight forward, and you\'ve
been using most of them, if you\'re familiar with (mostly) any
programming language out there.

- [If you want to view creds of a user which are in digits.]{#8854}

<figure id="a8f7" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*rI-PsoP37Kbo-MTX.png"
class="graf-image" data-image-id="0*rI-PsoP37Kbo-MTX.png"
data-width="570" data-height="131" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see that I used regex here, and deleted all lower/upper case
characters, including the (:) symbol and a space.

Note: This is a short note on how you can use this tool. Now try out
these features on your own and get use to this tool. You can also refer
to the following sites for more on the tool:

- [[**tr command in Unix/Linux with
  examples --- GeeksforGeeks**](https://www.geeksforgeeks.org/tr-command-in-unix-linux-with-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/tr-command-in-unix-linux-with-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#2c03}
- [[**Tr Command in Linux with Examples \|
  Linuxize**](https://linuxize.com/post/linux-tr-command/){.markup--anchor
  .markup--li-anchor
  data-href="https://linuxize.com/post/linux-tr-command/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#b91c}

**Q.1**: Run tr --- help command and tell how will you select any digit
character in the string?

> ***Answer: :digit:***

**Q.2:** What sequence is equivalent to \[a-zA-Z\] set?

> ***Answer: :alpha:***

**Q.3:** What sequence is equivalent to selecting hexadecimal
characters?

> ***Answer: :xdigit:***

### Task 6: AWWKAY {#618c .graf .graf--h3 .graf-after--blockquote name="618c"}

The AWK Command

This is the most-est powerful tool in my arsenal, I can't think of any
other command that can do something and not awk. It's like the
all-in-one tool. If you ever played CSGO, you can totally relate AWK
with AWP(the killer weapon).

*"Awk is a scripting language used for manipulating data and generating
reports.The awk command programming language requires no compiling, and
allows the user to use variables, numeric functions, string functions,
and logical operators."*

Sidenote: Just because it's the super tool, that's not necessary that
there is no need to learn about other tools. The awk commands can be
fairly longer to solve an operation than that of sed or xargs. A GNU
project of awk (namely, gawk) which is also the one installed on every
linux distro, is compatible with both awk and nawk( New-awk; also
project by AT&T).

Syntax:

``` {#8575 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
awk [flags] [select pattern/find(sort)/commands] [input file]
```

Note: awk does support getting output via piping.

- [If the commands you wrote are in a script you can execute the script
  commands by using the `-f`{.markup--code .markup--li-code} flag and
  specifying the name of the script file.
  (`awk -f script.awk input.txt`{.markup--code
  .markup--li-code})]{#e7b9}

Using AWK

- [To simply print a file with awk.]{#d026}

<figure id="28a1" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*dF5hFNpx6qFrJ-5Z.png"
class="graf-image" data-image-id="0*dF5hFNpx6qFrJ-5Z.png"
data-width="448" data-height="308" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see it simply just printed out data from file.txt.

- [To search for a pattern inside a file you enclose the pattern in
  forward slashes `/pattern/`{.markup--code .markup--li-code}. For
  instance, if I want to know who all plays CTF competitions the command
  should be like: `awk '/ctf/' file.txt`{.markup--code
  .markup--li-code}]{#6190}

<figure id="c670" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*Psx5kAA0b3I3TTRb.png"
class="graf-image" data-image-id="0*Psx5kAA0b3I3TTRb.png"
data-width="441" data-height="67" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Built-In variables in AWK

Let's talk a little bit about some of the in-built variables. Built-in
variables include field variables (\$1, \$2, \$3 .. \$n). These field
variables are used to specify a piece of data (data separated by a
delimeter defaulting to space). If I run
`awk '{print $1 $3}' file.txt`{.markup--code .markup--p-code} it will
list me the words that are at 1st and 3rd fields.

<figure id="b8ee" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7kZwzuaPj4B51as8.png"
class="graf-image" data-image-id="0*7kZwzuaPj4B51as8.png"
data-width="517" data-height="157" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see, it joined the words together because we didn't specify the
output delimeter. We will come to that later in this task. Right now,
let's just use a ","(comma) to bring the space.

Note: You may notice the use of {} around the print statement, that's
where we used a function. To use commands in awk scripts, you need to
mention them inside a function.

<figure id="e62a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QgzqKJhH8t0aviGs.png"
class="graf-image" data-image-id="0*QgzqKJhH8t0aviGs.png"
data-width="577" data-height="157" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Great, this seems a little nice.

Note: The \$0 variable points to the whole line. *Also, make sure to use
single quotes('') to specify patterns, awk treats double quotes("") as a
raw string. To use double quotes make sure that you escape the (\$)
sign(s) with a backslash (\\) each, to make it work properly.*

More on variables

**NR:** (Number Record) is the variable that keeps count of the rows
after each line's execution... You can use NR command to number the
lines (`awk '{print NR,$0}' file.txt`{.markup--code .markup--p-code}).
Note that awk considers rows as records.

<figure id="8b04" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xEmuiuUzeBGN3Foj.png"
class="graf-image" data-image-id="0*xEmuiuUzeBGN3Foj.png"
data-width="528" data-height="157" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

**FS:** (Field Separator) is the variable to set in case you want to
define the field for input stream. The field separation (defaut to
space) that we talked above and can be altered to whatever you want
while specifying the pattern. FS can be defined to another
character(s)(yea, can be plural) at the BEGIN{command}.

<figure id="19b1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2u2zcnV_AECTiLZf.png"
class="graf-image" data-image-id="0*2u2zcnV_AECTiLZf.png"
data-width="617" data-height="157" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

If you don't know the BEGIN yet, take it as a pattern that we specify
and following is the action on that pattern. Similarly, there is END
command, this is also a pattern that we specify, following the action to
perform on that pattern, and simply, we use them to define *actions*
like Field Separator, Record Separator etc. that are to be performed at
the start and at the end of the script, respectively.

`awk "BEGIN {FS='o'} {print $1,$3} END{print 'Total Rows=',NR}"`{.markup--code
.markup--p-code}

<figure id="8502" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ge7utTRmJU7uCvQv.png"
class="graf-image" data-image-id="0*ge7utTRmJU7uCvQv.png"
data-width="875" data-height="165" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

The output is weird because I separated the fields using a letter that
was making sense with the words in text. In short, this is actually how
a complete script is written in awk.

**RS**: (Record Separator): By default it separate rows with '\\n', you
can specify something else too.

<figure id="27c5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rOuPa7Bo7WXk8Y5x.png"
class="graf-image" data-image-id="0*rOuPa7Bo7WXk8Y5x.png"
data-width="672" data-height="443" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Notice that their has been a new line created wherever 'o' was used. It
also interpreted '\\n' used in the text file, so there are new lines
after end of every number too.

**OFS:** (Output Field Separator) You must have gathered some idea by
the full form, it is to specify a delimeter while outputing...

<figure id="c696" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*98VHGL6wifSWoSQ4.png"
class="graf-image" data-image-id="0*98VHGL6wifSWoSQ4.png"
data-width="725" data-height="338" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

I used OFS in both the commands, you can see that only in 2nd one the
delimiter was used. Note that the output field separator will separate
fields using (:) only when the fields are defined with the print
statement. With \$0 I didn't had anything else, if it were to be \$0,\$0
then the lines would be joining their reflection(non-laterally) with a
colon(:).

<figure id="48de" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*erekBC00CnSkmZzj.png"
class="graf-image" data-image-id="0*erekBC00CnSkmZzj.png"
data-width="725" data-height="182" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

**ORS:** (Output Record Separator) I don't think I really need to
specify it's usage...

<figure id="10e1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iIuOYN4Wy70QS7K3.png"
class="graf-image" data-image-id="0*iIuOYN4Wy70QS7K3.png"
data-width="727" data-height="283" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

My delimiter was a double new-line character.

This is not it... There is a lot more on AWK, you can do operations,
find string length, use conditions to sort, regex within awk and other
fun stuff. But I guess the task is already went a lot longer. Let's
quickly move on to some important flags that can come in handy while
doing strops.

JIC if you wanna read more on the tool, here are some great resources
regarding awk scripting.

- [[AWK --- Workflow --- Tutorialspoint](https://www.tutorialspoint.com/awk/awk_workflow.htm){.markup--anchor
  .markup--li-anchor
  data-href="https://www.tutorialspoint.com/awk/awk_workflow.htm"
  rel="noopener ugc nofollow noopener" target="_blank"} (For learning
  awk scripting in brief and quick)]{#5302}
- [[The printf statement in
  awk](http://osr5doc.xinuos.com/en/OSUserG/_The_printf_statement.html){.markup--anchor
  .markup--li-anchor
  data-href="http://osr5doc.xinuos.com/en/OSUserG/_The_printf_statement.html"
  rel="noopener ugc nofollow noopener" target="_blank"} (If you want to
  do more with formatting strings; you can use printf function
  also)]{#0986}
- [[AWK command in Unix/Linux with
  examples --- GeeksforGeeks](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/awk-command-unixlinux-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#2fdc}
- [And if you really want to dive deep on this tool, do check out man
  pages on gawk]{#f9f3}

**Important Flags**

<figure id="f9fd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HZXPHSXrWOmqNMGL.png"
class="graf-image" data-image-id="0*HZXPHSXrWOmqNMGL.png"
data-width="875" data-height="215" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

There are other flags as well, but they are of not much use. Especially
if you're learning this as a beginner

Just relax if you don't get much of this task, learning a scripting
language inside a single task is not an easy job. Just make sure you
understood the above told syntax well and followed the resources, rest
is all practice :-).

Ending this task with a fun fact, AWK is abbreviated after it's creators
(Aho, Weinberger, and Kernighan).

Download the above given file, and use awk command to print the
following output:

*ippsec:34024\
john:50024\
thecybermentor:25923\
liveoverflow:45345\
nahamsec:12365\
stok:1234*

<figure id="33da" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cBCPFn8MuXbcECLi.png"
class="graf-image" data-image-id="0*cBCPFn8MuXbcECLi.png"
data-width="371" data-height="181" />
</figure>

How will you make the output as following (there can be multiple; answer
it using the above specified variables in BEGIN pattern):

<figure id="c27f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8lOkvaEyTsrJAE1G.png"
class="graf-image" data-image-id="0*8lOkvaEyTsrJAE1G.png"
data-width="575" data-height="184" />
</figure>

> ***Answer: awk 'BEGIN{FS=" "; OFS=":"} {print \$1,\$4}' awk.txt***

ippsec, john, thecybermentor, liveoverflow, nahamsec, stok,

<figure id="15bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VSe9EoB6jb-NODSa.png"
class="graf-image" data-image-id="0*VSe9EoB6jb-NODSa.png"
data-width="622" data-height="92" />
</figure>

> ***Answer: awk 'BEGIN{ORS=", "} {print \$1}' awk.txt***

### Task 7: That's what she sed {#f507 .graf .graf--h3 .graf-after--blockquote name="f507"}

The sed life

sed(Stream EDitor) is a tool that can perform a number of string
operations. Listing a few, could be: FIND AND REPLACE, searching,
insertion, deletion. I think sed of a stream-oriented vi editor... Ok so
a few questions popped up, like how? and what is stream-oriented? Let's
not dive deep into streams, just keep in mind that I said it in contrast
with "orientation with input stream". You can't call vi stream oriented,
because it doesn't work with neither of input or output stream.

On the other hand, you can easily perform operations with sed command by
either piping the input or redirecting(\<) the input from a file. I
compared it with vi, because while learning this command I kinda missed
using vim, since I shifted to sublime(No offence to vim fanboys/fangirls
out there, I just use sublime to keep things common between my windows
and linux machine and it's a great lightweight editor, so uk).

Syntax: `sed [flags] [pattern/script] [input file]`{.markup--code
.markup--p-code}

**Important Flags**

<figure id="8d3b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ngdbILsWSDDs6NXp.png"
class="graf-image" data-image-id="0*ngdbILsWSDDs6NXp.png"
data-width="875" data-height="227" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

**The sed command**

There are endless ways of using sed. I am gonna walk you through a very
detailed general syntax of (mostly all) sed patterns, with some general
examples. Rest is your thinking and creativity, on how YOU utilize this
tool.

<figure id="9405" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vB2gDA0FvLxFLt3h.png"
class="graf-image" data-image-id="0*vB2gDA0FvLxFLt3h.png"
data-width="875" data-height="53" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Hope these colors could have helped you identify the parts. If you have
any previous knowledge of sed, feel free to co-relate. Again, this is
just the pattern inside sed command (excluding external flags). Also,
note the single quotes at the start/end.

Hmm, but may be, it's still not clear. Alright let's take a simple
example to relate this.

<figure id="b2eb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IcqWB14YW0h5QQb4.png"
class="graf-image" data-image-id="0*IcqWB14YW0h5QQb4.png"
data-width="270" data-height="37" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Let's not care about what's meaning of 1,3 all that slashes, that s,g.
And focus on the color codes. Hope the syntax is now making a little
sense... Great. Moving forward to flags.

**The purple gang**

<figure id="ecd2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OOIQnur8F_RHdm5F.png"
class="graf-image" data-image-id="0*OOIQnur8F_RHdm5F.png"
data-width="875" data-height="149" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

**The green gang**

<figure id="d57b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*w5NNFB7iz3eYo5HF.png"
class="graf-image" data-image-id="0*w5NNFB7iz3eYo5HF.png"
data-width="875" data-height="258" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Let's see these in action... Explaining the previously taken command,
(sed -e '1,3 s/john/JOHN/g' file.txt)

- [Starting with the sed keyword itself, initializes the sed
  command.]{#39c8}
- [With -e flag specifying that following is a script command.(you don't
  need to specify -e if it's a single command; as it will be
  automatically interpreted by sed as a positional argument)]{#cb23}
- [Then comes the pattern. Starting with the **yellow** portion is the
  condition(which is/are btw, generally on lines inside a file),
  specifying to take range of lines 1,3 (line index starts from 1) and
  execute the following code on that range of lines. Following a space
  comes the **mode,** specifying that we need to use a substitution
  mode(as we are substituting a value) by using s. Then we specify / as
  a delimiter to differentiate between the parts of code. After the
  first slash came the **pattern** we want to operate the substitution
  on(you may choose to use regex in this region too). Following the 2nd
  slash comes the **string** we want to replace the pattern with.
  Finally, after the last slash was an arg/flag, /g specifying to
  operate this operation globally, wherever the pattern was
  found.]{#de15}
- [Finally was the filename we want to take input from and apply
  operation/code that we specified beside it.]{#5687}

Hope there is no confusion as per sed is concerned. Hence, the output
for the above command would be like:

would be like:

<figure id="1883" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iGsb7JXmAp5elM0P.png"
class="graf-image" data-image-id="0*iGsb7JXmAp5elM0P.png"
data-width="580" data-height="157" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Let's view a few more examples to get the concept clear:

- [Viewing a range of Lines]{#8e84}

<figure id="f014" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*FrhmtMryHBZGEmgf.png"
class="graf-image" data-image-id="0*FrhmtMryHBZGEmgf.png"
data-width="463" data-height="92" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

-n flag suppressed the output and we got the duplicates created by p
arg.

- [Viewing the entire file except a given range]{#1310}

<figure id="fcb4" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*y_KNJhQkUwkoowOU.png"
class="graf-image" data-image-id="0*y_KNJhQkUwkoowOU.png"
data-width="422" data-height="91" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

- [Viewing multiple ranges of lines inside a file]{#7ed6}

<figure id="595c" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*1JYuO9OAQN1-pmq4.png"
class="graf-image" data-image-id="0*1JYuO9OAQN1-pmq4.png"
data-width="578" data-height="112" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

- [To start searching from nth pattern occurrence in a line you can use
  combination of /g with /1,/2,/3.]{#b879}

<figure id="c65a" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*JipHm1gULjzd7GF9.png"
class="graf-image" data-image-id="0*JipHm1gULjzd7GF9.png"
data-width="586" data-height="345" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see when I specified /1 it gave a change in the text, with /2 it
didn't. This is because there was only 1 occurrence of the string
"youtube", and the 2nd occurrence couldn't be found. Also I didn't used
1g or 2g because there were no further occurrences of the pattern, so
there is no need to use it. Still it would have worked the same, if
used. Try it on your own.

- [If you have log files to view which have trailing white spaces, and
  it is hard to read them, then you can fix that using regex.]{#8498}

<figure id="7103" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*GFbDBAkgXgqVWOTs.png"
class="graf-image" data-image-id="0*GFbDBAkgXgqVWOTs.png"
data-width="602" data-height="312" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Let's take one last example on this sed command.

- [More on regex can be: Making every line to start with a bullet point
  and enclose the digits in square brackets... Ok, but how? Let's first
  view it, and then we'll take a look at the explanation.]{#521c}

<figure id="5b7a" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*qV1aDnuxynlfn2Qy.png"
class="graf-image" data-image-id="0*qV1aDnuxynlfn2Qy.png"
data-width="875" data-height="326" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

"What is this?! where's that :alpha: came from? I understand the \\b is
part of regex you used, following those, un-identifiable escape
characters and some \\1 and \\2 referenced either wrong, as it's /1, /2
to identify the nth occurrence. I mean, it's so confusing".

I agree, it's so noisy, and hard to read. But believe 70% of it is
nothing to do with `sed`{.markup--code .markup--p-code}, it\'s all
regex, so take your time. Try to understand what the regex is doing.
Rest the \"to-be-replaced\" part is just a way sed is assigning the
groups to it\'s default variables we created within regex.

**Explanation**

<figure id="c41e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vsIYYd6pkS3Ey_MI.png"
class="graf-image" data-image-id="0*vsIYYd6pkS3Ey_MI.png"
data-width="450" data-height="42" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Hope things are a little clear, by undertaking the knowledge of previous
color coding. You can easily differentiate the mode, pattern,
to-be-replaced string. *Later I removed the background from the part
belonging to the keywords in sed. As there was some issue in changing
the font color, it just won't persist.*

- [Starting with the regex part. Opening a group with escape character,
  \^ to put the cursor at the starting of the line, and then \\b
  represents to search for beginning of a word, and then defines a set
  of characters to include, following a "\*" to specify 'n' number of
  characters. Then closes the group by escaping the closing brackets.
  Creating another regex group, using escape sequence, we then
  initialized another set and specified \* at the end of the set to take
  n characters of that set, at last group is closed using escape
  sequence.]{#4b8e}
- [At the replaced end, we are using escape sequences to make a
  bullet(it's just a good practice to use escape sequence with every
  symbolic character; even if the output is same), then we have escape
  characters for the square brackets enclosing a sed variable /2 (after
  /1 which is coming up).]{#93f7}
- [Now its turn for the sed's keyword part. We used \[:alpha:\] in the
  set defined by regex, which is nothing but another representation of
  using `a-zA-Z`{.markup--code .markup--li-code} in regex, which means
  to capture any alphabetic characters. sed offers such keywords(calling
  them \"bracket expressions\"), which we can use to make the input code
  look cleaner. Similarly we used the bracket expression for specifying
  digit as well which we specified using \[:digit:\].]{#7356}

Note: There's a space after the first bracket expression inside the
regex set (\[\[:alpha:\]{space}\]). As you see, this space was to
indicate the regex set *so that \* could take multiple words until the
digits start occurring in the text(regex logic)*.

- [Then there are some in-built variables as we saw in awp awk, that we
  used in the to-be-replace part of sed. \\1 depicted the first group
  which selected everything until the first character occurred. The
  second group comprised of a set consisting decimal characters, which
  were enclosed with \[\\2\] with the use of escseq.]{#ba91}

Here, we finished learning about sed variables, the number of groups you
create with regex, can be later indexed as variable \\n in sed.

Well this is pretty much it, on the sed command. If you want to learn
more, check-out the resources on the sed command.

Resources:

- [[Sed Command in Linux/Unix with
  examples --- GeeksforGeeks](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#261b}
- [[sed, a stream editor
  (gnu.org)](https://www.gnu.org/software/sed/manual/sed.html){.markup--anchor
  .markup--li-anchor
  data-href="https://www.gnu.org/software/sed/manual/sed.html"
  rel="noopener ugc nofollow noopener" target="_blank"} (Official
  Documentation)]{#3e82}
- [[15 Useful 'sed' Command Tips and Tricks for Daily Linux System
  Administration Tasks
  (tecmint.com)](https://www.tecmint.com/linux-sed-command-tips-tricks/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.tecmint.com/linux-sed-command-tips-tricks/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#38a3}

Again, if there is not much you could learn about this command don't
feel bad, just go through the resources and try practicing by making
your own texts and play with this command.

<figure id="81cb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0bqM8Ul4tgOCAr33.png"
class="graf-image" data-image-id="0*0bqM8Ul4tgOCAr33.png"
data-width="362" data-height="85" />
</figure>

**Q.1:** How would you substitute every 3rd occurrence of the word
'hack' to 'back' on every line inside the file file.txt?

> ***Answer: sed 's/hack/back/3g' file.txt***

**Q.2:** How will you do the same operation only on 3rd and 4th line in
file.txt?

> ***Answer: sed '3,4 s/hack/back/3g' file.txt***

**Q.3:** Download the given file, and try formatting the trailing spaces
in sed1.txt with a colon(:).

<figure id="b9b6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lhlml-q68ai0cjTC.png"
class="graf-image" data-image-id="0*lhlml-q68ai0cjTC.png"
data-width="433" data-height="189" />
</figure>

**Q.4:** View the sed2 file in the directory. Try putting all
alphabetical values together, to get the answer for this question.

<figure id="d230" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HME_fma0lwykPUs8.png"
class="graf-image" data-image-id="0*HME_fma0lwykPUs8.png"
data-width="387" data-height="242" />
</figure>

> ***Answer: CONGRATULATIONS YOU MADE IT THROUGH THIS SMALL LITTLE
> CHALLENGE***

**Q.5:** What pattern did you use to reach that answer string?

> ***Answer: 's/\[\[:digit:\]\]//g'***

Alternatively, you can use tr to remove all the digits, and then pipe
the output in sed to remove trailing whitespaces.

cat sed2.txt \| tr '\[:digit:\]' ' ' \| sed 's/ \*//g'

**Q.6:** What did she sed?(In double quotes)

> ***Answer: "That's What"***

### Task 8: My x-args a lot {#009f .graf .graf--h3 .graf-after--blockquote name="009f"}

xargs, a very simple command to use when it comes to make passed string
a command's argument, technically, positional argument. The official
documentation says, xargs is a command line tool used to build and
execute command from the standard input.

**Important flags**

<figure id="60b4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hP8GYQWblrpbqtwm.png"
class="graf-image" data-image-id="0*hP8GYQWblrpbqtwm.png"
data-width="875" data-height="535" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

xargs packs with a very large option of flags, although, a very simple
tool to work with. You don't have to stress too much on xargs, it is
just a small tool like sort, uniq (Coming soon). Go through the
following examples and then I have a useful note, *on using flags as a
positional arguments.*

Examples

- [What if we want to run multiple command with xargs in one
  line.]{#8a81}

<figure id="ae19" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*nQj48BZjQ1EL11HA.png"
class="graf-image" data-image-id="0*nQj48BZjQ1EL11HA.png"
data-width="875" data-height="94" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see I defined a variable *argVar* to use later in the 2 commands
I ran with `bash -c`{.markup--code .markup--p-code}.

- [You can use xargs with conjunction to find command to enhance the
  search results.]{#90a2}

<figure id="f8ae" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*OPY1g_ARnIIOoWAT.png"
class="graf-image" data-image-id="0*OPY1g_ARnIIOoWAT.png"
data-width="875" data-height="135" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Note: The find command prints results to standard output by default, so
the `-print`{.markup--code .markup--p-code} option is normally not
needed, but `-print0`{.markup--code .markup--p-code} separates the
filenames with a \\0 (NULL) byte so that names containing spaces or
newlines can be interpreted correctly.

- [You can use xargs command to grep a text from any file in any
  directory meeting a specific pattern/criteria.]{#bc8b}

<figure id="c59a" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*jRVdpJV1W6Nhk-qB.png"
class="graf-image" data-image-id="0*jRVdpJV1W6Nhk-qB.png"
data-width="875" data-height="326" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see that I used xargs to grep a pattern matching anything
starting with r with any bunch of characters\[:alnum:\] and ending with
0. Which returned me this string. If you want to practice on your own,
you can find flag.txt file inside the downloaded zip archive. Pick a
string find a unique pattern for it and then grep it. Peace.

Note: If the xargs is having same flags, that can also be interpreted by
the following module, in that case you need not worry, because the flags
used after the command are the one's that are interpreted. Just keep
that in mind and you're good to go.

A note on XARGS (and almost every command line module in linux/unix
system)

Let's take an example from one of the rooms I solved on privilege
escalating through tar running as super user. Room: [Linux PrivEsc \|
Task 10](https://tryhackme.com/room/linuxprivesc){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxprivesc"
rel="noopener ugc nofollow noopener" target="_blank"}

Gtfobins said, "tar -cf /dev/null
/dev/null --- checkpoint=1 --- checkpoint-action=exec=/bin/sh"

Great, but the catch in the challenge was, sudo was not given to tar,
SUID permissions were given to a file, which was not allowed to be
edited by any other user(owner: root). So if that script has to run it
will run with the root privileges. What we could do is make the files in
that directory in flag format, that tar could interpret as it's flag. So
when in our case, tar would start scanning the directory to get the
overview of the files to compress and combine them, it will interpret
those flags and will give us root shell.

Awesome technique. Isn't it? Well that's not the point. The point here
is, I found a little difficulty in creating those files (via command
line) with --- appended to them. I tried xargs but didn't work. I then
found an article
[here](https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/){.markup--anchor
.markup--p-anchor
data-href="https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/"
rel="noopener ugc nofollow noopener" target="_blank"}, which helped me
and I solved the challenge. Then when I started with the 5th phase of
hacking(Covering Tracks). I couldn't seem to delete those earlier
created `--checkpoint`{.markup--code .markup--p-code} files with
`rm`{.markup--code .markup--p-code}. I tried for an hour or so, but
couldn\'t and left. Well, I didn\'t knew this, until I started reading
documentations and man pages. Call it an instinct or just luck that I
found a way to *escape command line flags as a positional argument*. Why
all this theory, when I can simply get to this point? Well, I believe
that it\'s just a better way of learning, when you can append your
learnings with an event that had previously occurred. So later, I was
able to remove the files using the following command.

`rm -- --checkpoint=1`{.markup--code .markup--p-code}

`rm -- --checkpoint-action=exec=sh`{.markup--code .markup--p-code}

Notice something different? I was able to escape the following flags
using an empty flag notation. Infact. This padding technique works in
ALMOST EVERY command line module available for linux, unix systems.
Let's see this in action with xargs, and know that if this theory
actually works.

<figure id="608b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*C0PllpfwvLG_80lu.png"
class="graf-image" data-image-id="0*C0PllpfwvLG_80lu.png"
data-width="670" data-height="173" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see the rm didn't interpreted the files inside directory as a
flag when used --- padding. Also before we move forward, I want to show
one more thing...

<figure id="83f0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-esnh4NjpTSxQ2sM.png"
class="graf-image" data-image-id="0*-esnh4NjpTSxQ2sM.png"
data-width="875" data-height="47" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Wutt? I gave the padding it still showed me an error. Hmm... Did you
found what was the issue? Well even if you specify that padding to
escape the flags there are '/'s inside this string, which are making
`touch`{.markup--code .markup--p-code} to interpret them as create the
file *bash*, inside *bin* directory that is inside, some
*\--checkpoint-action=exec=* directory. You may try using \\/bin\\/bash
to escape the slashes, but that won\'t work either, because files can\'t
contain slashes in their name.

We can easily bypass this by just using bash or sh instead of specifying
the whole path, but make sure that your path is set to normal. Moving
forward...

<figure id="531c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KS6JrIxwTKWq53aR.png"
class="graf-image" data-image-id="0*KS6JrIxwTKWq53aR.png"
data-width="875" data-height="85" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Focus on the -n2 I used after xargs. 2 arguments at once, in first loop
`touch -- --checkpoint=1`{.markup--code .markup--p-code}, then
`touch -- --checkpoint-action=exec=sh`{.markup--code .markup--p-code}.
Now let\'s try running tar.

<figure id="3e79" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ne7QftU2lciv2Z6V.png"
class="graf-image" data-image-id="0*Ne7QftU2lciv2Z6V.png"
data-width="546" data-height="103" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Ohh ok, I see where the problem occurred, those 2 flag files that we
created were interpreted as flags and then tar had nothing to compress,
that's not a problem, let's create a testfile...

<figure id="edd0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*C5IeqIEmLZ0gUejb.png"
class="graf-image" data-image-id="0*C5IeqIEmLZ0gUejb.png"
data-width="561" data-height="226" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Bingo, we got a shell(not as root, because that was executed as my user.
Could give us root, if ran as it).

Hope this last was a good example on xargs usage. Remember, xargs is a
great command when it comes to handling command line arguments. It's not
a very vast tool which you could dive in. Though it has max-ly covered
all the areas in it's domain of passing and handling arguments to other
modules/commands. Like a sidekick, this can help you ease your daily
tasks. So keep a space for this tool in your arsenal.

**Q.1:** You're working in a team and your team leader sent you a list
of files that needs to be created ASAP within current directory so that
he can fake the synopsis report (that needs to be submitted within a
minute or 2) to the invigilator and change the permissions to read-only
to only you(Numberic representation). You can find the files list in the
"one" folder.

Use the following flags in ASCII order:

- [Verbose]{#bfdb}
- [Take argument as "files"]{#f701}

> ***Answer: cat file \| xargs -I files -t sh -c "touch files; chmod 400
> files"***

**Q.2:** You can find the files for this task in two folder.

> ***Answer: ls \| xargs -I word -n 1 -t sh -c 'echo word \>\>
> shortrockyou; rm word'***

**Q.3:** Which flag to use to specify max number of arguments in one
line.

> ***Answer: -n***

**Q.4:** How will you escape command line flags to positional arguments?

> ***Answer: ---***

### Task 9: There's always a special mention... Isn't it? {#84ae .graf .graf--h3 .graf-after--blockquote name="84ae"}

This task is going to be a quick introduction to 2 very awesome
commands: `uniq`{.markup--code .markup--p-code} and `sort`{.markup--code
.markup--p-code}.

uniq command

- [Unique command filters the output (from either a file or stdin) to
  remove any duplicates. Thus we get all unique lines and shorter output
  to focus on. This command greatly reduces stress on searching through
  file with repeated line outputs.]{#51b8}
- [There is one catch though, uniq command, ONLY, identifies the
  duplicate lines, if they are adjacent to each other. So you know why
  do we need a command to `sort`{.markup--code .markup--li-code} lines
  first.]{#9af4}

sort command

- [sort command, as the name suggests sorts the lines alphabetically and
  numerically, automatically. All you got to do is pipe the stdin into
  sort command.]{#62ee}

<figure id="c9c4" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*2xthcz3XmBlqH4DL.png"
class="graf-image" data-image-id="0*2xthcz3XmBlqH4DL.png"
data-width="428" data-height="295" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

**Important Flags for uniq**

<figure id="3cc6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*J5c4Q1O5t0yzufkD.png"
class="graf-image" data-image-id="0*J5c4Q1O5t0yzufkD.png"
data-width="875" data-height="239" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

**Important Flags for sort**

<figure id="6616" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uatv6PstxNf-Dfmh.png"
class="graf-image" data-image-id="0*uatv6PstxNf-Dfmh.png"
data-width="875" data-height="205" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

And this is it for these 2 short commands. Now, if you want to remove
any duplicate lines, a power combo would be `sort`{.markup--code
.markup--p-code} the lines and then use `uniq`{.markup--code
.markup--p-code} on the output.

`sort file.txt | uniq`{.markup--code .markup--p-code}

**Q.1**: Download the file given for this task, find the uniq items
after sorting the file. What is the 2271st word in the output.

> ***Answer: lollol***

**Q.2:** What was the index of term 'michele'

> ***Answer: 2550***

### Task 10: cURL or cRAWl {#d2bc .graf .graf--h3 .graf-after--blockquote name="d2bc"}

cURL(stands for crawl URL; It outputs the data of a URLs webpage in a
raw format). Another amazing command to perform activities that you can
do with your browser, in just a terminal way. You can't download cat
pictures from a direct google search and right clicking \> save the
image. But with a little grepping and pattern matching iframes, that can
be possible too. There are a lot of things that you can do with curl,
ranging from getting an offline copy of a webpage(grepping the sensitive
information later), to download V. large files or activating
webshells(for a reverse connection) just by curl-ing the URL.

curl is a very easy command to use once you get hold of it's flags, rest
is just self-explanatory.

Syntax: `curl `{.markup--code .markup--p-code .u-paddingRight0
.u-marginRight0}[`https://google.com/`{.markup--code .markup--p-code
.u-paddingRight0 .u-marginRight0}](https://google.com/){.markup--anchor
.markup--p-anchor data-href="https://google.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

**Important Flags**

<figure id="cb2a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*emilCoAtoxWCevr_.png"
class="graf-image" data-image-id="0*emilCoAtoxWCevr_.png"
data-width="875" data-height="587" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Examples

- [Continuing a download]{#f2f3}

<figure id="ddc9" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*jXCfECLdPUPnBi8N.png"
class="graf-image" data-image-id="0*jXCfECLdPUPnBi8N.png"
data-width="875" data-height="168" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

You can see that I continued the download by setting the --- continue-at
\<offset\> to a --- (hyphen; which is to continue download by
automatically identifying the offset)

- [Saving the file with the name it was saved on the server.]{#5365}

<figure id="798d" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZktAfq0aC-kPm1IP.png"
class="graf-image" data-image-id="0*ZktAfq0aC-kPm1IP.png"
data-width="807" data-height="128" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Yea my internet \*\*\*\*\*. That speed is in bytes.

**Last notes**

- [Above shown table is just a list of v. few flags that can be used
  with curl. I encourage you to read the man-page on
  [curl](https://curl.se/docs/manpage.html){.markup--anchor
  .markup--li-anchor data-href="https://curl.se/docs/manpage.html"
  rel="noopener ugc nofollow noopener" target="_blank"}
  yourself.]{#00f0}
- [curl doesn't only work on HTTP/HTTPS/FTP protocol it works on Telnet,
  POP, IMAP and a lot more. You can find a complete list of protocols on
  it's man page or
  [here](https://gist.github.com/belikeParamjot/9698ccdcb6a5d1e93e0c39312d42c95e){.markup--anchor
  .markup--li-anchor
  data-href="https://gist.github.com/belikeParamjot/9698ccdcb6a5d1e93e0c39312d42c95e"
  rel="noopener ugc nofollow noopener" target="_blank"}.]{#272f}
- [Just a sidenote: You can use curl as an alternative to wget, while
  transferring privesc scripts from attack box to the host
  system.]{#5c22}

**Resources**

- [[curl command in Linux with
  Examples --- GeeksforGeeks](https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#4412}
- [[curl --- How To
  Use](https://curl.se/docs/manpage.html){.markup--anchor
  .markup--li-anchor data-href="https://curl.se/docs/manpage.html"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#e1d8}
- [[15 Tips On How to Use 'Curl' Command in Linux
  (tecmint.com)](https://www.tecmint.com/linux-curl-command-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.tecmint.com/linux-curl-command-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#e1d7}

**Q.1:** Which flag allows you to limit the download/upload rate of a
file?

> ***Answer: --- limit-rate***

**Q.2:** How will you curl the webpage of
[https://tryhackme.com/](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"} specifying
user-agent as 'juzztesting'

> ***Answer: curl -A 'juzztesting'***
> [***https://tryhackme.com/***](https://tryhackme.com/){.markup--anchor
> .markup--blockquote-anchor data-href="https://tryhackme.com/"
> rel="noopener ugc nofollow noopener" target="_blank"}

**Q.3:** Can curl perform upload operations?(Yea/Nah)

> ***Answer: yea***

### Task 11: WebGoat or webGet {#b6de .graf .graf--h3 .graf-after--blockquote name="b6de"}

You definitely have known the command line way of downloading stuff with
wget command, and thus this is gonna be a quick guide to that tool.

Syntax: `wget protocol://url.com/`{.markup--code .markup--p-code}

**Important Flags**

<figure id="a965" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ei-OOFNmyc_wyj4W.png"
class="graf-image" data-image-id="0*Ei-OOFNmyc_wyj4W.png"
data-width="875" data-height="628" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Note: wget supports ftp, http and https. There are a lot more flags than
the current list, check out the [man
page](https://www.gnu.org/software/wget/manual/wget.html){.markup--anchor
.markup--p-anchor
data-href="https://www.gnu.org/software/wget/manual/wget.html"
rel="noopener ugc nofollow noopener" target="_blank"} online to read
more about it.

Examples

- [Downloading a file with different name]{#b631}

<figure id="6529" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZoVn5_qznxgs-clR.png"
class="graf-image" data-image-id="0*ZoVn5_qznxgs-clR.png"
data-width="875" data-height="163" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

- [Specifying logfile as log.txt with timestamping enabled]{#b44e}

<figure id="f4e0" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*y9apkXTC0ZGyD9IE.png"
class="graf-image" data-image-id="0*y9apkXTC0ZGyD9IE.png"
data-width="875" data-height="329" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

**Q.1:** How will you enable time logging at every new activity that
this tool initiates?

> ***Answer: -N***

**Q.2:** What command will you use to download
[https://xyz.com/mypackage.zip](https://xyz.com/mypackage.zip){.markup--anchor
.markup--p-anchor data-href="https://xyz.com/mypackage.zip"
rel="noopener ugc nofollow noopener" target="_blank"} using wget,
appending logs to an existing file named "package-logs.txt"

> ***Answer: wget -a package-logs.txt***
> [***https://xyz.com/mypackage.zip***](https://xyz.com/mypackage.zip){.markup--anchor
> .markup--blockquote-anchor data-href="https://xyz.com/mypackage.zip"
> rel="noopener ugc nofollow noopener" target="_blank"}

**Q.3:** Write the command to read URLs from "file.txt" and limit the
download speed to 1mbps.

> ***Answer: wget -i file.txt --- limit-rate=1m***

### Task 12: ROFL {#dfaa .graf .graf--h3 .graf-after--blockquote name="dfaa"}

Indeed it is, XXD(if you remove the first X, or a 4 eye rofl won't be
scary at all) nvm, let's start with a lovely command, which is well
known for hexdumps or even the reverse. This command is not very vast to
explore, but still knowing this command thoroughly will help you
handling hex strings and hex digits. Whetheryou're playing ctfs, or
bypassing JWT with automation, xxd can do it all. This command can take
input from a file or the input can be passed through piping or
redirection.

**Important Flags**

<figure id="bda9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*a0fT5AKc-lCyq9eM.png"
class="graf-image" data-image-id="0*a0fT5AKc-lCyq9eM.png"
data-width="875" data-height="476" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

- [Just in case if you been wondering -g flag sets the number of bytes
  in one column of a row and -c flags sets the number of bytes in one
  row. Now, if -g is set to 10 but -c is set to 9(means bytes specified
  in one row is less than the size of a group), then there will only be
  one column and the group size will fall back to the limit specified by
  the column bytes. -c flag precedes over -g.]{#ecbd}

Examples

- [Use of -E flag (For curious minds)]{#e0bc}

<figure id="3e5b" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*qKdvgzAZxFTe0B1w.png"
class="graf-image" data-image-id="0*qKdvgzAZxFTe0B1w.png"
data-width="688" data-height="157" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Also, just so you know EBCDIC is Extended Binary Coded Decimal
Interchange.

- [Output in binary and C include format]{#f1af}

<figure id="f7fc" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*A9FVXhERX8aKWK_3.png"
class="graf-image" data-image-id="0*A9FVXhERX8aKWK_3.png"
data-width="742" data-height="208" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

- [Specifying a length]{#5743}

<figure id="6471" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*EOeSEmea1jmZmfcv.png"
class="graf-image" data-image-id="0*EOeSEmea1jmZmfcv.png"
data-width="640" data-height="75" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Note that, rest of the words got discarded as the length was only 12
bytes(which included space at the end #0x20)

- [Seeking an offset]{#bcbc}

<figure id="afd0" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*GUZjUXyVcfuJ8_J7.png"
class="graf-image" data-image-id="0*GUZjUXyVcfuJ8_J7.png"
data-width="686" data-height="270" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Notice that the output seeked at the 0x10th(16th) byte and started
dumping the file.

- [Seeking at offset from the end of the file.]{#c00a}

<figure id="63e9" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ip-_6xnzuvDoGidp.png"
class="graf-image" data-image-id="0*Ip-_6xnzuvDoGidp.png"
data-width="683" data-height="83" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

Just by appending the offset's value with a hyphen the command starts
dumping from the end of the file.

Sidenote: There is a difference between `-s +offset`{.markup--code
.markup--p-code} and `-s offset`{.markup--code .markup--p-code} while
seeking through stdin. I am not gonna go in brief explaining the
difference just keep in mind that if there is error while seeking offset
through stdin, try redirecting stdin to a file and then perform hexdump
with xxd that might solve your problem.

**Q.1:** How will you seek at 10th byte(in hex) in file.txt and display
only 50 bytes?

> ***Answer: xxd -s 0xa -l 50 -b file.txt***

**Q.2:** How to display a n bytes of hexdump in 3 columns with a group
of 3 octets per row from file.txt? (Use flags alphabetically)

> ***Answer: xxd -c 9 -g 3 file.txt***

**Q.3:** Which has more precedence over the other -c flag or -g flag?

> ***Answer: -c***

**Q.4:** Download the file and find the value of flag.

<figure id="ce50" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VVtstRM9tQEXBgJy.png"
class="graf-image" data-image-id="0*VVtstRM9tQEXBgJy.png"
data-width="875" data-height="98" />
</figure>

### Task 13: The Last of Us {#3b1b .graf .graf--h3 .graf-after--figure name="3b1b"}

Let's start with the commands I found after doing a
`| sort | uniq`{.markup--code .markup--p-code} search on the first word
on every line in my \~/.bash_history(31337 commands got listed. This
task won\'t include nmap/gobuster commands, because that\'s not what
this room is about).

<figure id="b119" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SoEu0yxBZ2Vgn2Vs.png"
class="graf-image" data-image-id="0*SoEu0yxBZ2Vgn2Vs.png"
data-width="710" data-height="91" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

In case you're wondering, how I got custom .bash_history size, I edited
my .bashrc file in home directory

### gpg command {#c47e .graf .graf--h3 .graf-after--p name="c47e"}

*Sidenote: GPG(Gnu Privacy Guard) and PGP(Pretty Good Privacy) are 2
different types of encryption. PGP is based on RSA encryption, whereas
GPG(open-source) is a re-write of PGP and by default uses AES
encryption.*

- [You should be knowing about PGP and GPG keys when you find a file
  encrypted with GPG encryption. Thus below are some resources to easily
  know more about gpg: the command line tool.]{#1ecd}

Resources

- [[gpg --- Unix, Linux
  Command --- Tutorialspoint](https://www.tutorialspoint.com/unix_commands/gpg.htm){.markup--anchor
  .markup--li-anchor
  data-href="https://www.tutorialspoint.com/unix_commands/gpg.htm"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#8c26}
- [[GPG Cheat Sheet
  (hawaii.edu)](http://irtfweb.ifa.hawaii.edu/~lockhart/gpg/){.markup--anchor
  .markup--li-anchor
  data-href="http://irtfweb.ifa.hawaii.edu/~lockhart/gpg/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#bb76}

### tar command {#7157 .graf .graf--h3 .graf-after--li name="7157"}

- [Whether if it is a gzip archive or a bzip archive, encrypting and
  decrypting can be easily done by this tool. Do check out the man page
  for tar `man tar`{.markup--code .markup--li-code}.]{#b55e}

Resources:

- [[Linux Tar Commands Cheatsheet \| Never Ending Security
  (wordpress.com)](https://neverendingsecurity.wordpress.com/2015/04/13/linux-tar-commands-cheatsheet/){.markup--anchor
  .markup--li-anchor
  data-href="https://neverendingsecurity.wordpress.com/2015/04/13/linux-tar-commands-cheatsheet/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#f49e}
- [[tar command in Linux with
  examples --- GeeksforGeeks](https://www.geeksforgeeks.org/tar-command-linux-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/tar-command-linux-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#1dbd}

### id/pwd/uname commands {#c1d0 .graf .graf--h3 .graf-after--li name="c1d0"}

- [Let's not forget the legends that we deploy on the battlefield after
  getting init shell access on a machine.]{#3c83}

### ps/kill commands {#6bd3 .graf .graf--h3 .graf-after--li name="6bd3"}

- [List processes, and kill processes with PID. To know more about ps
  command you can find some help
  [here](https://man7.org/linux/man-pages/man1/ps.1.html){.markup--anchor
  .markup--li-anchor
  data-href="https://man7.org/linux/man-pages/man1/ps.1.html"
  rel="noopener ugc nofollow noopener" target="_blank"}.]{#c053}

### netstat command {#c544 .graf .graf--h3 .graf-after--li name="c544"}

- [This amazing command lists any network activity on the current
  system. Any ports that are open/listening/not-established, connection
  can be listed using this command.]{#4e49}
- [Make sure to check out this command's man page and read more about
  this.]{#7b8c}
- [Also know this, that there is an alternate to netstat command which
  does the pretty much same as netstat, i.e. `ss`{.markup--code
  .markup--li-code} (socket statistics) command(lists port activity in
  real time).]{#e567}

Resources

- [[Ultimate Netstat Cheat Sheet --- Master Netstat in 20 Minutes
  (rekha.com)](https://www.rekha.com/netstat-cheat-sheet-for-newbies.html){.markup--anchor
  .markup--li-anchor
  data-href="https://www.rekha.com/netstat-cheat-sheet-for-newbies.html"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#ad64}
- [[netstat(8) --- Linux man page
  (die.net)](https://linux.die.net/man/8/netstat){.markup--anchor
  .markup--li-anchor data-href="https://linux.die.net/man/8/netstat"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#b47f}
- [[SS --- Socket Statistics Commands Cheatsheet \| Never Ending
  Security
  (wordpress.com)](https://neverendingsecurity.wordpress.com/2015/04/13/ss-socket-statistics-commands-cheatsheet/){.markup--anchor
  .markup--li-anchor
  data-href="https://neverendingsecurity.wordpress.com/2015/04/13/ss-socket-statistics-commands-cheatsheet/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#1cf2}

### less/more commands {#6d7e .graf .graf--h3 .graf-after--li name="6d7e"}

- [These are another 2 awesome commands that offer an alternate to open
  and read the file. What's the difference? more is an old command and
  less was built to better the more command. More on one hand has
  limited backward scrolling, whereas as less has forward and backward
  navigation including better search options (/).]{#0c86}
- [Again, more is lovely in it's own way, I remember I got shell while
  doing a box from [vulnhub](https://vulnhub.com/){.markup--anchor
  .markup--li-anchor data-href="https://vulnhub.com/"
  rel="noopener ugc nofollow noopener" target="_blank"} using more
  command (that ssh shell was keep exiting after a successful login, I
  piped the session in more command and got shell through !/bin/sh. That
  challenge was something like, reduce your term size to only one line
  and open the ssh session piping into more command and then
  run !/bin/sh in more's command pallete, which I can't seem to
  re-create now). Sadly, I don't remember the box anymore. *If you
  remember the box somehow, reach out to me please.*]{#d959}
- [There is one more command which was created to improve some of
  `less`{.markup--code .markup--li-code} features, most command; It is
  not installed by default on some linux distros, you can install it
  with `sudo apt install most`{.markup--code .markup--li-code}.]{#e260}

Resources

- [[The Difference Between more, less And most
  Commands --- OSTechNix](https://ostechnix.com/the-difference-between-more-less-and-most-commands/){.markup--anchor
  .markup--li-anchor
  data-href="https://ostechnix.com/the-difference-between-more-less-and-most-commands/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#72b4}
- [[Less and More command
  (Explained)](https://www.tecmint.com/linux-more-command-and-less-command-examples/#:~:text=Learn%20Linux%20%27less%27%20Command,using%20page%20up%2Fdown%20keys.){.markup--anchor
  .markup--li-anchor
  data-href="https://www.tecmint.com/linux-more-command-and-less-command-examples/#:~:text=Learn%20Linux%20%27less%27%20Command,using%20page%20up%2Fdown%20keys."
  rel="noopener ugc nofollow noopener" target="_blank"}]{#0061}

### diff command {#dc42 .graf .graf--h3 .graf-after--li name="dc42"}

- [At the very basic of it's use, this command compares the character
  byte-by-byte and tries to find what is the difference between 2 files.
  Though this can ONLY compare 2 files at a time. Wanna learn more about
  this command, checkout resources.]{#8d25}
- [There is also another command known as comm. This command compares 2
  sorted files line by line. As diff tries to find any difference
  between the files, comm is more focused to find out what is common in
  between 2 files. Checkout resources to learn more.]{#628e}

Resources

- [[Comparing files and directories with the diff and comm Linux
  commands \| Network
  World](https://www.networkworld.com/article/3279724/comparing-files-and-directories-with-diff-and-comm.html#:~:text=The%20diff%20command%20would%20make,both%20commands%20is%20the%20same.&text=The%20comm%20command%20can%20provide,it%20can%20compare%20two%20files.){.markup--anchor
  .markup--li-anchor
  data-href="https://www.networkworld.com/article/3279724/comparing-files-and-directories-with-diff-and-comm.html#:~:text=The%20diff%20command%20would%20make,both%20commands%20is%20the%20same.&text=The%20comm%20command%20can%20provide,it%20can%20compare%20two%20files."
  rel="noopener ugc nofollow noopener" target="_blank"}]{#83a5}
- [[diff command in Linux with
  examples --- GeeksforGeeks](https://www.geeksforgeeks.org/diff-command-linux-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/diff-command-linux-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#6ee1}
- [[comm command in Linux with
  examples --- GeeksforGeeks](https://www.geeksforgeeks.org/comm-command-in-linux-with-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/comm-command-in-linux-with-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#ed82}

### base64 command {#c12a .graf .graf--h3 .graf-after--li name="c12a"}

<figure id="423e" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*uJoh70AYJs133rbm.png"
class="graf-image" data-image-id="0*uJoh70AYJs133rbm.png"
data-width="351" data-height="75" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

- [Why go to online sites when you can decode base32 and base64 at your
  own terminal.]{#13f4}

### tee command {#d395 .graf .graf--h3 .graf-after--li name="d395"}

- [Ever wondered, that you want to view the output in real-time and save
  the output in a file at the same time? Well standard redirection
  doesn't allow that. No worries, tee command is to the rescue. It reads
  from stdin and writes to the stdout and files as well.]{#7277}
- [A small handy tool that I use every time with linpeas to read my
  script results in real time and also saving the output at the
  machine's /tmp directory.]{#57a8}

<figure id="356f" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*BIAxT-mzL40o2-ue.png"
class="graf-image" data-image-id="0*BIAxT-mzL40o2-ue.png"
data-width="536" data-height="96" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

- [You can use it with -a flag to don't overwrite an existing file
  instead just append some more.]{#28c1}

### file/stat commands {#1fcb .graf .graf--h3 .graf-after--li name="1fcb"}

- [File command reads the file headers and tells you what the file
  actually is(inspite of what extension is used). Similarly is stat
  command, which gives you a file's/file system's status.]{#8a25}

<figure id="0944" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*uZrrlQreqKdUa6FQ.png"
class="graf-image" data-image-id="0*uZrrlQreqKdUa6FQ.png"
data-width="768" data-height="247" />
</figure>

[https://tryhackme.com/room/linuxmodules](https://tryhackme.com/room/linuxmodules){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxmodules"
rel="noopener ugc nofollow noopener" target="_blank"}

### export command {#03bc .graf .graf--h3 .graf-after--p name="03bc"}

- [This command is used to set the environment variables(The variables
  that got set whenever a shell/user session is opened). You can read
  more about this command through
  [here](https://www.geeksforgeeks.org/export-command-in-linux-with-examples/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.geeksforgeeks.org/export-command-in-linux-with-examples/"
  rel="noopener ugc nofollow noopener" target="_blank"}.]{#93a1}

### reset command {#0b77 .graf .graf--h3 .graf-after--li name="0b77"}

- [Say if your terminal is not working properly, any problem is
  occurring, but you can't afford to close the shell, you're just one
  `reset`{.markup--code .markup--li-code} command away to get your shell
  back to normal.]{#8570}

### systemctl/service command {#219f .graf .graf--h3 .graf-after--li name="219f"}

- [`service`{.markup--code .markup--li-code} command is a normal command
  to initialize services present in /etc/init.d, without making an admin
  worrying too much about the permanent system changes,
  `systemctl`{.markup--code .markup--li-code} on the other hand is a
  heavy command(doing pretty much the same job, just on systemd\'s
  level; systemd is a service manager in linux systems) which can hinder
  with the default settings. For eg. services initialized by systemctl
  stays in systemd\'s directory (directory which holds what program to
  run when a linux system boots up). Thus the programs initialized by
  systemctl boots up with system.]{#ccfe}
- [With `service`{.markup--code .markup--li-code} you can only use
  commands related to that particular service (reload, start, stop,
  status etc), and with a powerful tool like `systemctl`{.markup--code
  .markup--li-code}, you get to control the state of \"systemd\" system
  and service manager.]{#634d}

Note: If you don't know what you're doing, try using
`service`{.markup--code .markup--p-code} instead, to avoid any unwanted
service to stop/disable/masked, which might not fix even on a fresh boot
up. Backing up your important files has always been a good habit.

References

- [[Difference between Systemctl and service command --- Stack
  Overflow](https://stackoverflow.com/questions/43537851/difference-between-systemctl-and-service-command#:~:text=service%20operates%20on%20the%20files,file%20in%20%2Fetc%2Finit.){.markup--anchor
  .markup--li-anchor
  data-href="https://stackoverflow.com/questions/43537851/difference-between-systemctl-and-service-command#:~:text=service%20operates%20on%20the%20files,file%20in%20%2Fetc%2Finit."
  rel="noopener ugc nofollow noopener" target="_blank"}]{#1078}
- [[Systemctl Cheatsheet
  (github.com)](https://gist.github.com/adriacidre/307d2f9f5179fc748f22edac5af3d218){.markup--anchor
  .markup--li-anchor
  data-href="https://gist.github.com/adriacidre/307d2f9f5179fc748f22edac5af3d218"
  rel="noopener ugc nofollow noopener" target="_blank"} (A small
  cheatsheet you wanna read before working with systemctl).]{#787d}

Read the last learning task.

**Q.1:** It's safe to run systemctl command and experiment on your main
linux system neither following a proper guide or having any prior
knowledge? (Right/Wrong)

> ***Answer: wrong***

**Q.2:** resetHow will you import a given PGP private key. (Suppose the
name of the file is key.gpg)

> ***Answer: gpg --- import key.gpg***

**Q.3:** How will you list all port activity if netstat is not available
on a machine? (Full Name)

> ***Answer: Socket Statistics***

**Q.4:** What command can be used to fix a broken/irregular/weird acting
terminal shell?

> ***Answer: reset***

**Q.5:** Press F to pay respect

> ***Answer: F***

### Promote and Collaborate on Cybersecurity Insights {#813d .graf .graf--h3 .graf-after--blockquote name="813d"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#6da5 .graf .graf--h3 .graf-after--p name="6da5"}

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
.h-card} on [August 21, 2024](https://medium.com/p/4f07b9e8561d).

[Canonical
link](https://medium.com/@bevijaygupta/linux-modules-tryhackme-writeup-4f07b9e8561d){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
