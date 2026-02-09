::: {}
# Linux Strength Training Tryhackme Writeup {#linux-strength-training-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/linuxstrengthtraining
:::

::::::: {.section .e-content field="body"}
:::::: {#2572 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux Strength Training Tryhackme Writeup {#8d06 .graf .graf--h3 .graf--leading .graf--title name="8d06"}

<figure id="9be8" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*IdNdA8zeHPfdum3M.png"
class="graf-image" data-image-id="0*IdNdA8zeHPfdum3M.png"
data-width="513" data-height="233" data-is-featured="true" />
</figure>

[https://tryhackme.com/room/linuxstrengthtraining](https://tryhackme.com/room/linuxstrengthtraining){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/linuxstrengthtraining"
rel="noopener ugc nofollow noopener" target="_blank"}

**Room link:**
[https://tryhackme.com/room/malstrings](https://tryhackme.com/room/malstrings){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malstrings"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Task 2: Finding your way around linux --- overview {#79b7 .graf .graf--h3 .graf-after--p name="79b7"}

As a security researcher you will often be required to find specific
files/folders on a system based on various conditions ranging from, but
not limited to the following:

- [**filename**]{#a16c}
- [**size**]{#a5a3}
- [**user/group**]{#6993}
- [**date modified**]{#691a}
- [**date accessed**]{#db68}
- [**Its keyword contents**]{#4d3f}

Therefore, we can do this using the following syntax:-

### Find files based on filename {#25f3 .graf .graf--h3 .graf-after--p name="25f3"}

find \[directory path\] -type f -name \[filename\]

``` {#8444 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
find /home/Andy -type f -name sales.txt
```

### Find Directory based on directory name {#7608 .graf .graf--h3 .graf-after--pre name="7608"}

find \[directory path\] -type d -name \[filename\]

``` {#74a3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
find /home/Andy -type d -name pictures
```

### Find files based on size {#f86f .graf .graf--h3 .graf-after--pre name="f86f"}

find \[directory path\] -type f -size \[size\]

``` {#4752 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
find /home/Andy -type f -size 10c(c for bytes,
k for kilobytes
M megabytes
G for gigabytes
type:'man find' for full information on the  options)
```

### Find files based on username {#c42c .graf .graf--h3 .graf-after--pre name="c42c"}

find \[directory path\] -type f -user \[username\]

``` {#2ef9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
find /etc/server -type f -user john
```

### Find files based on group name {#61ac .graf .graf--h3 .graf-after--pre name="61ac"}

find \[directory path\] -type f -group \[group name\]

``` {#b4ba .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
find /etc/server -type f -group teamstar
```

### Find files modified after a specific date {#a0c2 .graf .graf--h3 .graf-after--pre name="a0c2"}

find \[directory path\] -type f -newermt '\[date and time\]'

``` {#2172 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
find / -type f -newermt '6/30/2020 0:00:00'(all dates/times after 6/30/2020 0:00:00 will be considered a condition to look for)
```

### Find files based on date modified {#176a .graf .graf--h3 .graf-after--pre name="176a"}

find \[directory path\] -type f -newermt \[start date range\] ! -newermt
\[end date range\]

``` {#f1c4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
find / -type f -newermt 2013-09-12 ! -newermt 2013-09-14(all  dates before 2013-09-12 will be excluded; all dates after 2013-09-14  will be excluded, therefore this only leaves 2013-09-13 as the date to  look for.)
```

### Find files based on date accessed {#5101 .graf .graf--h3 .graf-after--pre name="5101"}

find \[directory path\] -type f -newerat \[start date range\] ! -newerat
\[end date range\]

``` {#1847 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
find / -type f -newerat 2017-09-12 ! -newerat 2017-09-14(all dates before 2017-09-12 will be excluded; all dates after  2017-09-14 will be excluded, therefore this only leaves 2017-09-13 as  the date to look for.)
```

### Find files with a specific keyword {#915c .graf .graf--h3 .graf-after--pre name="915c"}

grep -iRl \[directory path/keyword\]

``` {#ca2d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
grep -iRl '/folderA/flag'
```

### read the manual for the find command {#8735 .graf .graf--h3 .graf-after--pre name="8735"}

man find

``` {#7025 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
man find
```

**Note:** There are many more useful commands aside from the examples
above. If you ever have trouble understanding any of the syntax or
getting it to work, head on over to
[explainshell.com](http://explainshell.com/){.markup--anchor
.markup--p-anchor data-href="http://explainshell.com/"
rel="noopener ugc nofollow noopener" target="_blank"} to check the
syntax and see how this tool can help you on your journey to Linux
greatness.

**Further notes:** if you do not know already, typing CTRL+L allows you
to clear the screen quicker rather than typing 'clear' all the time.
Additionally, hitting the up arrow allows you to return to a previously
typed command so you do not have to spend time retyping it again if you
made an error. Cool. Finally, placing: **2\>/dev/null** at the end of
your find command can help filter your results to exclude
files/directories that you do not have permission to.

**Question 1**. What is the correct option for finding files based on
group

> ***Answer: -group***

**Question 2.** What is format for finding a file with the user named
Francis and with a size of 52 kilobytes in the directory /home/francis/

> ***Answer: find /home/francis -type f -user francis -size 52k***

**Question 3**. SSH as **topson** using his password **topson**. Go to
the /home/topson/chatlogs directory and type the following: grep -iRl
'keyword'. What is the name of the file that you found using this
command?

ssh topson@\[Delpoyed Machine IP\] then enter the password "topson" when
the terminal asks for it.

``` {#b300 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh topson@10.10.31.202
```

I use the command\
cd /home/topson/chatlogs to enter the chatlogs directory. Finally I use
the grep-iRl 'keyword' to find the file

<figure id="05e6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0GYkonrHvaVZ2D1p.png"
class="graf-image" data-image-id="0*0GYkonrHvaVZ2D1p.png"
data-width="483" data-height="113" />
</figure>

> ***Answer: 2019--10--11***

Type: less \[filename\] to open the file. Then, before anything, type /
before typing: keyword followed by \[ENTER\]. Notice how that allowed us
to search for the first instance of that word in the entire document.
For much larger documents this can be useful and if there are many more
instances of that word in the document, we would be able to hit enter
again to find the next instance in the document.

``` {#d91e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
less 2019–10–11
```

Then type: `/`{.markup--code .markup--p-code} then
`keyword`{.markup--code .markup--p-code} then **Enter**

<figure id="d327" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*y5GvqOTLMdgN4bTw.png"
class="graf-image" data-image-id="0*y5GvqOTLMdgN4bTw.png"
data-width="205" data-height="97" />
</figure>

<figure id="75fb" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*M0G1mRx8j1LT5H4R.png"
class="graf-image" data-image-id="0*M0G1mRx8j1LT5H4R.png"
data-width="373" data-height="151" />
</figure>

Press **Q** to exit the `less`{.markup--code .markup--p-code} command.

**Question 4**. What are the characters subsequent to the word you
found?

> ***Answer: ttitor***

**Question 5**. Read the file named 'ReadMeIfStuck.txt'. What is the
Flag?

I start of by trying to find the ReadMeIfStuck.txt file. I do that with
the command

<figure id="3312" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EJGb5JbR1S2S2E_W.png"
class="graf-image" data-image-id="0*EJGb5JbR1S2S2E_W.png"
data-width="875" data-height="122" />
</figure>

**find / -type f -name additionalHINT 2\>/dev/null**

``` {#099b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
/ tells the tool to look inside all folders that's inside that path. /  is the highest path possible on Linux, so in this case I search through  the hole file system.  -type f tells the tool to only look for files  -name additionalHINT tells the tool to only look for that string.  Since I don't have access to all folders on the system I will also get  alot of errors when the find tool tries to traverse into them.  2>/dev/null tells the tool to throw away these messages.
```

<figure id="e16a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*x0_cDbCIMRX2OIdI.png"
class="graf-image" data-image-id="0*x0_cDbCIMRX2OIdI.png"
data-width="875" data-height="149" />
</figure>

This time they want us to find a directory with space. I simply do this
with the following command

**find / -type d -name telephone\\ numbers 2\>/dev/null**

``` {#4350 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
I use the \ which is an escape character, the escape character lets us  search for a character that otherwise have a special use. In this case  it's " ".
```

<figure id="36b3" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Qj8-hfWMYoV-dlu-.png"
class="graf-image" data-image-id="0*Qj8-hfWMYoV-dlu-.png"
data-width="875" data-height="326" />
</figure>

Step one find out where the /workflows directory hides so I can use it
to find the file. I do the same as before with the command

**find / -type d -name workflows 2\>/dev/null**

<figure id="0e7a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Sg7uyYHpxj6RDB-G.png"
class="graf-image" data-image-id="0*Sg7uyYHpxj6RDB-G.png"
data-width="622" data-height="94" />
</figure>

Great, I know where the directory is located, but to find this file I
will have to change up my command abit. I no longer have a name of the
file, but a date. I use the command

**find /home/topson/workflows -type f -newermt 2016--09--11 ! -newermt
2016--09--13**

<figure id="7319" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bPNETg_R3nmb6gmI.png"
class="graf-image" data-image-id="0*bPNETg_R3nmb6gmI.png"
data-width="875" data-height="105" />
</figure>

``` {#54d1 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
less /home/topson/workflows/xft/eBQRhHvx
```

Type: `/`{.markup--code .markup--p-code} then `Flag`{.markup--code
.markup--p-code} then **Enter** . Use **Pg Dn** until you see the
highlighted pattern

<figure id="ca60" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xFsSax4kPuWPoCzx.png"
class="graf-image" data-image-id="0*xFsSax4kPuWPoCzx.png"
data-width="875" data-height="186" />
</figure>

### Task 3: Working with files {#a36e .graf .graf--h3 .graf-after--figure name="a36e"}

**Question 1**. Hypothetically, you find yourself in a directory with
many files and want to move all these files to the directory of
/home/francis/logs. What is the correct command to do this?

> ***Answer: mv \* /home/francis/logs***

**Question 2.** Hypothetically, you want to transfer a file from your
/home/james/Desktop/ with the name script.py to the remote machine
(192.168.10.5) directory of /home/john/scripts using the username of
john. What would be the full command to do this?

> ***Answer: scp /home/james/Desktop/script.py
> john@192.168.10.5:/home/john/scripts***

**Question 3**. How would you rename a folder named -logs to -newlogs

> ***Answer: mv --- -logs -newlogs***

**Question 4.** How would you copy the file named encryption keys to the
directory of /home/john/logs

> ***Answer: cp "encryption keys" /home/john/logs***

**Question 5.** Find a file named readME_hint.txt inside topson's
directory and read it. Using the instructions it gives you, get the
second flag.

First off I use **find / -type f -name readME_hint.txt 2\>/dev/null**

to find the file. Then I read it with cat

<figure id="4a76" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kOBtuozStZ5cUYdN.png"
class="graf-image" data-image-id="0*kOBtuozStZ5cUYdN.png"
data-width="875" data-height="289" />
</figure>

I need to move the "MoveMe.txt" into the "march" folder and then execute
a sh program to get the flag. I find the folder by

**find / -type d -name \*march\* 2\>/dev/null**

the two \* on the side matches any characters. I use

``` {#5724 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
find / -type f -name *MoveMe.txt* 2>/dev/nullmv -- /home/topson/corperateFiles/RecordsFinances/-MoveMe.txt /home/topson/corperateFiles/RecordsFinances/-march\ folder/cd -- /home/topson/corperateFiles/RecordsFinances/-march\ folder/
```

<figure id="4f1d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*HoEcXeKK688aPUuH.png"
class="graf-image" data-image-id="0*HoEcXeKK688aPUuH.png"
data-width="875" data-height="286" />
</figure>

### Task 4: Hashing --- introduction {#e10a .graf .graf--h3 .graf-after--figure name="e10a"}

**What is hashing?**

Next we will talk about hashing, which is important for any Linux
security researcher. Hashing refers to taking any data input, such as a
password and calculating its hash equivalent. The hash equivalent is a
long string which cannot be reversed since the act of hashing is known
as a one-way function. For example, if you visit:
[https://www.md5hashgenerator.com/](https://www.md5hashgenerator.com/){.markup--anchor
.markup--p-anchor data-href="https://www.md5hashgenerator.com/"
rel="noopener ugc nofollow noopener" target="_blank"} and type the
following: mypassword123 or any other password, you will see how the
hash algorithm known as MD5 will calculate and output a MD5 hash
equivalent. Therefore, 'mypassword123' would have the MD5 hash
equivalent of '**9c87baa223f464954940f859bcf2e233'.**

<figure id="5837" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZZTMqFH6k_hnvXvw.png"
class="graf-image" data-image-id="0*ZZTMqFH6k_hnvXvw.png"
data-width="569" data-height="226" />
</figure>

**Why is hashing important?**

Note: MD5 and SHA1 are both examples of weak hash algorithms which have
been proven to be vulnerable to something known as hash collision
attacks which is explained further here:
[https://privacycanada.net/hash-functions/hash-collision-attack/](https://privacycanada.net/hash-functions/hash-collision-attack/){.markup--anchor
.markup--p-anchor
data-href="https://privacycanada.net/hash-functions/hash-collision-attack/"
rel="noopener ugc nofollow noopener" target="_blank"}. In short, do not
use them because it has been proven that two different inputs can
produce the same output (hash equivalent), thus, meaning that your
password may produce the same hash as someone with a completely
different password. Instead, SHA-256 is widely considered stronger as of
today and is recommended.

**How to crack hashes?**

Hashes can be cracked through the method of brute-forcing. This
essentially means using a wordlist and inputting each potential password
from the wordlist into the hash function to see if we get a hash
equivalent output that is equal to any of the hashes stored in the
database. However, in the example we store the hash in a text file
before specifying a wordlist to which we want to compare out calculated
hashes with.

<figure id="cbd9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PTz8Au2iUy8RraX9.png"
class="graf-image" data-image-id="0*PTz8Au2iUy8RraX9.png"
data-width="512" data-height="161" />
</figure>

Using a program called John the Ripper we can specify the format of the
hash we wish to crack (md5) the wordlist (rockyou.txt) and the wordlist
(hash.txt). Please see the full man page for garnering a more complete
understanding of all of the commands you can run with this program.

<figure id="ee88" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NrDZpfdeBOgQCrgm.png"
class="graf-image" data-image-id="0*NrDZpfdeBOgQCrgm.png"
data-width="603" data-height="33" />
</figure>

Eventually John the Ripper may find the password if it was contained the
wordlist. In the real world, you may have to find a larger wordlist with
a strong amount of common password/username combinations. In this
example below the password was found to be 'password'.

<figure id="2255" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WXc1Es-gr6uMZHhM.png"
class="graf-image" data-image-id="0*WXc1Es-gr6uMZHhM.png"
data-width="372" data-height="114" />
</figure>

Note: If you ever encounter a hash that you do not know the type of you
can use a tool called hash-identifier. However, with less widely used
hashes the tool will not be accurate and therefore will still rely on
you to develop the skill of manually identifying what type of hash it
is, however this is out of the scope of this room. The syntax for
identifying unknown hashes is as so:

Hash-identifier \[hash\] as seen below in a real example:

<figure id="8139" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4ncFonAJESN9_jFG.png"
class="graf-image" data-image-id="0*4ncFonAJESN9_jFG.png"
data-width="608" data-height="33" />
</figure>

Alternatively you could pipe the output of the file storing the hash to
hash-identifier as shown below, which may be quicker.

<figure id="ea6d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3K8AotvncFMvLCEu.png"
class="graf-image" data-image-id="0*3K8AotvncFMvLCEu.png"
data-width="324" data-height="34" />
</figure>

The result should show us the most likely hash types that the hash most
likely is. As you can see there are two most probable hashes. In this
case the correct hash was in fact SHA-256, therefore you can see how in
most cases the first result is the correct answer, but please be aware
that this not always the case since many hash types can appear similar
in terms of string formatting.

<figure id="5147" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2np3QYRYPC6eiGhq.png"
class="graf-image" data-image-id="0*2np3QYRYPC6eiGhq.png"
data-width="674" data-height="375" />
</figure>

**Question 1**. Download the hash file attached to this task and attempt
to crack the MD5 hash. What is the password?

<figure id="f2b1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8uycz5F4dy1dyLWT.png"
class="graf-image" data-image-id="0*8uycz5F4dy1dyLWT.png"
data-width="685" data-height="405" />
</figure>

<figure id="55ad" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*B5EiEQHUeV1Cgwl7.png"
class="graf-image" data-image-id="0*B5EiEQHUeV1Cgwl7.png"
data-width="649" data-height="248" />
</figure>

> ***Answer: secret123***

SSH as **sarah** using: sarah@\[MACHINE:IP\] and use the password:
**rainbowtree1230x**

First of I need to find the file, luckily I am starting to get good at
this. I use

**find / -type f -name hashA.txt 2\>/dev/null** to find the file.

<figure id="889c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_UchqJesqQf166vs.png"
class="graf-image" data-image-id="0*_UchqJesqQf166vs.png"
data-width="875" data-height="173" />
</figure>

**Question 2.** What is the hash type stored in the file hashA.txt

<figure id="497b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MTP7qrj07C8GbJYa.png"
class="graf-image" data-image-id="0*MTP7qrj07C8GbJYa.png"
data-width="875" data-height="322" />
</figure>

> ***Answer: md4***

**Question 3.** Crack hashA.txt using john the ripper, what is the
password?

<figure id="3adc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EolbF3JgbpfxY52A.png"
class="graf-image" data-image-id="0*EolbF3JgbpfxY52A.png"
data-width="601" data-height="241" />
</figure>

> ***Answer: admin***

**Question 4.** What is the hash type stored in the file hashB.txt

<figure id="2524" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uT2jS99yDgJQYmsp.png"
class="graf-image" data-image-id="0*uT2jS99yDgJQYmsp.png"
data-width="661" data-height="126" />
</figure>

<figure id="f2a9" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*BiZdZSxYQwgpsyQT.png"
class="graf-image" data-image-id="0*BiZdZSxYQwgpsyQT.png"
data-width="730" data-height="411" />
</figure>

> ***Answer: SHA-1***

**Question 5.** Find a wordlist with the file extention of '.mnf' and
use it to crack the hash with the filename hashC.txt. What is the
password?

<figure id="d274" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3oWbZg_5LpAC_-Vn.png"
class="graf-image" data-image-id="0*3oWbZg_5LpAC_-Vn.png"
data-width="687" data-height="129" />
</figure>

<figure id="3f18" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qWOeUn0Su6Kk323X.png"
class="graf-image" data-image-id="0*qWOeUn0Su6Kk323X.png"
data-width="866" data-height="404" />
</figure>

Hash type is **SHA-256**

To find the wordlist I use **find / -type f -name \*.mnf 2\>/dev/null**

Sarah's password **rainbowtree1230x**

we need to download the '**ww.mnf**' to use it as word-list with
JohnTheRipper.\
To download the word-list use **scp** command from your computer:

<figure id="a0dc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dduCfxhT_UvBdq1s.png"
class="graf-image" data-image-id="0*dduCfxhT_UvBdq1s.png"
data-width="853" data-height="292" />
</figure>

<figure id="4cd3" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ta_782n9k5ZU9g-c.png"
class="graf-image" data-image-id="0*ta_782n9k5ZU9g-c.png"
data-width="631" data-height="274" />
</figure>

> ***Answer: unacvaolipatnuggi***

**Question 6.** Crack hashB.txt using john the ripper, what is the
password?

<figure id="1567" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*S2QOGO72bNexEwLn.png"
class="graf-image" data-image-id="0*S2QOGO72bNexEwLn.png"
data-width="656" data-height="115" />
</figure>

<figure id="cb04" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*gKVKgGZUcGDZ1D0j.png"
class="graf-image" data-image-id="0*gKVKgGZUcGDZ1D0j.png"
data-width="666" data-height="404" />
</figure>

<figure id="b736" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*aJJbsFd4nfWg9n8W.png"
class="graf-image" data-image-id="0*aJJbsFd4nfWg9n8W.png"
data-width="688" data-height="331" />
</figure>

> ***Answer: letmein***

### Task 5: Decoding base64 {#c787 .graf .graf--h3 .graf-after--blockquote name="c787"}

**What is base64**

Base64 is a group of binary-to-text encoding schemes that represent
binary data in an ASCII string format. In summary, it is just another
way in which data can be represented; some systems rely on a base64
encoding of data for processing while others may not. Head over to:
[https://www.base64encode.net/](https://www.base64encode.net/){.markup--anchor
.markup--p-anchor data-href="https://www.base64encode.net/"
rel="noopener ugc nofollow noopener" target="_blank"} and input any text
and encode it. You should end up with something similiar below:

As you can see, the string 'example' gets coverted to the base64
'ZXhhbXBsZQ==' encoded string. This would allow certain systems to now
be able to read and process the data properly.

<figure id="ed02" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BZlrittmeT4XCbhS.png"
class="graf-image" data-image-id="0*BZlrittmeT4XCbhS.png"
data-width="564" data-height="765" />
</figure>

[https://www.base64encode.net/](https://www.base64encode.net/){.markup--anchor
.markup--p-anchor data-href="https://www.base64encode.net/"
rel="noopener ugc nofollow noopener" target="_blank"}

**Why should I care?**

There may be times when you encounter base64 converted data in files on
a system and needed to convert it to a human readable format. Therefore,
we can use the tool 'base64' with a pipe to translate it back to
something that is human readable.

cat \[filename\] \| base64 -d

<figure id="7c92" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cykEdM8zl6QnQH0K.png"
class="graf-image" data-image-id="0*cykEdM8zl6QnQH0K.png"
data-width="399" data-height="44" />
</figure>

to transfer the output to a new text file simply use he \> operator
followed by the new filename.

<figure id="f6db" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7IKpSqqQ4IehCY1l.png"
class="graf-image" data-image-id="0*7IKpSqqQ4IehCY1l.png"
data-width="505" data-height="29" />
</figure>

Once again, encoding/decoding is changing data format. The data itself
does not change, just how it reads.

I encourage you to spend some time reading about encoding. At least
enough so you understand the difference between encoding/decoding vs
encryption/decryption as beginners sometimes confuse them with each
other.

**Question 1**. what is the name of the tool which allows us to decode
base64 strings?

> ***Answer: base64***

**Question 2.** find a file called encoded.txt. What is the special
answer?

<figure id="67da" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*StISoPllNnN90ctC.png"
class="graf-image" data-image-id="0*StISoPllNnN90ctC.png"
data-width="801" data-height="107" />
</figure>

Now use less command to view file you see instruction to look for
'**special**' keyword in file, type**/special** and \[ENTER\] to move
through file till you '**special**' keyword.

<figure id="2609" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MQBXx_94I-WATYae.png"
class="graf-image" data-image-id="0*MQBXx_94I-WATYae.png"
data-width="875" data-height="96" />
</figure>

Now, find the file '**ent.txt**'. It does not seem to be base64 encoded
string. Use hash-identifier to check hashing algorithm. When check using
hash-identifier you see it is **md4** hash.

<figure id="e04d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*scEe13nHOh9gDqob.png"
class="graf-image" data-image-id="0*scEe13nHOh9gDqob.png"
data-width="645" data-height="135" />
</figure>

Finally, use JohnTheRipper to crack password, use rockyou.txt word-list.

<figure id="19d7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Bt_alVLNu24GZpBL.png"
class="graf-image" data-image-id="0*Bt_alVLNu24GZpBL.png"
data-width="597" data-height="231" />
</figure>

> ***Answer: john***

### Task 6: Encryption/Decryption using gpg {#68b4 .graf .graf--h3 .graf-after--blockquote name="68b4"}

**What is encryption/decryption**

Encryption refers to the process of concealing sensitive data by
converting it to an unintelligible format. The only way to reverse the
process is to use a key; this is known as decryption. For further
explanation please
visit:[**https://www.cisco.com/c/en/us/products/security/encryption-explained.html**](https://www.cisco.com/c/en/us/products/security/encryption-explained.html){.markup--anchor
.markup--p-anchor
data-href="https://www.cisco.com/c/en/us/products/security/encryption-explained.html"
rel="noopener ugc nofollow noopener" target="_blank"} but in short,
encryption is just a way to protect data using a private key. For
example, the following string 'secret data' can be converted to
'QFnvZbCSffGzrauFXx9icxsN9UHHuU+sCL0sGcUCPGKyRquc9ldAfFIpVI+m8mc/' using
a key derived from the password 'pass'. It is also important to note
that there are many different types of encryption schemes, known as
algorithms such as AES-256/128, 3DES, Blowfish, ect. Among these, AES is
considered to be the reccomended encryption algorithm to use due to the
fact that it has been tested and proven to be a strong scheme.
Furthermore, there are two main types of encryption methods, aysmmetric
and symmetric. However, in this room we will be focusing on symmetric
encryption. If you are interested in knowing the difference or more on
encryption please visit:
[**https://www.thesslstore.com/blog/types-of-encryption-encryption-algorithms-how-to-choose-the-right-one/**](https://www.thesslstore.com/blog/types-of-encryption-encryption-algorithms-how-to-choose-the-right-one/){.markup--anchor
.markup--p-anchor
data-href="https://www.thesslstore.com/blog/types-of-encryption-encryption-algorithms-how-to-choose-the-right-one/"
rel="noopener ugc nofollow noopener" target="_blank"}

**How to encrypt**

As seen below, we have a text file with sensitive information inside of
it.

<figure id="8e4c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PwXiozLgwKdV65K2.png"
class="graf-image" data-image-id="0*PwXiozLgwKdV65K2.png"
data-width="794" data-height="77" />
</figure>

This can be encrypted using the the program gpg to encrypt it using the
AES-256 scheme:

**gpg --- cipher-algo \[encryption type\] \[encryption method\] \[file
to encrypt\]**

<figure id="d502" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OPz2qWASiU44gS34.png"
class="graf-image" data-image-id="0*OPz2qWASiU44gS34.png"
data-width="536" data-height="65" />
</figure>

You will notice how it will ask for a password. This is when you can
specify a password for gpg to derive the key from.

<figure id="b22f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UAiJpf2U57gxGJZg.png"
class="graf-image" data-image-id="0*UAiJpf2U57gxGJZg.png"
data-width="268" data-height="132" />
</figure>

Then a new encrypted file will be created with the extension gpg as you
can see below.

<figure id="6c14" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vy8BGmSoN9Xpcndk.png"
class="graf-image" data-image-id="0*vy8BGmSoN9Xpcndk.png"
data-width="299" data-height="29" />
</figure>

If you attempt to read the contents of this file you will see how it
shows unintelligible code.

<figure id="deba" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*937fe6oao22Nfg1q.png"
class="graf-image" data-image-id="0*937fe6oao22Nfg1q.png"
data-width="805" data-height="117" />
</figure>

**How to decrypt**

Decrypting is very easy as it only takes one line as shown below:

**gpg \[encrypted file\]**

<figure id="ace5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9dp2nWadS9UqePVb.png"
class="graf-image" data-image-id="0*9dp2nWadS9UqePVb.png"
data-width="255" data-height="48" />
</figure>

**Note:** You may notice how it does not ask us for the password to
decrypt the file, this is because we we have already entered it when we
were encrypting the file and so Linux stored the password for quick use.
However if we restart our system or attempt to decrypt the file in a
different linux machine, it will ask us for the password to decrypt the
file.

**Remember:** You can always use the man pages to learn more about what
you can do with gpg.

Now try it for yourself. Make a random text file and enter some readable
sentences in there before encrypting and decrypting it as illustrated
above.

**Question 1**. Create a text file write some readable sentence. Encrypt
it using gpg, it will ask you to set a password.

<figure id="bc19" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Bt0aq3uW8xIYqWfo.png"
class="graf-image" data-image-id="0*Bt0aq3uW8xIYqWfo.png"
data-width="542" data-height="128" />
</figure>

<figure id="70e7" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*iAQIgxYxTyc9cMwT.png"
class="graf-image" data-image-id="0*iAQIgxYxTyc9cMwT.png"
data-width="620" data-height="207" />
</figure>

Then decrypt using: ***gpg data.txt.gpg***

**Question 2**. You wish to encrypt a file called history_logs.txt using
the AES-128 scheme. What is the full command to do this?

> ***Answer: gpg --- cipher-algo AES-128 --- symmetric
> history_logs.txt***

**Question 3.** What is the command to decrypt the file you just
encrypted?

> ***Answer: gpg history_logs.txt.gpg***

**Question 4.** Find an encrypted file called layer4.txt, its password
is bob. Use this to locate the flag. What is the flag?

<figure id="35b5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*XGQviI96PZAoVJOj.png"
class="graf-image" data-image-id="0*XGQviI96PZAoVJOj.png"
data-width="718" data-height="457" />
</figure>

<figure id="b9c1" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*7cBaVTL3s9zlkZUg.png"
class="graf-image" data-image-id="0*7cBaVTL3s9zlkZUg.png"
data-width="784" data-height="300" />
</figure>

Finally, find the 'layer1.txt' decrypt it using gpg and password given,
you will the flag.

<figure id="a657" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Xp1LEI5RYxFXXwAD.png"
class="graf-image" data-image-id="0*Xp1LEI5RYxFXXwAD.png"
data-width="702" data-height="208" />
</figure>

### Task 7: Cracking encrypted gpg files {#267f .graf .graf--h3 .graf-after--figure name="267f"}

**How to crack encrypted files using john the ripper**

Now that you have a basic understanding using gpg, the next question is,
what if we do not have the password or key to decrypt the file? How can
we crack this. Well, similar to how we brute-forced the hashes in task 4
with John the Ripper, we can do the same for encrypted files.

If you are using Kali linux or Parrot OS, you should have a binary add
on called gpg2john. This binary program allows us to convert the gpg
file into a hash string that john the ripper can understand when it
comes to brute-forcing the password against a wordlist. Simply type
'sudo gpg2john' into your terminal to ensure you have it. The output
should be as seen below. In any case if you do not have it installed
head over to:
[**https://github.com/openwall/john**](https://github.com/openwall/john){.markup--anchor
.markup--p-anchor data-href="https://github.com/openwall/john"
rel="noopener ugc nofollow noopener" target="_blank"} and follow the
instructions to install it.

<figure id="4527" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Rg3S-52s-GCkKwMe.png"
class="graf-image" data-image-id="0*Rg3S-52s-GCkKwMe.png"
data-width="729" data-height="91" />
</figure>

Next, type the following command below to generate the hash for John the
Ripper:

gpg2john \[encrypted gpg file\] \> \[filename of the hash you want to
create\]

<figure id="6f7f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NxvlYvY7Rnx9tJef.png"
class="graf-image" data-image-id="0*NxvlYvY7Rnx9tJef.png"
data-width="382" data-height="45" />
</figure>

The command above allows us to generate the hash for John the Ripper to
understand. Next we can begin the fun part of cracking the encrypted
file as seen below:

john wordlist=\[location/name of wordlist\] --- format=gpg \[name of
hash we just created\]

<figure id="c487" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JgoB85E8lH-IdPZP.png"
class="graf-image" data-image-id="0*JgoB85E8lH-IdPZP.png"
data-width="532" data-height="24" />
</figure>

The result should reveal the password if you have used a strong wordlist
that contains it.

<figure id="d670" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wHC60W59o-_dC-wi.png"
class="graf-image" data-image-id="0*wHC60W59o-_dC-wi.png"
data-width="623" data-height="194" />
</figure>

Now try it yourself! Encrypt a file and use a common password contained
in the wordlist you wish to use. Follow the instructions above to
decrypt as if you are a hacker. If it worked, well done.

**Question 1**. Find an encrypted file called personal.txt.gpg and find
a wordlist called data.txt. Use tac to reverse the wordlist before
brute-forcing it against the encrypted file. What is the the password to
the encrypted file?

<figure id="375b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bTddaD5LU8BP8E6Q.png"
class="graf-image" data-image-id="0*bTddaD5LU8BP8E6Q.png"
data-width="818" data-height="208" />
</figure>

Now I do the same with the wordlist

<figure id="eca4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5bLlyVSTeOMW2ERQ.png"
class="graf-image" data-image-id="0*5bLlyVSTeOMW2ERQ.png"
data-width="775" data-height="204" />
</figure>

Now I need to use **tac data.txt \> reversed_data.txt** to reverse the
contents of the wordlist. To use john I first need to extract the hash
from the personal.txt.gpg. I do that with **gpg2john personal.txt.gpg \>
personal.hash**

Now I just need to run john to solve it for me.

<figure id="c801" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wUG9uDSsre8EZarx.png"
class="graf-image" data-image-id="0*wUG9uDSsre8EZarx.png"
data-width="695" data-height="484" />
</figure>

> ***Answer: valamanezivonia***

**Question 2.** What is written in this now decrypted file?

<figure id="70b3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vZULdw-9jWc491XB.png"
class="graf-image" data-image-id="0*vZULdw-9jWc491XB.png"
data-width="486" data-height="406" />
</figure>

> ***Answer: getting stronger in linux***

### TASK 8: Reading SQL Databases in Linux {#2de1 .graf .graf--h3 .graf-after--blockquote name="2de1"}

**What is SQL?**

SQL is a language for storing, manipulating and retrieving data from
databases. Therefore, it is important to firmly grasp the concept of how
to read data from databases in Linux. If your understanding of databases
is weak or you understanding nothing about them, please read this first
before continuing:
[**https://www.elated.com/mysql-for-absolute-beginners/**](https://www.elated.com/mysql-for-absolute-beginners/){.markup--anchor
.markup--p-anchor
data-href="https://www.elated.com/mysql-for-absolute-beginners/"
rel="noopener ugc nofollow noopener" target="_blank"} as it will explain
fully the concept of databases for beginners. The key thing to remember
is that developers mostly create 'relational databases' which use
multiple databases that reference each other for organising data, hence
the name 'relational databases'. Furthermore, each database contains
tables of records and each table can consist of multiple columns and
rows which store the data in a organised format. Now that we have gotten
that out of the way let's begin.

Since this is a beginners room we will be reading the the database of a
local mysql workspace. This can be done as follows:

**Service mysql start/stop**

Start starts mysql while stop stops it. Additionally, you could use
restart if you encounter any issues while mysql is running.

<figure id="2f93" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BZsvXsT-ZYqkwW4A.png"
class="graf-image" data-image-id="0*BZsvXsT-ZYqkwW4A.png"
data-width="243" data-height="29" />
</figure>

**Connect to remote SQL database:**

Mysql databases can be hosted for remote access. To access remote
databases use the following command:

mysql -u \[username\] -p -h \[host ip\]

<figure id="f4b5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0swiqsY8m--kL_W4.png"
class="graf-image" data-image-id="0*0swiqsY8m--kL_W4.png"
data-width="350" data-height="37" />
</figure>

**Open SQL database file locally:**

To open mysql file/files locally, simply change to the directory of the
mysql file and type mysql as shown below. You'll be taken to a
specialised command prompt for mysql.

Note: In some cases you may have to run mysql -p \[password\] if the
mysql system was configured to require authenticiation.

1\. mysql -u \[username\] -p

<figure id="cbc1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6tqws8SFeMSaYIaH.png"
class="graf-image" data-image-id="0*6tqws8SFeMSaYIaH.png"
data-width="805" data-height="248" />
</figure>

Type "source" followed by the filename of the mysql database to specify
that you wish to view its database.

2\. source \[sql filename\]

<figure id="d104" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nmXPXTFoN5xzo1RC.png"
class="graf-image" data-image-id="0*nmXPXTFoN5xzo1RC.png"
data-width="209" data-height="37" />
</figure>

**Displaying the databases**

After this, you will see how mysql takes a little time to load the
database. Once finished, type the following too see all of the
relational databases:

SHOW DATABASES;

<figure id="d86f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*f3CdSyReW44PsaSy.png"
class="graf-image" data-image-id="0*f3CdSyReW44PsaSy.png"
data-width="458" data-height="304" />
</figure>

**Choosing a database to view**

**We can select one of the databases by using the use command followed
by the name of it. In the example below we select the 'employees'
database.**

**USE \[database name\]**

<figure id="95db" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*X_iQW_XDhU5DsEim.png"
class="graf-image" data-image-id="0*X_iQW_XDhU5DsEim.png"
data-width="413" data-height="109" />
</figure>

**Displaying the tables in the selected database**

We can display which tables inside that database we selected previously
using:

SHOW TABLES;

<figure id="1248" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*H3tXJgk7oWLae5j3.png"
class="graf-image" data-image-id="0*H3tXJgk7oWLae5j3.png"
data-width="401" data-height="362" />
</figure>

Describing the table data structure

We can also view the table structure of individual tables using the
DESCRIBE command:

DESCRIBE \[table name\]

<figure id="18a7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*y0qPdAZf7dy8OWQo.png"
class="graf-image" data-image-id="0*y0qPdAZf7dy8OWQo.png"
data-width="677" data-height="332" />
</figure>

**Displaying all the data stored in a specific table**

Now for the really fun part. Let's display all the data stored in the
employees database using the following:

SELECT \* FROM \[table name\]

<figure id="54f1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KWLfglFLVC0i9YiS.png"
class="graf-image" data-image-id="0*KWLfglFLVC0i9YiS.png"
data-width="541" data-height="68" />
</figure>

As seen below, we can see that this database contains some personal
employee information.

<figure id="2689" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*XLbzOWetMWDrF25p.png"
class="graf-image" data-image-id="0*XLbzOWetMWDrF25p.png"
data-width="795" data-height="385" />
</figure>

**Question 1**. Find a file called employees.sql and read the SQL
database. (Sarah and Sameer can log both into mysql using the password:
password). Find the flag contained in one of the tables. What is the
flag?

First off I need to find the database I use the following command to
find it:

**find / -type f -name employees.sql 2\>/dev/null**

<figure id="b70c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JURwuYqzRI5EgZ2Z.png"
class="graf-image" data-image-id="0*JURwuYqzRI5EgZ2Z.png"
data-width="644" data-height="87" />
</figure>

I found the database path /home/sarah/serverLx/employees.sql I use the
command **service mysql status** to see if mysql allready is running.

<figure id="9a1c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fs-26iuok_pWupjf.png"
class="graf-image" data-image-id="0*fs-26iuok_pWupjf.png"
data-width="565" data-height="300" />
</figure>

In this case it is so I cd to /home/sarah/serverLx/ and open mysql with

> *mysql -u sarah -p*

providing the password that I got from the question,
password=**password**

-u tells mysql what user it should run as\
-p tells mysql that I want to provide a password

<figure id="2bd8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*A5G7ZWsh3Pm1h89M.png"
class="graf-image" data-image-id="0*A5G7ZWsh3Pm1h89M.png"
data-width="798" data-height="346" />
</figure>

First I need to tell mysql what database I want to use, I do this with
the

**source employees.sql** command.

<figure id="e01b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Wm56ql78lyTF8MwE.png"
class="graf-image" data-image-id="0*Wm56ql78lyTF8MwE.png"
data-width="532" data-height="356" />
</figure>

The next step is to load the database and search for the flag. I use the
command **USE employees;** to enter into the employees database since
that's where I was told the flag would be.

<figure id="7c5f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FhJEZuWmV9kBDs0y.png"
class="graf-image" data-image-id="0*FhJEZuWmV9kBDs0y.png"
data-width="315" data-height="403" />
</figure>

At this point I know that the flag is in one of these tables, however I
have no clue in which one. I use the **DESCRIBE employees;** to see if
that gives me a hint in where to look.

Now, you can notice that the flag contains '{' symbol from the format
given in answer space. From employee table which datatype will have that
symbol, so int cannot have because it has all number only, data also
cannot have that symbol, same applies for gender.\
Lastly, it is narrowed down to **first_name** and **last_name** because
it is using varchar datatype. We'll use pattern to find the flag.\
You can find more info on w3schools:
[https://www.w3schools.com/SQL/func_sqlserver_patindex.asp](https://www.w3schools.com/SQL/func_sqlserver_patindex.asp){.markup--anchor
.markup--p-anchor
data-href="https://www.w3schools.com/SQL/func_sqlserver_patindex.asp"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="39b5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EZzgwQWu7vJBw2eX.png"
class="graf-image" data-image-id="0*EZzgwQWu7vJBw2eX.png"
data-width="792" data-height="222" />
</figure>

### TASK 9: Final Challenge {#15dd .graf .graf--h3 .graf-after--figure name="15dd"}

**Question 1** .Go to the /home/shared/chatlogs directory and read the
first chat log named: LpnQ. Use this to help you to proceed to the next
task.

<figure id="e3c7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LvobCNlzFddnXvf6.png"
class="graf-image" data-image-id="0*LvobCNlzFddnXvf6.png"
data-width="606" data-height="240" />
</figure>

**Question 2**. What is Sameer's SSH password?

First of I need to distinguish the relevant parts of the message. For
this question I want to find Sameer's SSH password.\
Lucy says that the new security engineer has accidently stored a SSH
password in plain text somwhere. I check to see if I can find anything
by just searching for Sameer inside a file with\
grep -iRl Sameer /home 2\>/dev/null I find three chatlogs one being the
one I just read. I view the others and find the SSH password

``` {#4aff .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
-i is supplied to make a non case sensitive search. 
 -R is supplied to search through all files recursivly 
 -l is supplied to only print files that matches the word I'm searching for.  I search in /home because I'm mainly looking for chatlogs and they are  stored under home/shared in this case. I use /home instead of  /home/shared because I want to search both home/shared and home/sarah at  the same time.
```

<figure id="7257" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*kVWkVbVLw9WlM4Zh.png"
class="graf-image" data-image-id="0*kVWkVbVLw9WlM4Zh.png"
data-width="723" data-height="435" />
</figure>

> ***Answer: thegreatestpasswordever000***

**Question 2** . What is the password for the sql database back-up copy

By refering back to the second message I'm told that I need to sign in
to Sameers account and search for it. I'm also told that I should look
for a file about 50mb in the **home/shared/sql/conf**. By finding that
file I will know where the wordlists are stored and that the wordlist
I'm looking for has a word starting with "ebq" inside it. First off I
ssh into Sameer's account. After that I use **find /home/shared/sql/
-type f -size 50M** to search for the file. I find a file filled with
Lipsum text when I cat it, I open it with nano to search for it, but I
see that the information is at the top

<figure id="8e4f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*a1O5Of13DuJehF6I.png"
class="graf-image" data-image-id="0*a1O5Of13DuJehF6I.png"
data-width="648" data-height="133" />
</figure>

<figure id="e59f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*FyFdL6YtfuGLW7HN.png"
class="graf-image" data-image-id="0*FyFdL6YtfuGLW7HN.png"
data-width="875" data-height="213" />
</figure>

``` {#882d .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
aG9tZS9zYW1lZXIvSGlzdG9yeSBMQi9sYWJtaW5kL2xhdGVzdEJ1aWxkL2NvbmZpZ0JEQgo=
```

<figure id="ca42" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*zj_PEqE5HCLByceW.png"
class="graf-image" data-image-id="0*zj_PEqE5HCLByceW.png"
data-width="875" data-height="95" />
</figure>

I know the wordlist directory is encoded with base since I see the "="
padding at the end. I write to base64 code to a file and use **base64 -d
base.txt**

and get the directory that the wordlist is in. Now I need to find the
wordlist, I use **grep -iRl ebq /home/sameer/History\\
LB/labmind/latestBuild/configBDB/** to search for the wordlist. I find
three wordlists, I append to eachother to make one big wordlist. I do
this with **cat \>\>**

Next I need to find and download the actual backup, I was told it would
be

**/home/shared/sql/**

directory according to Sameer in a previous message. The backup would be
named with the date of the message(2020--08--13). I search for it with

**find /home/shared/sql/ -type f -name \*2020--08--13\* 2\>/dev/null**

and I found it. Now I need to copy it to my local machine with

**scp sameer@10.10.4.233:/home/shared/sql/2020--08--13.zip.gpg** .

<figure id="2787" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pIL15pUKASuZqzDV.png"
class="graf-image" data-image-id="0*pIL15pUKASuZqzDV.png"
data-width="841" data-height="213" />
</figure>

s mention in chat that the password begins with letters '**ebq**'. Use
grep command to word-list that only contains letters '**ebq**'. You will
find 3 files. Now combine these 3 files into 1 new file to make a
complete word-list.

<figure id="db91" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*e5sITjwiDWQDT2P4.png"
class="graf-image" data-image-id="0*e5sITjwiDWQDT2P4.png"
data-width="875" data-height="148" />
</figure>

move **wordlist.txt** to sameer's home directory

<figure id="daa1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RCfANaPo-_pDTEW0.png"
class="graf-image" data-image-id="0*RCfANaPo-_pDTEW0.png"
data-width="578" data-height="102" />
</figure>

now use the **grep** command to search for words in the **wordlist.txt**
that will start from **ebq**

**grep -e ebq wordlist.txt**

<figure id="d71a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-CgGLQI8qORGIeEs.png"
class="graf-image" data-image-id="0*-CgGLQI8qORGIeEs.png"
data-width="670" data-height="498" />
</figure>

<figure id="e8c9" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*jIE5PPQopGOnJnia.png"
class="graf-image" data-image-id="0*jIE5PPQopGOnJnia.png"
data-width="438" data-height="315" />
</figure>

Enter newWordlist passwrd one by one and you will get password
**ebqattle**

**Question 3**. Find the SSH password of the user James. What is the
password?

``` {#821b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
unzip 2020-08-13.zip
```

<figure id="22f3" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*MCJ3twDighf8ccCr.png"
class="graf-image" data-image-id="0*MCJ3twDighf8ccCr.png"
data-width="421" data-height="187" />
</figure>

notice that it has employees.sql database file, lets open mysql as sarah
and use the following commands:

**mysql -u sarah -p** (enter **password** for password)\
**source employees.sql\
show databases;\
use employees;\
describe employees;\
select \* from employees where first_name like 'James';**

<figure id="de61" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rVVzEril7Gy_Ho2J.png"
class="graf-image" data-image-id="0*rVVzEril7Gy_Ho2J.png"
data-width="780" data-height="202" />
</figure>

**Question 4**. SSH as james and change the user to root?

<figure id="6d71" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rh8K1jE9o1yrLKsY.png"
class="graf-image" data-image-id="0*rh8K1jE9o1yrLKsY.png"
data-width="469" data-height="184" />
</figure>

**Question 5**. What is the root flag?

<figure id="acab" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vHvPsMcO7oLN7BXL.png"
class="graf-image" data-image-id="0*vHvPsMcO7oLN7BXL.png"
data-width="470" data-height="182" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#7193 .graf .graf--h3 .graf-after--figure name="7193"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#e00e .graf .graf--h3 .graf-after--p name="e00e"}

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
.h-card} on [August 28, 2024](https://medium.com/p/48c2d241cfe8).

[Canonical
link](https://medium.com/@bevijaygupta/linux-strength-training-tryhackme-writeup-48c2d241cfe8){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
