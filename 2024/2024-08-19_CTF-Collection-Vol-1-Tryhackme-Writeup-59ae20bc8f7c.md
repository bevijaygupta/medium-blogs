---
title: "CTF Collection Vol 1 Tryhackme Writeup 59ae20bc8f7c"
platform: Medium
original_file: 2024-08-19_CTF-Collection-Vol-1-Tryhackme-Writeup-59ae20bc8f7c.md
---

# CTF Collection Vol 1 Tryhackme Writeup 59ae20bc8f7c

::: {}
# CTF Collection Vol.1 Tryhackme Writeup {#ctf-collection-vol.1-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "CTF Collection Vol.1"
:::

::::::: {.section .e-content field="body"}
:::::: {#06ee .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### CTF Collection Vol.1 Tryhackme Writeup {#8dd0 .graf .graf--h3 .graf--leading .graf--title name="8dd0"}

**This is a Writeup of Tryhackme room "CTF Collection Vol.1"**

<figure id="6b3e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CQSSZce5Z3DxSy8s.png"
class="graf-image" data-image-id="0*CQSSZce5Z3DxSy8s.png"
data-width="477" data-height="274" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/ctfcollectionvol1](https://tryhackme.com/room/ctfcollectionvol1){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/ctfcollectionvol1"
rel="noopener ugc nofollow noopener noopener" target="_blank"}\
**Note: This room is Free**

**Difficulty: Easy**

### Task 2: What does the base said? {#679e .graf .graf--h3 .graf-after--p name="679e"}

Can you decode the following?

VEhNe2p1NTdfZDNjMGQzXzdoM19iNDUzfQ==

<figure id="5ff9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KJT7_XOLrklhoNKe.png"
class="graf-image" data-image-id="0*KJT7_XOLrklhoNKe.png"
data-width="619" data-height="73" />
</figure>

### Task 3: Meta meta {#8ff1 .graf .graf--h3 .graf-after--figure name="8ff1"}

<figure id="0339" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*7QoT59nz1yV8kzpV.png"
class="graf-image" data-image-id="0*7QoT59nz1yV8kzpV.png"
data-width="710" data-height="592" />
</figure>

### Task 4: Mon, are we going to be okay? {#f982 .graf .graf--h3 .graf-after--figure name="f982"}

<figure id="7665" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*iVIyqZgtSp6qKIED.png"
class="graf-image" data-image-id="0*iVIyqZgtSp6qKIED.png"
data-width="459" data-height="284" />
</figure>

### Task 5: Erm......Magick {#3c2c .graf .graf--h3 .graf-after--figure name="3c2c"}

<figure id="59d1" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*3WWWdrs_f-tSCBP6.png"
class="graf-image" data-image-id="0*3WWWdrs_f-tSCBP6.png"
data-width="433" data-height="226" />
</figure>

### Task 6: QRrrrr {#4e60 .graf .graf--h3 .graf-after--figure name="4e60"}

<figure id="445d" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*Qs_v-39znJLNryhn.png"
class="graf-image" data-image-id="0*Qs_v-39znJLNryhn.png"
data-width="807" data-height="519" />
</figure>

