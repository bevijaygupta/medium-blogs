::: {}
# Crack The Hash Level 2 Tryhackme Writeup {#crack-the-hash-level-2-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Crack The Hash Level 2"
:::

::::::: {.section .e-content field="body"}
:::::: {#713c .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Crack The Hash Level 2 Tryhackme Writeup {#4127 .graf .graf--h3 .graf--leading .graf--title name="4127"}

**This is a Writeup of Tryhackme room "Crack The Hash Level 2"**

<figure id="1ae5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1HvOrMlEFXMyJW0U.png"
class="graf-image" data-image-id="0*1HvOrMlEFXMyJW0U.png"
data-width="566" data-height="290" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/malstrings](https://tryhackme.com/room/malstrings){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malstrings"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Task 1: Introduction {#050b .graf .graf--h3 .graf-after--p name="050b"}

Password cracking is part of the penetration tester job but is rarely
taught on challenges platforms. In this room you will learn to how to
crack hashes, identify hash types, create custom wordlists, find
specific wordlists, create mutations rules, etc.

This room is a spiritual successor to [**Crack the
Hash**](https://tryhackme.com/room/crackthehash){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/crackthehash"
rel="noopener ugc nofollow noopener" target="_blank"}**.**

<figure id="8c3a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-jvsfb9iAvTRs8E9.png"
class="graf-image" data-image-id="0*-jvsfb9iAvTRs8E9.png"
data-width="501" data-height="124" />
</figure>

[https://tryhackme.com/room/crackthehash](https://tryhackme.com/room/crackthehash){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/crackthehash"
rel="noopener ugc nofollow noopener" target="_blank"}

I recommend you to have done the room [**Crack the
hash**](https://tryhackme.com/room/crackthehash){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/crackthehash"
rel="noopener ugc nofollow noopener" target="_blank"} before attempting
this one, which is harder and will use more advanced techniques.

However this room include a course about hash cracking before you have
to face the cracking challenges, it may be a good idea to read the
course part before doing [**Crack the
hash**](https://tryhackme.com/room/crackthehash){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/crackthehash"
rel="noopener ugc nofollow noopener" target="_blank"} if you are a new
comer.

### Task 2: Hash identification {#4bcb .graf .graf--h3 .graf-after--p name="4bcb"}

Often the first thing you will need when you encounter a hash, is trying
to identify which kind of hash it is.\
There are a lot of hash types, some are very famous like MD5 or SHA1 but
other are less and there are several hash types possible for a given
character set and length.

[**Haiti**](https://noraj.github.io/haiti/){.markup--anchor
.markup--p-anchor data-href="https://noraj.github.io/haiti/"
rel="noopener ugc nofollow noopener" target="_blank"} is a CLI tool to
identify the hash type of a given hash.
[**Install**](https://noraj.github.io/haiti/#/pages/install){.markup--anchor
.markup--p-anchor
data-href="https://noraj.github.io/haiti/#/pages/install"
rel="noopener ugc nofollow noopener" target="_blank"} it.

``` {#ddea .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
gem install haiti-hash
```

Launch Haiti on this hash:

``` {#a1ab .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
741ebf5166b9ece4cca88a3868c44871e8370707cf19af3ceaa4a6fba006f224ae03f39153492853
```

**Question 1**. What kind of hash it is?

<figure id="40c1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*r0SEArYjv7NiMmCB.png"
class="graf-image" data-image-id="0*r0SEArYjv7NiMmCB.png"
data-width="875" data-height="174" />
</figure>

> ***Answer: RIPEMD-320***

Launch Haiti on this hash:

``` {#9c77 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
1aec7a56aa08b25b596057e1ccbcb6d768b770eaa0f355ccbd56aee5040e02ee
```

<figure id="cd3f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*3k02f7PhzVT_vNpv.png"
class="graf-image" data-image-id="0*3k02f7PhzVT_vNpv.png"
data-width="771" data-height="280" />
</figure>

**Question 2**. What is Keccak-256 Hashcat code?

> ***Answer: 17800***

**Question 3.** What is Keccak-256 John the Ripper code?

> ***Answer: raw-keccak-256***

### Task 3: Wordlists {#f034 .graf .graf--h3 .graf-after--blockquote name="f034"}

For hash cracking you will often need some custom or specialized
dictionaries called wordlists.

[**SecLists**](https://github.com/danielmiessler/SecLists){.markup--anchor
.markup--p-anchor data-href="https://github.com/danielmiessler/SecLists"
rel="noopener ugc nofollow noopener" target="_blank"} is a collection of
multiple types of lists used during security assessments, collected in
one place. List types include usernames, passwords, URLs, sensitive data
patterns, fuzzing payloads, web shells, and many more.

[**wordlistctl**](https://github.com/BlackArch/wordlistctl){.markup--anchor
.markup--p-anchor data-href="https://github.com/BlackArch/wordlistctl"
rel="noopener ugc nofollow noopener" target="_blank"} is a script to
fetch, install, update and search wordlist archives from websites
offering wordlists with more than 6300 wordlists available.

[**Rawsec's CyberSecurity
Inventory**](https://inventory.raw.pm/overview.html){.markup--anchor
.markup--p-anchor data-href="https://inventory.raw.pm/overview.html"
rel="noopener ugc nofollow noopener" target="_blank"} is an inventory of
tools and resources about CyberSecurity. The
[**Cracking**](https://inventory.raw.pm/tools.html#title-tools-cracking){.markup--anchor
.markup--p-anchor
data-href="https://inventory.raw.pm/tools.html#title-tools-cracking"
rel="noopener ugc nofollow noopener" target="_blank"} category will be
especially useful to find wordlist generator tools.

**Note**: On the exercise below we will see how to use how to use
wordlistctl to download a list, for the example I took rockyou which is
a famous wordlist but if you use TryHackMe AttackBox or Kali Linux you
should already have it under `/usr/share/wordlists/`{.markup--code
.markup--p-code}, so you don\'t need to download it again, this is just
an example to show you how wordlistctl works.

[**RockYou**](https://en.wikipedia.org/wiki/RockYou#Data_breach){.markup--anchor
.markup--p-anchor
data-href="https://en.wikipedia.org/wiki/RockYou#Data_breach"
rel="noopener ugc nofollow noopener" target="_blank"} is a famous
wordlist contains a large set of commonly used password sorted by
frequency.

<figure id="85a9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Yn39COK5T9YgiE2m.png"
class="graf-image" data-image-id="0*Yn39COK5T9YgiE2m.png"
data-width="602" data-height="360" />
</figure>

To search for this wordlist with wordlistclt run:

`wordlistctl search rockyou`{.markup--code .markup--p-code}

<figure id="f24b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jczcxssUGe30nkI3.png"
class="graf-image" data-image-id="0*jczcxssUGe30nkI3.png"
data-width="545" data-height="275" />
</figure>

**Question 1**. Which option do you need to add to the previous command
to search into local archives instead of remote ones?

<figure id="fa1d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*XYzbP1q4QGXHDXcH.png"
class="graf-image" data-image-id="0*XYzbP1q4QGXHDXcH.png"
data-width="704" data-height="372" />
</figure>

> ***Answer: -l***

Download and install rockyou wordlist by running this command:
`wordlistctl fetch -l rockyou`{.markup--code .markup--p-code}

<figure id="6ab2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vw1GgTJn379RzRLk.png"
class="graf-image" data-image-id="0*vw1GgTJn379RzRLk.png"
data-width="645" data-height="211" />
</figure>

Now search again for rockyou on your local archive with
`wordlistctl search -l rockyou`{.markup--code .markup--p-code}

<figure id="ab78" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1_yFUdqjICURuWFX.png"
class="graf-image" data-image-id="0*1_yFUdqjICURuWFX.png"
data-width="682" data-height="183" />
</figure>

You should see that the wordlist is deployed at
`/usr/share/wordlists/passwords/rockyou.txt.tar.gz`{.markup--code
.markup--p-code}

But the wordlist is compressed in a tar.gz archive, to decompress it run
`wordlistctl fetch -l rockyou -d`{.markup--code .markup--p-code}.

<figure id="8657" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xbuVUmiWihXqgVHm.png"
class="graf-image" data-image-id="0*xbuVUmiWihXqgVHm.png"
data-width="692" data-height="174" />
</figure>

If you run `wordlistctl search -l rockyou`{.markup--code
.markup--p-code} one more time, what is the path where is stored the
wordlist?

<figure id="7772" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*c0vxNxNwsSIiPtys.png"
class="graf-image" data-image-id="0*c0vxNxNwsSIiPtys.png"
data-width="623" data-height="173" />
</figure>

> ***Answer: /usr/share/wordlists/passwords/rockyou.txt***

You can search for a wordlist about a specific subject (eg. facebook)
`wordlistctl search facebook`{.markup--code .markup--p-code} or list all
wordlists from a category (eg. fuzzing)
`wordlistctl list -g fuzzing`{.markup--code .markup--p-code}.

**Question 2**. What is the name of the first wordlist in the usernames
category?

<figure id="26a3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8KPkDxp7v8lliEaX.png"
class="graf-image" data-image-id="0*8KPkDxp7v8lliEaX.png"
data-width="576" data-height="352" />
</figure>

> ***Answer: CommonAdminBase64***

### Task 4: Cracking tools, modes & rules {#a8c5 .graf .graf--h3 .graf-after--blockquote name="a8c5"}

Finally you'll need a cracking tool, the 2 very common ones are:

- [[**Hashcat**](https://hashcat.net/hashcat/){.markup--anchor
  .markup--li-anchor data-href="https://hashcat.net/hashcat/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#f38c}
- [[**John the Ripper**](http://www.openwall.com/john/){.markup--anchor
  .markup--li-anchor data-href="http://www.openwall.com/john/"
  rel="noopener ugc nofollow noopener" target="_blank"} (jumbo
  version)]{#4207}

There are several modes of cracking you can use:

- [**Wordlist mode**, which consist in trying all words contained in a
  dictionary. For example, a list of common passwords, a list of
  usernames, etc.]{#d4f6}
- [**Incremental mode**, which consist in trying all possible character
  combinations as passwords. This is powerful but much more longer
  especially if the password is long.]{#1cba}
- [**Rule mode**, which consist in using the wordlist mode by adding it
  some pattern or mangle the string. For example adding the current
  year, or appending a common special character.]{#0c98}

There are 2 ways of performing a rule based bruteforce:

1.  [Generating a custom wordlist and using the classic wordlist mode
    with it.]{#c726}
2.  [Using a common wordlist and tell the cracking tool to apply some
    custom mangling rules on it.]{#8173}

The second option is much more powerful as you wont waste gigabytes by
storing tons of wordlists and waste time generating ones you will use
only one time. Rather having a few interesting lists and apply various
mangling rules that yo ucan re-use over different wordlist.

John the Ripper already include various mangling rules but you can
create your owns and apply them the wordlist when cracking:

``` {#333c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
$ john hash.txt --wordlist=/usr/share/wordlists/passwords/rockyou.txt rules=norajCommon02
```

You can consult John the Ripper [**Wordlist rules
syntax**](https://www.openwall.com/john/doc/RULES.shtml){.markup--anchor
.markup--p-anchor
data-href="https://www.openwall.com/john/doc/RULES.shtml"
rel="noopener ugc nofollow noopener" target="_blank"} for creating your
own rules.\
I'll give you the main ideas of mutation rules, of course several can be
combined together

- [**Border mutation** --- commonly used combinations of digits and
  special symbols can be added at the end or at the beginning, or
  both]{#fc45}
- [**Freak mutation** --- letters are replaced with similarly looking
  special symbols]{#f84d}
- [**Case mutation** --- the program checks all variations of
  uppercase/lowercase letters for any character]{#273e}
- [**Order mutation** --- character order is reversed]{#1dac}
- [**Repetition mutation** --- the same group of characters are repeated
  several times]{#c766}
- [**Vowels mutation** --- vowels are omitted or capitalized]{#8464}
- [**Strip mutation** --- one or several characters are removed]{#83ab}
- [**Swap mutation** --- some characters are swapped and change
  places]{#4206}
- [**Duplicate mutation** --- some characters are duplicated]{#d9c0}
- [**Delimiter mutation** --- delimiters are added between
  characters]{#912d}

Depending of your distribution, the John configuration may be located at
`/etc/john/john.conf`{.markup--code .markup--p-code} and/or
`/usr/share/john/john.conf`{.markup--code .markup--p-code}. To locate
the JtR install directory run locate `john.conf`{.markup--code
.markup--p-code}, then create `john-local.conf`{.markup--code
.markup--p-code} in the same directory (in my
case`/usr/share/john/john-local.conf`{.markup--code .markup--p-code})
and create our rules in here.

<figure id="9ebb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4WrKfNBgdgQsbIAJ.png"
class="graf-image" data-image-id="0*4WrKfNBgdgQsbIAJ.png"
data-width="420" data-height="227" />
</figure>

Let's use the top 10 000 most used password list from
[SecLists](https://github.com/danielmiessler/SecLists#install){.markup--anchor
.markup--p-anchor
data-href="https://github.com/danielmiessler/SecLists#install"
rel="noopener ugc nofollow noopener" target="_blank"}
(`/usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt`{.markup--code
.markup--p-code}) and generate a simple border mutation by appending all
2 digits combinations at the end of each password.\
Let\'s edit `/usr/share/john/john-local.conf`{.markup--code
.markup--p-code} and add a new rule:,

Now let's crack the SHA1 hash
`2d5c517a4f7a14dcb38329d228a7d18a3b78ce83`{.markup--code
.markup--p-code}, we just have to write the hash in a text file and to
specify the hash type, the wordlist and our rule name.
`john hash.txt --format=raw-sha1 --wordlist=/usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt --rules=THM01`{.markup--code
.markup--p-code}

What was the password?

<figure id="6e89" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Fhnnim0UhPs1juvD.png"
class="graf-image" data-image-id="0*Fhnnim0UhPs1juvD.png"
data-width="875" data-height="369" />
</figure>

> ***Answer: moonligh56***

### Task 5: Custom wordlist generation {#2f6b .graf .graf--h3 .graf-after--blockquote name="2f6b"}

As I said in the previous task mangling rules avoid to waste storage
space and time but there are some cases where generating a custom
wordlist could be a better idea:

- [You will often re-use the wordlist, generating one will save
  computation power rather than using a mangling rule]{#5507}
- [You want to use the wordlist with several tools]{#3481}
- [You want to use a tool that support wordlists but not mangling
  rules]{#a88a}
- [You find the custom rule syntax of John too complex]{#ddcd}

**Question 1**. Crack the following md5 hash with the wordlist generated
in the previous steps.

<figure id="8fdd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KXuLHAsZtXzvF1wH.png"
class="graf-image" data-image-id="0*KXuLHAsZtXzvF1wH.png"
data-width="675" data-height="337" />
</figure>

> ***Answer: mOlo\$\$u\$***

Now let's use
[**CeWL**](https://github.com/digininja/CeWL){.markup--anchor
.markup--p-anchor data-href="https://github.com/digininja/CeWL"
rel="noopener ugc nofollow noopener" target="_blank"} to generate a
wordlist from a website. It could be useful to retrieve a lot of words
related to the password's topic.

For example to download all words from example.org with a depth of 2,
run:\
`cewl -d 2 -w $(pwd)/example.txt https://example.org`{.markup--code
.markup--p-code}\
The depth is the number of link level the spider will follow.

What is the last word of the list?

<figure id="257e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*T3kGFAMmEnFyjCyn.png"
class="graf-image" data-image-id="0*T3kGFAMmEnFyjCyn.png"
data-width="580" data-height="372" />
</figure>

> ***Answer: information***

With
[**TTPassGen**](https://github.com/tp7309/TTPassGen){.markup--anchor
.markup--p-anchor data-href="https://github.com/tp7309/TTPassGen"
rel="noopener ugc nofollow noopener" target="_blank"} we can craft
wordlists from scratch. Create a first wordlist containing all 4 digits
PIN code value.

`ttpassgen --rule '[?d]{4:4:*}' pin.txt`{.markup--code .markup--p-code}

``` {#4b8b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
pip install ttpassgen
```

<figure id="9acf" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*QKlmWavb0NYiOvI9.png"
class="graf-image" data-image-id="0*QKlmWavb0NYiOvI9.png"
data-width="875" data-height="175" />
</figure>

Generate a list of all lowercase chars combinations of length 1 to 3.

`ttpassgen --rule '[?l]{1:3:*}' abc.txt`{.markup--code .markup--p-code}

<figure id="cefc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*U3Lb15cbKU9X0nJP.png"
class="graf-image" data-image-id="0*U3Lb15cbKU9X0nJP.png"
data-width="875" data-height="169" />
</figure>

Then we can create a new wordlist that is a combination of several
wordlists. Eg. combine the PIN wordlist and the letter wordlist
separated by a dash.

`ttpassgen --dictlist 'pin.txt,abc.txt' --rule '$0[-]{1}$1' combination.txt`{.markup--code
.markup--p-code}

Be warned combining wordlists quickly generated huge files, here
combination.txt is 1.64 GB.

``` {#36bd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
$ wc pin.txt 
10000 10000 50000 pin.txt$ wc abc.txt 
18278 18278 72384 abc.txt$ wc combination.txt 
 182780000  182780000 1637740000 combination.txt
```

<figure id="ffb1" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*dwKR5PDtzm6AbMTk.png"
class="graf-image" data-image-id="0*dwKR5PDtzm6AbMTk.png"
data-width="875" data-height="168" />
</figure>

Crack this md5 hash with combination.txt.

`e5b47b7e8df2597077e703c76ee86aee`{.markup--code .markup--p-code}

<figure id="1f97" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zw_ymVdOou48duJw.png"
class="graf-image" data-image-id="0*zw_ymVdOou48duJw.png"
data-width="677" data-height="322" />
</figure>

> ***Answer: 1551-li***

### Task 6: It's time to crack hashes {#3993 .graf .graf--h3 .graf-after--blockquote name="3993"}

You will have to crack several hashes. For each hash you will be given a
short scenario that will help you to create a mangling rules, build a
wordlist or finding some specialized data you'll need to crack the hash.

The scenarios are located on the website: Password advisor
(http://10.10.92.247), each piece of advice matches one of the following
hashes (in the same order).

**Question 1**. Advice n°1 **b16f211a8ad7f97778e5006c7cecdf31**

Hint: English male name, MD5, Border mutation, custom rule

<figure id="992a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SJlEzJTY5zA6UaxN.png"
class="graf-image" data-image-id="0*SJlEzJTY5zA6UaxN.png"
data-width="844" data-height="262" />
</figure>

<figure id="f368" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*vVX1pPXH-KykfQSr.png"
class="graf-image" data-image-id="0*vVX1pPXH-KykfQSr.png"
data-width="674" data-height="184" />
</figure>

The question mentions it uses border mutation where we add combination
of digits and/or special characters to both or one of the ends of the
word. If we do it by creating wordlists, it will take too much time and
storage. To go around this, we can use mangling rules as the room
teaches in one of the previous tasks. For this task we only need the 5
Digits+Special Character Combination eg: **xxxxxname**, **xxxxnamex**,
**xxxnamexx**, **xxnamexxx**, **xnamexxxx**, **namexxxxx** where x is
either a special character or digit.

``` {#1c82 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
Adding rule in john.conf
locate john.conf
leafpad /etc/john/john.conf
```

Download Rules from the link

[http://s000.tinyupload.com/index.php?file_id=07601583944998921775](http://s000.tinyupload.com/index.php?file_id=07601583944998921775){.markup--anchor
.markup--p-anchor
data-href="http://s000.tinyupload.com/index.php?file_id=07601583944998921775"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="207f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*XQj2FSdMnYFRGKu6.png"
class="graf-image" data-image-id="0*XQj2FSdMnYFRGKu6.png"
data-width="875" data-height="301" />
</figure>

The **SAM01** is the name of the rule you will call it with

<figure id="f536" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hd5IHUzYDVn5UTJ9.png"
class="graf-image" data-image-id="0*hd5IHUzYDVn5UTJ9.png"
data-width="875" data-height="212" />
</figure>

**Question 2**. Advice n°2 **7463fcb720de92803d179e7f83070f97**\
Hint: English female name, MD5, Border mutation, custom rule

<figure id="6aaa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7qKLbH7S7VKxaTja.png"
class="graf-image" data-image-id="0*7qKLbH7S7VKxaTja.png"
data-width="792" data-height="316" />
</figure>

``` {#4133 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
# Following from the previous question, open the john.conf file and replace the line starting with cAz… with the following:
```

### [http://s000.tinyupload.com/index.php?file_id=45684960321058540739&source=post_page\-\-\-\--292c86b72ea0\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--](http://s000.tinyupload.com/index.php?file_id=45684960321058540739&source=post_page-----292c86b72ea0--------------------------------){.markup--anchor .markup--h3-anchor data-href="http://s000.tinyupload.com/index.php?file_id=45684960321058540739&source=post_page-----292c86b72ea0--------------------------------" rel="nofollow noopener" target="_blank"} {#129d .graf .graf--h3 .graf-after--pre name="129d"}

(Don't replace \[List.Rules:SAM01\], replace the rule below it)

<figure id="aa20" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Wn04n75f4IdEWLmW.png"
class="graf-image" data-image-id="0*Wn04n75f4IdEWLmW.png"
data-width="875" data-height="144" />
</figure>

<figure id="ef18" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*UKMaz3NefH0YiULa.png"
class="graf-image" data-image-id="0*UKMaz3NefH0YiULa.png"
data-width="875" data-height="144" />
</figure>

So now its done

This time I sorted the names from longest to shortest so I can avoid the
really short length names as I didn't think they would be used here so I
could save some time

``` {#8247 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat femalenames-usa-top1000.txt| awk '{ print length($0) " " $0; }' $file | sort -r -n | cut -d ' ' -f 2- > sorted_female.txt
```

<figure id="c8e6" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*tNT1PWkCr4O_KHYP.png"
class="graf-image" data-image-id="0*tNT1PWkCr4O_KHYP.png"
data-width="875" data-height="319" />
</figure>

**Question 3**. Advice n°3 **f4476669333651be5b37ec6d81ef526f**

Hint: Town name of Mexico, MD5, Freak mutation, mentalist tool

<figure id="de36" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3zqSh_kuirTLwaFq.png"
class="graf-image" data-image-id="0*3zqSh_kuirTLwaFq.png"
data-width="747" data-height="254" />
</figure>

Remove spaces from file

``` {#4f27 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat cities.txt | tr -d "[:blank:]"
```

Change Uppercase to Lowercase

``` {#c9a5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="less"}
cat cities.txt | tr [:upper:] [:lower:]
```

We will use the default l33t rule which will try different combination
of letter replacements eg: Mexico -\> M3x1c0 or M3x1co and so on.

<figure id="0216" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YZwd8PdyNwPxsp1w.png"
class="graf-image" data-image-id="0*YZwd8PdyNwPxsp1w.png"
data-width="742" data-height="301" />
</figure>

**Question 4**.Advice n°4 **a3a321e1c246c773177363200a6c0466a5030afc**

Hint: User's own name, SHA1, case mutation with existing rule

The password is **Case mutated** where we toggle the lowercase and
uppercase for different chars and we can use a default rule for this.
The default rule to use here is **NT**
([Credit](https://security.stackexchange.com/questions/124044/use-john-the-ripper-to-permutate-cases-in-one-password){.markup--anchor
.markup--p-anchor
data-href="https://security.stackexchange.com/questions/124044/use-john-the-ripper-to-permutate-cases-in-one-password"
rel="noopener ugc nofollow noopener" target="_blank"}).

<figure id="6881" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*J9Eq0QhS7jMAOTWu.png"
class="graf-image" data-image-id="0*J9Eq0QhS7jMAOTWu.png"
data-width="755" data-height="375" />
</figure>

**Question 5**. Advice n°5 **d5e085772469d544a447bc8250890949**\
Hint: Lyrics, MD5, Order mutation, lyricpass

``` {#34cd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo ‘d5e085772469d544a447bc8250890949’ > hash.txt
git clone https://github.com/initstring/lyricpass.git
```

<figure id="8491" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*3QI_VxhcajTtUZOO.png"
class="graf-image" data-image-id="0*3QI_VxhcajTtUZOO.png"
data-width="875" data-height="305" />
</figure>

``` {#2406 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
I changed file names using mv
mv wordlist-2021-02-15-17.52.57 wordlist
mv raw-lyrics-2021-02-15-17.52.57 raw-lyrics
```

As listed
[**here**](https://hashcat.net/wiki/doku.php?id=rule_based_attack){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=rule_based_attack"
rel="noopener ugc nofollow noopener" target="_blank"}, we can make use
of the hashcat rule for reversing characters 'r'.

``` {#0445 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
# Create a rule using mask processor which is usually bundled with hashcat:
mp64 -o reverse.rule ‘r’If you don't have mp64 (mask processor), you can make the rule without it:
echo ‘r’ > reverse.rulehashcat -m 0 hash.txt raw-lyrics -r reverse.rule
```

<figure id="7fee" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*m_zOFtsShEilVSO2.png"
class="graf-image" data-image-id="0*m_zOFtsShEilVSO2.png"
data-width="570" data-height="192" />
</figure>

<figure id="387e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*BBM3HaqncfjxO809.png"
class="graf-image" data-image-id="0*BBM3HaqncfjxO809.png"
data-width="875" data-height="202" />
</figure>

**Question 6**. Advice n°6 **377081d69d23759c5946a95d1b757adc**

Hint: Phone number, MD5, No mutation, pnwgen

``` {#14bd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo 377081d69d23759c5946a95d1b757adc > hash.txt
```

Searching for Sint Maarten phone number online reveals +1 721 and
counting the asterisks in TryHackMe answer box gives us 12 characters.

<figure id="2b0d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yt6Z1IVbOYcMCS9j.png"
class="graf-image" data-image-id="0*yt6Z1IVbOYcMCS9j.png"
data-width="791" data-height="206" />
</figure>

- [1 721--555--1212 -\> +17215551212 (12 chars)\
  We know that it will always start with +1721 (first 5 chars) so we
  only need to brute-force the last 7 chars.\
  Eg: +1721xxxxxxx]{#2f4f}

<figure id="e33f" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*zkV818vsOktVM5Hz.png"
class="graf-image" data-image-id="0*zkV818vsOktVM5Hz.png"
data-width="762" data-height="230" />
</figure>

I know that the question hints towards using pnwgen, but I felt
comfortable using ttpassgen even though I got it wrong a few times in
the start.

<figure id="185c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DScxwImISpbRyKJ6.png"
class="graf-image" data-image-id="0*DScxwImISpbRyKJ6.png"
data-width="798" data-height="294" />
</figure>

Crack the hash

<figure id="bb03" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*B3ZgWAAGhYMoiNUB.png"
class="graf-image" data-image-id="0*B3ZgWAAGhYMoiNUB.png"
data-width="650" data-height="230" />
</figure>

**Question 7**. Advice n°7
**ba6e8f9cd4140ac8b8d2bf96c9acd2fb58c0827d556b78e331d1113fcbfe425ca9299fe917f6015978f7e1644382d1ea45fd581aed6298acde2fa01e7d83cdbd**

Hint: Rockyou, SHA3--512, No mutation

<figure id="0b95" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3OhGVTXxneiXHUhH.png"
class="graf-image" data-image-id="0*3OhGVTXxneiXHUhH.png"
data-width="875" data-height="212" />
</figure>

<figure id="a5b2" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*iX_pmVxgRRpj-hr9.png"
class="graf-image" data-image-id="0*iX_pmVxgRRpj-hr9.png"
data-width="875" data-height="164" />
</figure>

**Question 8**. Advice n°8
**9f7376709d3fe09b389a27876834a13c6f275ed9a806d4c8df78f0ce1aad8fb343316133e810096e0999eaf1d2bca37c336e1b7726b213e001333d636e896617**

Hint: Web scrapping, blake2, Repetition, CeWL

I was getting an error when I tried cracking the hashing but it turns
out I wrote it in the [**wrong
format**](https://hashcat.net/forum/thread-8726.html){.markup--anchor
.markup--p-anchor data-href="https://hashcat.net/forum/thread-8726.html"
rel="noopener ugc nofollow noopener" target="_blank"}. Following on from
[**previous
link**](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"}**,** we find that
the correct format for the BLAKE2 hash is to add **\$BLAKE2\$** at the
start of the hash.

<figure id="3b4b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zIXG3KAybgo6Kt5y.png"
class="graf-image" data-image-id="0*zIXG3KAybgo6Kt5y.png"
data-width="875" data-height="221" />
</figure>

Add rules in **john.conf**

<figure id="6e88" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*th-QS1Ld0ROUQ6s2.png"
class="graf-image" data-image-id="0*th-QS1Ld0ROUQ6s2.png"
data-width="229" data-height="110" />
</figure>

<figure id="d02a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*0e-SOCzCU7RzQR0V.png"
class="graf-image" data-image-id="0*0e-SOCzCU7RzQR0V.png"
data-width="777" data-height="228" />
</figure>

**Question 9**. Advice n°9
**\$6\$kI6VJ0a31.SNRsLR\$Wk30X8w8iEC2FpasTo0Z5U7wke0TpfbDtSwayrNebqKjYWC4gjKoNEJxO/DkP.YFTLVFirQ5PEh4glQIHuKfA/**

Hint: Rockyou, SHA512-crypt, No mutation

<figure id="0e2d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*e9nxhr0toi_eVMmA.png"
class="graf-image" data-image-id="0*e9nxhr0toi_eVMmA.png"
data-width="875" data-height="238" />
</figure>

<figure id="59b1" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*i4jXew6t8EU9goWE.png"
class="graf-image" data-image-id="0*i4jXew6t8EU9goWE.png"
data-width="875" data-height="110" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#ac5a .graf .graf--h3 .graf-after--figure name="ac5a"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#eb1a .graf .graf--h3 .graf-after--p name="eb1a"}

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
.h-card} on [August 25, 2024](https://medium.com/p/fb8eeb9edbfa).

[Canonical
link](https://medium.com/@bevijaygupta/crack-the-hash-level-2-tryhackme-writeup-fb8eeb9edbfa){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
