---
title: "Hashing Crypto 101 TryHackme Writeup 41d0d32a7feb"
platform: Medium
original_file: 2024-08-29_Hashing-Crypto-101-TryHackme-Writeup-41d0d32a7feb.md
---

# Hashing Crypto 101 TryHackme Writeup 41d0d32a7feb

::: {}
# Hashing Crypto 101 TryHackme Writeup {#hashing-crypto-101-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/hashingcrypto101 Note: This room
is for Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#5289 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Hashing Crypto 101 TryHackme Writeup {#4ee6 .graf .graf--h3 .graf--leading .graf--title name="4ee6"}

<figure id="f577" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*bRR7Zo-7BawsJEHC.png"
class="graf-image" data-image-id="0*bRR7Zo-7BawsJEHC.png"
data-width="557" data-height="307" />
</figure>

**Room link:**
[https://tryhackme.com/room/hashingcrypto101](https://tryhackme.com/room/hashingcrypto101){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/hashingcrypto101"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Before we start, we need to get some jargon out of the way.\
Read these, and take in as much as you can. We'll expand on some of them
later in the room.

**Plaintext** --- Data before encryption or hashing, often text but not
always as it could be a photograph or other file instead.

**Encoding** --- This is NOT a form of encryption, just a form of data
representation like base64 or hexadecimal. Immediately reversible.

**Hash** --- A hash is the output of a hash function. Hashing can also
be used as a verb, "to hash", meaning to produce the hash value of some
data.

**Brute force** --- Attacking cryptography by trying every different
password or every different key

**Cryptanalysis** --- Attacking cryptography by finding a weakness in
the underlying maths

This room will likely involve some research. Get good at using search
engines, it's crucial to infosec.

Read the words, and understand the meanings!\
**Question 1**. Is base64 encryption or encoding?

> ***Answer: encoding***

### What's a hash function? {#3da4 .graf .graf--h3 .graf-after--blockquote name="3da4"}

Hash functions are quite different from encryption. There is no key, and
it's meant to be impossible (or very very difficult) to go from the
output back to the input.

A hash function takes some input data of any size, and creates a summary
or "digest" of that data. The output is a fixed size. It's hard to
predict what the output will be for any input and vice versa. Good
hashing algorithms will be (relatively) fast to compute, and slow to
reverse (Go from output and determine input). Any small change in the
input data (even a single bit) should cause a large change in the
output.

The output of a hash function is normally raw bytes, which are then
encoded. Common encodings for this are base 64 or hexadecimal. Decoding
these won't give you anything useful.

### Why should I care? {#b9b2 .graf .graf--h3 .graf-after--p name="b9b2"}

Hashing is used very often in cyber security. When you logged into
TryHackMe, that used hashing to verify your password. When you logged
into your computer, that also used hashing to verify your password. You
interact indirectly with hashing more than you would think, mostly in
the context of passwords.

### What's a hash collision? {#1611 .graf .graf--h3 .graf-after--p name="1611"}

A hash collision is when 2 different inputs give the same output. Hash
functions are designed to avoid this as best as they can, especially
being able to engineer (create intentionally) a collision. Due to the
pigeonhole effect, collisions are not avoidable. The pigeonhole effect
is basically, there are a set number of different output values for the
hash function, but you can give it any size input. As there are more
inputs than outputs, some of the inputs must give the same output. If
you have 128 pigeons and 96 pigeonholes, some of the pigeons are going
to have to share.

MD5 and SHA1 have been attacked, and made technically insecure due to
engineering hash collisions. However, no attack has yet given a
collision in both algorithms at the same time so if you use the MD5 hash
AND the SHA1 hash to compare, you will see they're different. The MD5
collision example is available from
[https://www.mscs.dal.ca/\~selinger/md5collision/](https://www.mscs.dal.ca/~selinger/md5collision/){.markup--anchor
.markup--p-anchor
data-href="https://www.mscs.dal.ca/~selinger/md5collision/"
rel="noopener ugc nofollow noopener" target="_blank"} and details of the
SHA1 Collision are available from
[https://shattered.io/](https://shattered.io/){.markup--anchor
.markup--p-anchor data-href="https://shattered.io/"
rel="noopener ugc nofollow noopener" target="_blank"}. Due to these, you
shouldn't trust either algorithm for hashing passwords or data.

**Question 2**. What is the output size in bytes of the MD5 hash
function?

MD5 processes a variable-length message into a fixed-length output of
128 bits.

128 bit= 16 bytes

> ***Answer: 16***

**Question 3**. Can you avoid hash collisions? (Yea/Nay)

> ***Answer: Nay***

**Question 4**. If you have an 8 bit hash output, how many possible
hashes are there?

> ***Answer: 256***

### What can we do with hashing? {#a5f3 .graf .graf--h3 .graf-after--blockquote name="a5f3"}

Hashing is used for 2 main purposes in Cyber Security. To verify
integrity of data (More on that later), or for verifying passwords.

### Hashing for password verification {#4c7e .graf .graf--h3 .graf-after--p name="4c7e"}

Most webapps need to verify a user's password at some point. Storing
these passwords in plain text would be bad. You've probably seen news
stories about companies that have had their database leaked. Knowing
some people, they use the same password for everything including their
banking, so leaking these would be really really bad.

Quite a few data breaches have leaked plaintext passwords. You're
probably familiar with "rockyou.txt" on Kali as a password word list.
This came from a company that made widgets for MySpace. They stored
their passwords in plaintext and the company had a data breach. The txt
file contains over 14 million passwords (although some are \*unlikely\*
to have been user passwords. Sort by length if you want to see what I
mean).

Adobe had a notable data breach that was slightly different. The
passwords were encrypted, rather than hashed and the encryption that was
used was not secure. This meant that the plaintext could be relatively
quickly retrieved. If you want to read more about this breach, this post
from Sophos is excellent:
[https://nakedsecurity.sophos.com/2013/11/04/anatomy-of-a-password-disaster-adobes-giant-sized-cryptographic-blunder/](https://nakedsecurity.sophos.com/2013/11/04/anatomy-of-a-password-disaster-adobes-giant-sized-cryptographic-blunder/){.markup--anchor
.markup--p-anchor
data-href="https://nakedsecurity.sophos.com/2013/11/04/anatomy-of-a-password-disaster-adobes-giant-sized-cryptographic-blunder/"
rel="noopener ugc nofollow noopener" target="_blank"}

Linkedin also had a data breach. Linkedin used SHA1 for password
verification, which is quite quick to compute using GPUs.

You can't encrypt the passwords, as the key has to be stored somewhere.
If someone gets the key, they can just decrypt the passwords.

This is where hashing comes in. What if, instead of storing the
password, you just stored the hash of the password? This means you never
have to store the user's password, and if your database was leaked then
an attacker would have to crack each password to find out what the
password was. That sounds fairly useful.

There's just one problem with this. What if two users have the same
password? As a hash function will always turn the same input into the
same output, you will store the same password hash for each user. That
means if someone cracks that hash, they get into more than one account.
It also means that someone can create a "Rainbow table" to break the
hashes.

A rainbow table is a lookup table of hashes to plaintexts, so you can
quickly find out what password a user had just from the hash. A rainbow
table trades time taken to crack a hash for hard disk space, but they do
take time to create.\
Here's a quick example so you can try and understand what they're like.

<figure id="0856" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DWlJGIfrBOdAO78e.png"
class="graf-image" data-image-id="0*DWlJGIfrBOdAO78e.png"
data-width="811" data-height="496" />
</figure>

[https://tryhackme.com/room/hashingcrypto101](https://tryhackme.com/room/hashingcrypto101){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/hashingcrypto101"
rel="noopener ugc nofollow noopener" target="_blank"}

Websites like
[**Crackstation**](http://crackstation.net/){.markup--anchor
.markup--p-anchor data-href="http://crackstation.net/"
rel="noopener ugc nofollow noopener" target="_blank"} internally use
HUGE rainbow tables to provide fast password cracking for hashes without
salts. Doing a lookup in a sorted list of hashes is really quite fast,
much much faster than trying to crack the hash.

### Protecting against rainbow tables {#1f8e .graf .graf--h3 .graf-after--p name="1f8e"}

To protect against rainbow tables, we add a salt to the passwords. The
salt is randomly generated and stored in the database, unique to each
user. In theory, you could use the same salt for all users but that
means that duplicate passwords would still have the same hash, and a
rainbow table could still be created specific passwords with that salt.

The salt is added to either the start or the end of the password before
it's hashed, and this means that every user will have a different
password hash even if they have the same password. Hash functions like
bcrypt and sha512crypt handle this automatically. Salts don't need to be
kept private.

**Question 1**. Crack the hash "d0199f51d2728db6011945145a1b607a" using
the rainbow table manually.

You can use this
[***website***](https://hashes.com/en/decrypt/hash){.markup--anchor
.markup--p-anchor data-href="https://hashes.com/en/decrypt/hash"
rel="noopener ugc nofollow noopener" target="_blank"} to crack this hash
value

> ***Answer: basketball***

**Question 2.** Crack the hash "5b31f93c09ad1d065c0491b764d04933" using
online tools

You can use this
[***website***](https://hashes.com/en/decrypt/hash){.markup--anchor
.markup--p-anchor data-href="https://hashes.com/en/decrypt/hash"
rel="noopener ugc nofollow noopener" target="_blank"} to crack this hash
value.

> ***Answer: tryhackme***

**Question 3.** Should you encrypt passwords? Yea/Nay

> ***Answer: Nay***

### Recognising password hashes {#95b7 .graf .graf--h3 .graf-after--blockquote name="95b7"}

Automated hash recognition tools such as
[https://pypi.org/project/hashID/](https://pypi.org/project/hashID/){.markup--anchor
.markup--p-anchor data-href="https://pypi.org/project/hashID/"
rel="noopener ugc nofollow noopener" target="_blank"} exist, but they
are unreliable for many formats. For hashes that have a prefix, the
tools are reliable. Use a healthy combination of context and tools. If
you found the hash in a web application database, it's more likely to be
md5 than NTLM. Automated hash recognition tools often get these hash
types mixed up, which highlights the importance of learning yourself.

Unix style password hashes are very easy to recognise, as they have a
prefix. The prefix tells you the hashing algorithm used to generate the
hash. The standard format is **\$format\$rounds\$salt\$hash**.

Windows passwords are hashed using NTLM, which is a variant of md4.
They're visually identical to md4 and md5 hashes, so it's very important
to use context to work out the hash type.

On Linux, password hashes are stored in /etc/shadow. This file is
normally only readable by root. They used to be stored in /etc/passwd,
and were readable by everyone.

On Windows, password hashes are stored in the SAM. Windows tries to
prevent normal users from dumping them, but tools like mimikatz exist
for this. Importantly, the hashes found there are split into NT hashes
and LM hashes.

Here's a quick table of the most Unix style password prefixes that
you'll see.

<figure id="8732" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7FE0MEOlsVNRVXnN.png"
class="graf-image" data-image-id="0*7FE0MEOlsVNRVXnN.png"
data-width="875" data-height="188" />
</figure>

A great place to find more hash formats and password prefixes is the
hashcat example page, available here:
[https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"}.\
For other hash types, you'll normally need to go by length, encoding or
some research into the application that generated them. Never
underestimate the power of research.

**Question 1**. How many rounds does sha512crypt (\$6\$) use by default?

You can read this
[***website***](https://blog.michael.franzl.name/2016/09/09/hashing-passwords-sha512-stronger-than-bcrypt-rounds/){.markup--anchor
.markup--p-anchor
data-href="https://blog.michael.franzl.name/2016/09/09/hashing-passwords-sha512-stronger-than-bcrypt-rounds/"
rel="noopener ugc nofollow noopener" target="_blank"} for this question

<figure id="b2ff" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0GAD1R3pwtPWKNTB.png"
class="graf-image" data-image-id="0*0GAD1R3pwtPWKNTB.png"
data-width="628" data-height="314" />
</figure>

> ***Answer: 5000***

**Question 2.** What's the hashcat example hash (from the website) for
Citrix Netscaler hashes?

You can find the answer in this
[***website***](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"}.

<figure id="b09c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*g-NgyuNTkab8Sn_0.png"
class="graf-image" data-image-id="0*g-NgyuNTkab8Sn_0.png"
data-width="875" data-height="127" />
</figure>

> ***Answer: 1765058016a22f1b4e076dccd1c3df4e8e5c0839ccded98ea***

**Question 3.** How long is a Windows NTLM hash, in characters?

<figure id="fe4f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ED2DWuEoikCzU0g2.png"
class="graf-image" data-image-id="0*ED2DWuEoikCzU0g2.png"
data-width="653" data-height="86" />
</figure>

You can find the answer in this
[***website***](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"}.

> ***Answer: 32***

### Password Cracking {#79ee .graf .graf--h3 .graf-after--blockquote name="79ee"}

We've already mentioned rainbow tables as a method to crack hashes that
don't have a salt, but what if there's a salt involved?

You can't "decrypt" password hashes. They're not encrypted. You have to
crack the hashes by hashing a large number of different inputs (often
rockyou, these are the possible passwords), potentially adding the salt
if there is one and comparing it to the target hash. Once it matches,
you know what the password was. Tools like Hashcat and John the Ripper
are normally used for this.

### Why crack on GPUs? {#f9f9 .graf .graf--h3 .graf-after--p name="f9f9"}

Graphics cards have thousands of cores. Although they can't do the same
sort of work that a CPU can, they are very good at some of the maths
involved in hash functions. This means you can use a graphics card to
crack most hash types much more quickly. Some hashing algorithms,
notably bcrypt, are designed so that hashing on a GPU is about the same
speed as hashing on a CPU which helps them resist cracking.

### Cracking on VMs? {#18cb .graf .graf--h3 .graf-after--p name="18cb"}

It's worth mentioning that virtual machines normally don't have access
to the host's graphics card(s) (You can set this up, but it's a lot of
work). If you want to run hashcat, it's best to run it on your host
(Windows builds are available on the website, run it from powershell).
You can get Hashcat working with OpenCL in a VM, but the speeds will
likely be much worse than cracking on your host. John the ripper uses
CPU by default and as such, works in a VM out of the box although you
may get better speeds running it on the host OS as it will have more
threads and no overhead from running in a VM.

**NEVER (I repeat, NEVER!) use --- force for hashcat**. It can lead to
false positives (wrong passwords being given to you) and false negatives
(skips over the correct hash).

UPDATE: As of Kali 2020.2, hashcat 6.0 will run on the CPU
without --- force. I still recommend cracking on your host OS if you
have a GPU, as it will be much much faster.

### Time to get cracking! {#f85e .graf .graf--h3 .graf-after--p name="f85e"}

I'll provide the hashes. Crack them. You can choose how. You'll need to
use online tools, Hashcat, and/or John the Ripper. Remember the
restrictions on online rainbow tables. Don't be afraid to use the hints.
Rockyou or online tools should be enough to find all of these.

**Question 1**. Crack this hash:
\$2a\$06\$7yoU3Ng8dHTXphAg913cyO6Bjs3K5lBnwq5FJyA6d01pMSrddr1ZG

<figure id="2daa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rXFwsj8zlEzXCecy.png"
class="graf-image" data-image-id="0*rXFwsj8zlEzXCecy.png"
data-width="792" data-height="58" />
</figure>

Then, I analyzed this hash value.

<figure id="9713" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aOM2WDas8b5w4avk.png"
class="graf-image" data-image-id="0*aOM2WDas8b5w4avk.png"
data-width="713" data-height="566" />
</figure>

[https://www.tunnelsup.com/hash-analyzer/](https://www.tunnelsup.com/hash-analyzer/){.markup--anchor
.markup--p-anchor data-href="https://www.tunnelsup.com/hash-analyzer/"
rel="noopener ugc nofollow noopener" target="_blank"}

Then I used "hashcat" in Kali Linux.

In hashcat tool, bcrypt hash code is 3200. You can see this hash code
with "hashcat --help" command.

<figure id="70dd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tqDSiiyxAOk4FMSs.png"
class="graf-image" data-image-id="0*tqDSiiyxAOk4FMSs.png"
data-width="500" data-height="82" />
</figure>

Then I used this command and "rockyou.txt" file for worldlist.

<figure id="d160" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zxt1gMdSUjGTmdoQ.png"
class="graf-image" data-image-id="0*zxt1gMdSUjGTmdoQ.png"
data-width="703" data-height="184" />
</figure>

<figure id="459f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*HPFv8UpLXrprjiOZ.png"
class="graf-image" data-image-id="0*HPFv8UpLXrprjiOZ.png"
data-width="751" data-height="269" />
</figure>

> ***Answer: 85208520***

**Question 2**. Crack this hash:
9eb7ee7f551d2f0ac684981bd1f1e2fa4a37590199636753efe614d4db30e8e1

<figure id="41f1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Dw9i5amijO9HG2ZE.png"
class="graf-image" data-image-id="0*Dw9i5amijO9HG2ZE.png"
data-width="715" data-height="492" />
</figure>

<figure id="627c" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ioc7rhng5wUrYIY4.png"
class="graf-image" data-image-id="0*ioc7rhng5wUrYIY4.png"
data-width="672" data-height="234" />
</figure>

<figure id="e949" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ybjJU_xWpssVAyS5.png"
class="graf-image" data-image-id="0*ybjJU_xWpssVAyS5.png"
data-width="793" data-height="233" />
</figure>

> ***Answer: halloween***

**Question 3.** Crack this hash:
\$6\$GQXVvW4EuM\$ehD6jWiMsfNorxy5SINsgdlxmAEl3.yif0/c3NqzGLa0P.S7KRDYjycw5bnYkF5ZtB8wQy8KnskuWQS3Yr1wQ0

same method

> ***Answer: spaceman***

**Question 4.** Bored of this yet? Crack this hash:
b6b0d451bbf6fed658659a9e7e5598fe

You can use this
[***website***](https://hashes.com/en/decrypt/hash){.markup--anchor
.markup--p-anchor data-href="https://hashes.com/en/decrypt/hash"
rel="noopener ugc nofollow noopener" target="_blank"} to crack this hash
value.

> ***Answer: funforyou***

### Hashing for integrity checking {#bff5 .graf .graf--h3 .graf-after--blockquote name="bff5"}

### Integrity Checking {#2ca7 .graf .graf--h3 .graf-after--h3 name="2ca7"}

Hashing can be used to check that files haven't been changed. If you put
the same data in, you always get the same data out. If even a single bit
changes, the hash will change a lot. This means you can use it to check
that files haven't been modified or to make sure that they have
downloaded correctly. You can also use hashing to find duplicate files,
if two pictures have the same hash then they are the same picture.

### HMACs {#9bb4 .graf .graf--h3 .graf-after--p name="9bb4"}

HMAC is a method of using a cryptographic hashing function to verify the
authenticity and integrity of data. The TryHackMe VPN uses HMAC-SHA512
for message authentication, which you can see in the terminal output. A
HMAC can be used to ensure that the person who created the HMAC is who
they say they are (authenticity), and that the message hasn't been
modified or corrupted (integrity). They use a secret key, and a hashing
algorithm in order to produce a hash.

What's the SHA1 sum for the amd64 Kali 2019.4 ISO?
[http://old.kali.org/kali-images/kali-2019.4/](http://old.kali.org/kali-images/kali-2019.4/){.markup--anchor
.markup--p-anchor
data-href="http://old.kali.org/kali-images/kali-2019.4/"
rel="noopener ugc nofollow noopener" target="_blank"}

[http://old.kali.org/kali-images/kali-2019.4/SHA1SUMS](http://old.kali.org/kali-images/kali-2019.4/SHA1SUMS){.markup--anchor
.markup--p-anchor
data-href="http://old.kali.org/kali-images/kali-2019.4/SHA1SUMS"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="c800" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2SQdlYVKNuOf925C.png"
class="graf-image" data-image-id="0*2SQdlYVKNuOf925C.png"
data-width="875" data-height="248" />
</figure>

[http://old.kali.org/kali-images/kali-2019.4/SHA1SUMS](http://old.kali.org/kali-images/kali-2019.4/SHA1SUMS){.markup--anchor
.markup--p-anchor
data-href="http://old.kali.org/kali-images/kali-2019.4/SHA1SUMS"
rel="noopener ugc nofollow noopener" target="_blank"}

OR

After download kali linux

<figure id="791c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*E4DVpnGLAafHJFso.png"
class="graf-image" data-image-id="0*E4DVpnGLAafHJFso.png"
data-width="684" data-height="52" />
</figure>

> ***Answer: 186c5227e24ceb60deb711f1bdc34ad9f4718ff9***

What's the hashcat mode number for HMAC-SHA512 (key = \$pass)?

You can see this code in this
[***website***](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"}.

<figure id="f94f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Al107uxJBHBddi4f.png"
class="graf-image" data-image-id="0*Al107uxJBHBddi4f.png"
data-width="875" data-height="50" />
</figure>

[https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"}

OR

<figure id="4f2d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HCvaYtNk0gy0ZGpe.png"
class="graf-image" data-image-id="0*HCvaYtNk0gy0ZGpe.png"
data-width="562" data-height="120" />
</figure>

> ***Answer: 1750***

### Promote and Collaborate on Cybersecurity Insights {#6f24 .graf .graf--h3 .graf-after--blockquote name="6f24"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#96f4 .graf .graf--h3 .graf-after--p name="96f4"}

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
.h-card} on [August 29, 2024](https://medium.com/p/41d0d32a7feb).

[Canonical
link](https://medium.com/@bevijaygupta/hashing-crypto-101-tryhackme-writeup-41d0d32a7feb){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