[https://zxing.org/](https://zxing.org/){.markup--anchor
.markup--p-anchor data-href="https://zxing.org/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="0ab0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*F_aueLlgcAA9u3TH.png"
class="graf-image" data-image-id="0*F_aueLlgcAA9u3TH.png"
data-width="707" data-height="354" />
</figure>

[https://zxing.org/](https://zxing.org/){.markup--anchor
.markup--p-anchor data-href="https://zxing.org/"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 7 :Reverse it or read it? {#bc65 .graf .graf--h3 .graf-after--p name="bc65"}

You are required to download an ELF executable (a linux version of a
windows .exe executable). This file is a binary file so I tried strings
command once again to extract the printable characters and I found the
flag

<figure id="4750" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_6BeMQJ5vLnSoMBO.png"
class="graf-image" data-image-id="0*_6BeMQJ5vLnSoMBO.png"
data-width="375" data-height="86" />
</figure>

### Task 8 :Another decoding stuff {#c7cc .graf .graf--h3 .graf-after--figure name="c7cc"}

Can you decode it?

3agrSy1CewF9v8ukcSkPSYm3oKUoByUpKG4L

I was a bit confused at first. I took a look at the hints its has being
stated "base58". I found out that base58 is used to represent large
integers as normal text. I used a online base58 decoder and retrived the
flag

``` {#d168 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
apt install base58
```

<figure id="ea3d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*8FRSZ0fA7YkoSelQ.png"
class="graf-image" data-image-id="0*8FRSZ0fA7YkoSelQ.png"
data-width="616" data-height="87" />
</figure>

### Task 9 :Left or right {#9260 .graf .graf--h3 .graf-after--figure name="9260"}

Left, right, left, right... Rot 13 is too mainstream. Solve this

MAF{atbe_max_vtxltk}

Rot 13 is a encryption scheme used to encrypt infomation. How it
works ? . It takes a single character and shift 13 places in the
alphabet. Rot 13 is also a subset of Caesar cipher. I tried Rot13 it
didn't work and then I started bruteforcing charcter shifts and on the
19th shift I got it.

<figure id="20ac" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oWl2YH2Jjo2vwVoS.png"
class="graf-image" data-image-id="0*oWl2YH2Jjo2vwVoS.png"
data-width="875" data-height="256" />
</figure>

[https://cryptii.com/pipes/rot13-decoder](https://cryptii.com/pipes/rot13-decoder){.markup--anchor
.markup--p-anchor data-href="https://cryptii.com/pipes/rot13-decoder"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 10 :Make a comment {#68a6 .graf .graf--h3 .graf-after--p name="68a6"}

The hint is given the in the title of the question itself. If you
inspect the page with the dev tools you can veiw it between the tags.

<figure id="26e6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hIbc5ZJrsbdy5mOW.png"
class="graf-image" data-image-id="0*hIbc5ZJrsbdy5mOW.png"
data-width="677" data-height="303" />
</figure>

### Task 11 :Can you fix it? {#f644 .graf .graf--h3 .graf-after--figure name="f644"}

There is a courpted png file that you need to download. I got the hex
dump of the courpted png image with the xxd command

<figure id="a19e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DdKYqn7oLPhiumJX.png"
class="graf-image" data-image-id="0*DdKYqn7oLPhiumJX.png"
data-width="710" data-height="263" />
</figure>

Image is corrupted because it is missing the PNG header (**89 50 4E
47**):

A magic number is a number embedded at or near the beginning of a file
that indicates its file format. So let's replace the magic number with
the correct magic number of an png image. I googled it and found out
that

You can fix it as follows:

``` {#4305 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
printf '\x89\x50\x4E\x47' | dd of=spoil.png bs=4 conv=notrunc
```

<figure id="2e58" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ql8_dWjfOiYTMPIT.png"
class="graf-image" data-image-id="0*ql8_dWjfOiYTMPIT.png"
data-width="727" data-height="381" />
</figure>

<figure id="d9dd" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*2WMHhbDQ4ZN0mOaf.png"
class="graf-image" data-image-id="0*2WMHhbDQ4ZN0mOaf.png"
data-width="812" data-height="812" />
</figure>

### \[ Task 12 \] Read it {#2f56 .graf .graf--h3 .graf-after--figure name="2f56"}

Some hidden flag inside Tryhackme social account.

If you take a look at the hints it says

<figure id="8bd0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2sKm88mbwFDrzX00.png"
class="graf-image" data-image-id="0*2sKm88mbwFDrzX00.png"
data-width="494" data-height="187" />
</figure>

I did a google search and found a post thats interesting

<figure id="55c3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*82VPVhHL6ieMPwHG.png"
class="graf-image" data-image-id="0*82VPVhHL6ieMPwHG.png"
data-width="745" data-height="373" />
</figure>

### Task 13 :Spin my head {#f269 .graf .graf--h3 .graf-after--figure name="f269"}

What is this?

``` {#ad16 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++++. — — — — — — .+++++.>+++++++++++++++++++++++.<<++++++++++++++++++.>> — — — — — — — — — -. — — — — -.++++++++++++++.++++++++++++.<++++++++++++++++++.+++++++++.<+++.+.> — — .>++++.
```

This code is a programming language called "brainfuck" that's not so
popular or used. You can find an online decoder/interpreter online

<figure id="a532" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FTXm585UGVNtxLbp.png"
class="graf-image" data-image-id="0*FTXm585UGVNtxLbp.png"
data-width="875" data-height="393" />
</figure>

[https://sange.fi/esoteric/brainfuck/impl/interp/i.html](https://sange.fi/esoteric/brainfuck/impl/interp/i.html){.markup--anchor
.markup--p-anchor
data-href="https://sange.fi/esoteric/brainfuck/impl/interp/i.html"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 14 :An exclusive! {#06f6 .graf .graf--h3 .graf-after--p name="06f6"}

Exclusive strings for everyone!

S1: 44585d6b2368737c65252166234f20626d\
S2: 1010101010101010101010101010101010

In this challenge you have to do a XOR operation against the tow values
(S1 XOR S2). I found a site online which helps me to do this easily.

<figure id="0fe3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*orlrDWhizXFyaEgD.png"
class="graf-image" data-image-id="0*orlrDWhizXFyaEgD.png"
data-width="732" data-height="245" />
</figure>

### Task 15: Binary walk {#9fd0 .graf .graf--h3 .graf-after--figure name="9fd0"}

In this challenge you must download a jpg file. There is a tool called
"binwalk" that helps you to see if there are any hidden files inside the
specified file. (-e = extract)

<figure id="1df5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CLvxsr0-Eh8cgTEZ.png"
class="graf-image" data-image-id="0*CLvxsr0-Eh8cgTEZ.png"
data-width="625" data-height="531" />
</figure>

Binwalk creates a directory to store all the extracted files that it has
found. You can find your flag in this directory.

### Task 16 :Darkness {#b827 .graf .graf--h3 .graf-after--p name="b827"}

Accorging to the hints you can use stegsolve to filter/isolate different
colors in an image. But in our case we can also view the image file and
find the flag but you should have a sharp vision to see it. Anyways you
can download stegsolve with these terminal commands

wget
[http://www.caesum.com/handbook/Stegsolve.jar](http://www.caesum.com/handbook/Stegsolve.jar){.markup--anchor
.markup--p-anchor
data-href="http://www.caesum.com/handbook/Stegsolve.jar"
rel="noopener ugc nofollow noopener" target="_blank"} -O stegsolve.jar\
chmod +x stegsolve.jar

Now let's veiw the image with stegsolve by opening the file and changing
the color filters

<figure id="35d4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tryvTm5Jf374JSzz.png"
class="graf-image" data-image-id="0*tryvTm5Jf374JSzz.png"
data-width="875" data-height="416" />
</figure>

<figure id="879c" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*joI29bk00vKUNdMU.png"
class="graf-image" data-image-id="0*joI29bk00vKUNdMU.png"
data-width="474" data-height="330" />
</figure>

<figure id="29ed" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*zPO1VbU3oHQL8tUH.png"
class="graf-image" data-image-id="0*zPO1VbU3oHQL8tUH.png"
data-width="514" data-height="348" />
</figure>

<figure id="8dc3" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*bSdCWyA-8D1APHgn.png"
class="graf-image" data-image-id="0*bSdCWyA-8D1APHgn.png"
data-width="875" data-height="361" />
</figure>

### Task 17 :A sounding QR {#badf .graf .graf--h3 .graf-after--figure name="badf"}

How good is your listening skill?

P/S: The flag formatted as THM{Listened Flag}, the flag should be in All
CAPS

In this challenge you should download a QR code. Decode the QR code will
give you a URL to a soundcloud audio clip.

Upload the QR code to
[**https://zxing.org/w/decode.jspx**](https://zxing.org/w/decode.jspx){.markup--anchor
.markup--p-anchor data-href="https://zxing.org/w/decode.jspx"
rel="noopener ugc nofollow noopener" target="_blank"}**.** It decodes
as:

<figure id="79ee" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CpTTUWo2pYixURBk.png"
class="graf-image" data-image-id="0*CpTTUWo2pYixURBk.png"
data-width="729" data-height="517" />
</figure>

[https://zxing.org/w/decode.jspx](https://zxing.org/w/decode.jspx){.markup--anchor
.markup--p-anchor data-href="https://zxing.org/w/decode.jspx"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="e88b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iaE5bAURh0KPMMK2.png"
class="graf-image" data-image-id="0*iaE5bAURh0KPMMK2.png"
data-width="875" data-height="377" />
</figure>

[https://zxing.org/w/decode](https://zxing.org/w/decode){.markup--anchor
.markup--p-anchor data-href="https://zxing.org/w/decode"
rel="noopener ugc nofollow noopener" target="_blank"}

If you hear the audio clip real slow you might get it a bit more clear
or you can capture the recoding and play it in slow motion

### Task 18 :Dig up the past {#0593 .graf .graf--h3 .graf-after--p name="0593"}

Sometimes we need a 'machine' to dig the past

Targetted website:
[https://www.embeddedhacker.com/](https://www.embeddedhacker.com/){.markup--anchor
.markup--p-anchor data-href="https://www.embeddedhacker.com/"
rel="noopener ugc nofollow noopener" target="_blank"}\
Targetted time: 2 January 2020

\[Q\] Sometimes we need a 'machine' to dig the past.\
I noticed the 2 words that gives a clue "machine" and "past". It's the
WayBack Machine. The wayback machine is simply a website that stores
snapshots of other websites, noting the date and time of each snapshot
that it captures.\
I searched for the target website (https://www.embeddedhacker.com/) on
wayback machine

<figure id="989b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*y064sch3xQFW3nby.png"
class="graf-image" data-image-id="0*y064sch3xQFW3nby.png"
data-width="805" data-height="147" />
</figure>

[https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/](https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/){.markup--anchor
.markup--p-anchor
data-href="https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

Note that there is a snap taken on 02 Jan 2020 at 13:12 pm

<figure id="e9c3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JRWtCWtKTzSoBEuw.png"
class="graf-image" data-image-id="0*JRWtCWtKTzSoBEuw.png"
data-width="283" data-height="223" />
</figure>

[https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/](https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/){.markup--anchor
.markup--p-anchor
data-href="https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

While scrolling down I found a post named THM Flag posted on Jan 02 2020

<figure id="a56c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NY5x-dYRUZ0HVdP_.png"
class="graf-image" data-image-id="0*NY5x-dYRUZ0HVdP_.png"
data-width="549" data-height="221" />
</figure>

[https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/](https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/){.markup--anchor
.markup--p-anchor
data-href="https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 19 :Uncrackable! {#bf31 .graf .graf--h3 .graf-after--p name="bf31"}

Can you solve the following? By the way, I lost the key. Sorry \>.\<

MYKAHODTQ{RVG_YVGGK_FAL_WXF}

Flag format: TRYHACKME{FLAG IN ALL CAP}

In this challenge there is a cipher to decrypt. At first I taught it was
a caesar cipher but in the end I realized that this a vigenere cipher
decryption challenge after seeing this.

TRYHACKME is acting as a constant string so we can use TRYHACKME as the
key.

<figure id="f0cd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5T2dVwZgIh0bnvAj.png"
class="graf-image" data-image-id="0*5T2dVwZgIh0bnvAj.png"
data-width="875" data-height="332" />
</figure>

It looks like we found another constant THMTHMTHM. Lets try it again
with this key.

<figure id="966e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2UsyU2LQd5yhrU0L.png"
class="graf-image" data-image-id="0*2UsyU2LQd5yhrU0L.png"
data-width="875" data-height="231" />
</figure>

### Task 20 :Small bases {#6d71 .graf .graf--h3 .graf-after--figure name="6d71"}

Decode the following text.

581695969015253365094191591547859387620042736036246486373595515576333693

You take a look at the hints

<figure id="ad7a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OARFVd1Z-A7K1mFV.png"
class="graf-image" data-image-id="0*OARFVd1Z-A7K1mFV.png"
data-width="493" data-height="177" />
</figure>

You should convert the decimal number to hex and then hex to ascii
encoding. So let's do it

<figure id="f0ce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ppvx6Jbip6-zsNzN.png"
class="graf-image" data-image-id="0*Ppvx6Jbip6-zsNzN.png"
data-width="825" data-height="223" />
</figure>

### Task 21 :Read the packet {#3afb .graf .graf--h3 .graf-after--figure name="3afb"}

In this challenge you have to download a network capture file. I Opened
the capture file with wireshark. There were a whole lot of network
traffic captured so I had to use a filter. I used GET Method http filter
( http.request.method == "GET" ) to see if there were any files
transfered. For my surprise there was one file called flag.txt.

<figure id="23a7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*V-Gigv73dH3fA22l.png"
class="graf-image" data-image-id="0*V-Gigv73dH3fA22l.png"
data-width="875" data-height="450" />
</figure>

<figure id="4c45" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*2tscS4SNqjvpw59E.png"
class="graf-image" data-image-id="0*2tscS4SNqjvpw59E.png"
data-width="875" data-height="156" />
</figure>

I Followed the HTTP stream of this file and got the flag

<figure id="4b29" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0gmzLozZ2nN4lQ9w.png"
class="graf-image" data-image-id="0*0gmzLozZ2nN4lQ9w.png"
data-width="875" data-height="597" />
</figure>

<figure id="af71" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*suuT_fstnbvW0tbg.png"
class="graf-image" data-image-id="0*suuT_fstnbvW0tbg.png"
data-width="568" data-height="561" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#4d24 .graf .graf--h3 .graf-after--figure name="4d24"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#82a9 .graf .graf--h3 .graf-after--p name="82a9"}

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
.h-card} on [August 19, 2024](https://medium.com/p/59ae20bc8f7c).

[Canonical
link](https://medium.com/@bevijaygupta/ctf-collection-vol-1-tryhackme-writeup-59ae20bc8f7c){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
