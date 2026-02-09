::: {}
# John The Ripper TryHackme Writeup {#john-the-ripper-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/johntheripper0
:::

::::::: {.section .e-content field="body"}
:::::: {#10a4 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### John The Ripper TryHackme Writeup {#5882 .graf .graf--h3 .graf--leading .graf--title name="5882"}

<figure id="d54f" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*TFf3eBAWGsEcZ137.png"
class="graf-image" data-image-id="0*TFf3eBAWGsEcZ137.png"
data-width="875" data-height="231" data-is-featured="true" />
</figure>

[https://tryhackme.com/room/johntheripper0](https://tryhackme.com/room/johntheripper0){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/johntheripper0"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 2: Setting up John the Ripper {#dc07 .graf .graf--h3 .graf-after--p name="dc07"}

Question: What is the most popular extended version of John the Ripper?

> ***Answer****: Jumbo John*

### Task 3: Wordlists {#b99a .graf .graf--h3 .graf-after--blockquote name="b99a"}

Question: What website was the rockyou.txt wordlist created from a
breach on?

> ***Answer:*** *rockyou.com*

### Task 4: Cracking Basic Hashes {#1f0b .graf .graf--h3 .graf-after--blockquote name="1f0b"}

Tool we use
[hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master){.markup--anchor
.markup--p-anchor
data-href="https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master"
rel="noopener ugc nofollow noopener" target="_blank"}. This tool is
already install in kali linux

``` {#2c10 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
python3 hash-identifier.py
```

for the Practical we need to download "firsttaskhashes.zip"

So Here we unzip the file

<figure id="85e4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bxwGq-n6lFrX30Zd.png"
class="graf-image" data-image-id="0*bxwGq-n6lFrX30Zd.png"
data-width="527" data-height="459" />
</figure>

**Question:** What type of hash is hash1.txt?

copy hash from hash1.txt

<figure id="bf23" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dEf8G4rwilQm6Kw4.png"
class="graf-image" data-image-id="0*dEf8G4rwilQm6Kw4.png"
data-width="518" data-height="75" />
</figure>

Use
[Hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master){.markup--anchor
.markup--p-anchor
data-href="https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master"
rel="noopener ugc nofollow noopener" target="_blank"} tool to analyze
hash format

<figure id="358c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YH0yEBSsDIpWLH8L.png"
class="graf-image" data-image-id="0*YH0yEBSsDIpWLH8L.png"
data-width="794" data-height="382" />
</figure>

Hash identifier show us it is possible **MD5** hash format

**Answer: MD5**

Question 2: What is the cracked value of hash1.txt?

<figure id="3d50" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*khOEpeLImvdG1CpK.png"
class="graf-image" data-image-id="0*khOEpeLImvdG1CpK.png"
data-width="609" data-height="206" />
</figure>

> ***Answer: biscuit***

Question 3: What type of hash is hash2.txt?

Repeat the process for hash2.txt

<figure id="b022" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8622OQGdCa86Fg4R.png"
class="graf-image" data-image-id="0*8622OQGdCa86Fg4R.png"
data-width="785" data-height="456" />
</figure>

Possible hash found SHA-1 or SHA1

> ***Answer: SHA1***

Question: What is the cracked value of hash2.txt

<figure id="9209" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*X3xdEj6B0S77j2Vn.png"
class="graf-image" data-image-id="0*X3xdEj6B0S77j2Vn.png"
data-width="628" data-height="206" />
</figure>

> ***Answer****:* ***kangeroo***

Question: What type of hash is hash3.txt?

<figure id="627c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4FqWtvjzMiMhMTkx.png"
class="graf-image" data-image-id="0*4FqWtvjzMiMhMTkx.png"
data-width="857" data-height="459" />
</figure>

Possible Hash found SHA-256 or SHA256 or Haval256.

> ***Answer: SHA256***

Question: What is the cracked value of hash3.txt?

<figure id="856c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-Ad63nbxWPda5JIL.png"
class="graf-image" data-image-id="0*-Ad63nbxWPda5JIL.png"
data-width="639" data-height="222" />
</figure>

> ***Answer: microphone***

Question: What type of hash is hash4.txt?

<figure id="c823" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZAOa_-sdj0vIhw_4.png"
class="graf-image" data-image-id="0*ZAOa_-sdj0vIhw_4.png"
data-width="875" data-height="295" />
</figure>

Possible Hash found SHA-512 or SHA512 or **Whirlpool**

> ***Answer: Whirlpool***

Question: What is the cracked value of hash4.txt

<figure id="9913" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*79FTWqh-34cqukZ4.png"
class="graf-image" data-image-id="0*79FTWqh-34cqukZ4.png"
data-width="643" data-height="231" />
</figure>

> ***Answer: colossal***

### Task 5: Cracking Windows Authentication Hashes {#34d3 .graf .graf--h3 .graf-after--blockquote name="34d3"}

This section is about cracking Windows hashes and **NTHash / NTLM**

Question: What do we need to set the "format" flag to, in order to crack
this?'

> ***Answer: NT***

Question: What is the cracked value of this password?

Download the file from the section and here we use **format=nt**

<figure id="361f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bzDMIXJ7nVV25rZv.png"
class="graf-image" data-image-id="0*bzDMIXJ7nVV25rZv.png"
data-width="550" data-height="208" />
</figure>

> ***Answer: mushroom***

### Task 6: Cracking /etc/shadow Hashes {#6b23 .graf .graf--h3 .graf-after--blockquote name="6b23"}

This section is about cracking /etc/shadow or Linux user password hashes

Question: What is the root password?

We Use format=sha512crypt Because sha512crypt hash started from \$6\$

We can check by using "hashcat --- help"

<figure id="f303" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oz-zZjyw85f7dzMH.png"
class="graf-image" data-image-id="0*oz-zZjyw85f7dzMH.png"
data-width="551" data-height="189" />
</figure>

<figure id="34d5" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*4d3JBEdwiTFuVQ2z.png"
class="graf-image" data-image-id="0*4d3JBEdwiTFuVQ2z.png"
data-width="680" data-height="225" />
</figure>

> ***Answer: 1234***

### Task 7: Single Crack Mode {#8dc3 .graf .graf--h3 .graf-after--blockquote name="8dc3"}

So In this mode we don't need a wordlist , but need to put the flag "-
-single", " --- format

Question: What is Joker's password?

Download the file from this section and find hash format

<figure id="bf92" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oSFj5qyxczSnUSON.png"
class="graf-image" data-image-id="0*oSFj5qyxczSnUSON.png"
data-width="792" data-height="456" />
</figure>

Possible hash found MD5, now add the jocker word before the hash

<figure id="4732" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vqvGM1GJdc6bvNuC.png"
class="graf-image" data-image-id="0*vqvGM1GJdc6bvNuC.png"
data-width="613" data-height="398" />
</figure>

> ***Answer: Jok3r***

### Task 8: Custom Rules {#c997 .graf .graf--h3 .graf-after--blockquote name="c997"}

In this section we learn about custom rules for John.Jumbo John already
comes with a large list of custom rules, which contain modifiers for use
almost all cases. If you get stuck, try looking at those rules \[around
line 678\] if your syntax isn't working properly.

The way we use custom rules in john are like this:

john --- wordlist=\[path to wordlist\] --- rule=PoloPassword \[path to
file\]

Question 1 : What do custom rules allow us to exploit?

> ***Answer: Password complexity predictability***

Question 2: What rule would we use to add all capital letters to the end
of the word?

**Hint:**
[https://www.openwall.com/john/doc/RULES.shtml](https://www.openwall.com/john/doc/RULES.shtml){.markup--anchor
.markup--p-anchor
data-href="https://www.openwall.com/john/doc/RULES.shtml"
rel="noopener ugc nofollow noopener" target="_blank"}

**Note:** Do note copy paste this answer write yourself

> ***Answer:*** *Az"\[A-Z\]"*

Question3: What flag would we use to call a custom rule called
"THMRules"

> ***Answer: --- -rule=THMRules***

### Task 9: Cracking Password Protected Zip File {#d4a4 .graf .graf--h3 .graf-after--blockquote name="d4a4"}

In this section we learn about how to crack password protected Zip file.

For this task we use zip2john tool if you have already install john. Or
you can locate where it is located and copy zip2john to your folder.

<figure id="e3e7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hIoIvf1YuGGGnFae.png"
class="graf-image" data-image-id="0*hIoIvf1YuGGGnFae.png"
data-width="373" data-height="145" />
</figure>

Question: What is the password for the secure.zip file?

First we need to Extract the hash from the file secure.zip to a
secure.txt file. So we need to run zip2john. Now the hash is in
secure.txt

<figure id="7766" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*j7VLbvQXoYmpE7hU.png"
class="graf-image" data-image-id="0*j7VLbvQXoYmpE7hU.png"
data-width="529" data-height="81" />
</figure>

To crack the hash we use wordlists rockyou.

<figure id="8ce4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kCGKhkaTtWwx_74Z.png"
class="graf-image" data-image-id="0*kCGKhkaTtWwx_74Z.png"
data-width="551" data-height="208" />
</figure>

So this is the password for secure.zip

> ***Answer: pass123***

Question 2: What is the contents of the flag inside the zip file?

Now unzip the file secure.zip it ask for password. Then Use pass123

<figure id="f67d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YUveWBUzjvOh9ZI7.png"
class="graf-image" data-image-id="0*YUveWBUzjvOh9ZI7.png"
data-width="445" data-height="249" />
</figure>

### Task 10: Cracking Password Protected RAR File {#4dd6 .graf .graf--h3 .graf-after--figure name="4dd6"}

In this section we learn about how to crack password protected RARfile.

For this task we use rar2john tool if you have already install john. Or
you can locate where it is located and copy rar2john to your folder.

Question 1: What is the password for the secure.rar file?

First we need to Extract the hash from the file secure.rar to a
secure.txt file. So we need to run rar2john. Now the hash is in
secure.txt

<figure id="5c63" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5ZwosisndD8t3dx5.png"
class="graf-image" data-image-id="0*5ZwosisndD8t3dx5.png"
data-width="812" data-height="287" />
</figure>

This is the password for secure.rar. Now Extract the file from
secure.rar .For this use unrar e secure.rar.If it is ask for password
use "password"

> ***Answer: password***

<figure id="f6d6" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*xP3JmSRyVA9aAHbj.png"
class="graf-image" data-image-id="0*xP3JmSRyVA9aAHbj.png"
data-width="683" data-height="326" />
</figure>

### Task 10: Cracking SSH Keys with John {#aae7 .graf .graf--h3 .graf-after--figure name="aae7"}

This section is about cracking SSH keys with John. For this first we use
ssh2john to extract hash from id_rsa file.

``` {#4ce7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
locate ssh2john
```

<figure id="84fb" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*-aT25TWr-6_WlXsg.png"
class="graf-image" data-image-id="0*-aT25TWr-6_WlXsg.png"
data-width="479" data-height="195" />
</figure>

Question 1: What is the SSH private key password?

<figure id="2982" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VF3WG5vNutLNbGoM.png"
class="graf-image" data-image-id="0*VF3WG5vNutLNbGoM.png"
data-width="720" data-height="287" />
</figure>

> ***Answer: mango***

### Promote and Collaborate on Cybersecurity Insights {#ffdc .graf .graf--h3 .graf-after--blockquote name="ffdc"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#47a8 .graf .graf--h3 .graf-after--p name="47a8"}

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
.h-card} on [September 7, 2024](https://medium.com/p/e7d0ac9f965b).

[Canonical
link](https://medium.com/@bevijaygupta/john-the-ripper-tryhackme-writeup-e7d0ac9f965b){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
