---
title: "Cyborg Tryhackme Writeup 58381f39b6cc"
platform: Medium
original_file: 2024-08-23_Cyborg-Tryhackme-Writeup-58381f39b6cc.md
---

# Cyborg Tryhackme Writeup 58381f39b6cc

::: {}
# Cyborg Tryhackme Writeup {#cyborg-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Cyborg"
:::

::::::: {.section .e-content field="body"}
:::::: {#19fe .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Cyborg Tryhackme Writeup {#c64e .graf .graf--h3 .graf--leading .graf--title name="c64e"}

**This is a Writeup of Tryhackme room "Cyborg"**

<figure id="8bd9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oidoI-Taepw_nXU7.png"
class="graf-image" data-image-id="0*oidoI-Taepw_nXU7.png"
data-width="496" data-height="246" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/cyborgt8](https://tryhackme.com/room/cyborgt8){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/cyborgt8"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

This writeup will help you solve the Cyborg box on
[TryHackMe](https://tryhackme.com/){.markup--anchor .markup--p-anchor
data-href="https://tryhackme.com/" rel="noopener ugc nofollow noopener"
target="_blank"}. Before we start enumerating the box, add the following
line to your `/etc/hosts`{.markup--code .markup--p-code} file.

``` {#b1c7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo "10.10.186.238   cyborg.thm" >> /etc/hosts
```

### TryHackMe Cyborg --- Enumeration {#e9bc .graf .graf--h3 .graf-after--pre name="e9bc"}

As per usual, we start by running a port scan on the host using
`nmap`{.markup--code .markup--p-code}. The `sC`{.markup--code
.markup--p-code} and `sV`{.markup--code .markup--p-code} flags indicate
that basic vulnerability scripts are executed against the target and
that the port scan tries to find version information.

<figure id="9890" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*K41hwaa2uFK5MbPw.png"
class="graf-image" data-image-id="0*K41hwaa2uFK5MbPw.png"
data-width="618" data-height="338" />
</figure>

The answers to the first three questions can be found in this output.
First, there are `2`{.markup--code .markup--p-code} open ports. Second,
the service running on port `22`{.markup--code .markup--p-code} is SSH.
Third, the service running on port `80`{.markup--code .markup--p-code}
is `HTTP`{.markup--code .markup--p-code}. Browsing to:
`http://cyborg.thm/`{.markup--code .markup--p-code} gives us the
following page:

**#1**: Scan the machine, how many ports are open?

> ***Answer: 2***

**#2**: What service is running on port 22?

> ***Answer: SSH***

**#3**: What service is running on port 80?

> ***Answer: http***

<figure id="0470" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*e--uSQkCf9dm3KCD.png"
class="graf-image" data-image-id="0*e--uSQkCf9dm3KCD.png"
data-width="779" data-height="254" />
</figure>

**Gobuster**

``` {#1f6f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://cyborg.thm/ -w /usr/share/wordlists/common.txt
```

<figure id="d0c2" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*4dJ86yOGumHJRs-r.png"
class="graf-image" data-image-id="0*4dJ86yOGumHJRs-r.png"
data-width="481" data-height="213" />
</figure>

he most interesting paths are `etc`{.markup--code .markup--p-code} and
`admin`{.markup--code .markup--p-code}.

Browsing to
[http://cyborg.thm/admin/](http://cyborg.thm/admin/){.markup--anchor
.markup--p-anchor data-href="http://cyborg.thm/admin/"
rel="noopener ugc nofollow noopener" target="_blank"} gives us the
following website:

<figure id="0e26" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yhiLsGIdb4XZhGE6.png"
class="graf-image" data-image-id="0*yhiLsGIdb4XZhGE6.png"
data-width="779" data-height="384" />
</figure>

<figure id="b027" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*p_53qwQ3XZl4HZ6t.png"
class="graf-image" data-image-id="0*p_53qwQ3XZl4HZ6t.png"
data-width="789" data-height="648" />
</figure>

So „Alex" is not sure how to configure squid properly and maybe we find
at the found /etc directory more usefuls stuff and a backup file is
alway worth a look.

Browsing to the `etc`{.markup--code .markup--p-code} directory we can
find the following hash:

<figure id="b58b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*XII_XnOl4LCqoMH8.png"
class="graf-image" data-image-id="0*XII_XnOl4LCqoMH8.png"
data-width="524" data-height="141" />
</figure>

We can crack this hash using `john`{.markup--code .markup--p-code}. You
can install John using the following [GitHub
page](https://github.com/openwall/john){.markup--anchor
.markup--p-anchor data-href="https://github.com/openwall/john"
rel="noopener ugc nofollow noopener" target="_blank"}. After installing
`john`{.markup--code .markup--p-code} run the following command to crack
the hash.

<figure id="99de" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OeUQAkICeWRm-zfv.png"
class="graf-image" data-image-id="0*OeUQAkICeWRm-zfv.png"
data-width="676" data-height="348" />
</figure>

### User Flag {#a439 .graf .graf--h3 .graf-after--figure name="a439"}

Nice we found a password! Going back to the admin section, we can
download an archive file by clicking one of the links in the header.
Download the `archive.tar`{.markup--code .markup--p-code} file by
running:

<figure id="7979" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xSq9R7C2mzkHCMdm.png"
class="graf-image" data-image-id="0*xSq9R7C2mzkHCMdm.png"
data-width="467" data-height="187" />
</figure>

<figure id="88e6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*HqMPMcJdY_KLcV7A.png"
class="graf-image" data-image-id="0*HqMPMcJdY_KLcV7A.png"
data-width="441" data-height="329" />
</figure>

<figure id="1058" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*-L5eKuLe1EYUuBMx.png"
class="graf-image" data-image-id="0*-L5eKuLe1EYUuBMx.png"
data-width="474" data-height="100" />
</figure>

Nice, we just found out that these files together are a backup created
by `Borg`{.markup--code .markup--p-code}. You can install
`Borg`{.markup--code .markup--p-code} by running the following commands:

``` {#99be .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
sudo apt install borgbackup -y
```

After that we can list the repository to verify our findings with

<figure id="6d25" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TiR6OnELZnOZ7wLT.png"
class="graf-image" data-image-id="0*TiR6OnELZnOZ7wLT.png"
data-width="875" data-height="139" />
</figure>

Create a new folder and open / mount the repository with the following
command

``` {#720c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mkdir unpacked
borg mount home/field/dev/final_archive unpacked
*put in passphrase*
```

Now our directory `unpacked `{.markup--code .markup--p-code}is filled
with new files that we can check out.

<figure id="2ba3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DW-P0ez5Pk8wh9x9.png"
class="graf-image" data-image-id="0*DW-P0ez5Pk8wh9x9.png"
data-width="663" data-height="198" />
</figure>

<figure id="b665" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*N7eMn7cNlhV7MD3F.png"
class="graf-image" data-image-id="0*N7eMn7cNlhV7MD3F.png"
data-width="875" data-height="132" />
</figure>

It looks like we have anything we need to tickle that port 22 and we can
unmount the archive with

``` {#0d19 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
borg umount unpacked
```

Connect via ssh and grad that user flag!

``` {#6cbf .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh alex@cyborg.thm
```

<figure id="7ee9" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZjxZsCyE-rTq40CB.png"
class="graf-image" data-image-id="0*ZjxZsCyE-rTq40CB.png"
data-width="767" data-height="150" />
</figure>

### Root Flag {#7035 .graf .graf--h3 .graf-after--figure name="7035"}

### Privilege Escalation {#b95d .graf .graf--h3 .graf-after--h3 name="b95d"}

<figure id="ed06" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*CQzmMRinFv8xK1ZF.png"
class="graf-image" data-image-id="0*CQzmMRinFv8xK1ZF.png"
data-width="563" data-height="204" />
</figure>

The file is owned by `alex`{.markup--code .markup--p-code} so we can
freely edit the contents of this file to become root. Run the following
commands to become the `root`{.markup--code .markup--p-code} user:

<figure id="245a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eDXHXfr4_NjPPS-J.png"
class="graf-image" data-image-id="0*eDXHXfr4_NjPPS-J.png"
data-width="629" data-height="258" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#897b .graf .graf--h3 .graf-after--figure name="897b"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#bf38 .graf .graf--h3 .graf-after--p name="bf38"}

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
.h-card} on [August 23, 2024](https://medium.com/p/58381f39b6cc).

[Canonical
link](https://medium.com/@bevijaygupta/cyborg-tryhackme-writeup-58381f39b6cc){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
