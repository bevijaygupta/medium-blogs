---
title: "Network Services 2 Tryhackme Writeup  NFS  SMTP   MYSQL  9e0855df66ef"
platform: Medium
original_file: 2024-08-29_Network-Services-2-Tryhackme-Writeup--NFS--SMTP---MYSQL--9e0855df66ef.md
---

# Network Services 2 Tryhackme Writeup  NFS  SMTP   MYSQL  9e0855df66ef

::: {}
# Network Services 2 Tryhackme Writeup (NFS ,SMTP , MYSQL) {#network-services-2-tryhackme-writeup-nfs-smtp-mysql .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/networkservices2
:::

:::::::: {.section .e-content field="body"}
::::::: {#feb6 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::::: section-content
:::: {.section-inner .sectionLayout--insetColumn}
### Network Services 2 Tryhackme Writeup (NFS ,SMTP , MYSQL) {#0813 .graf .graf--h3 .graf--leading .graf--title name="0813"}

<figure id="8bf8" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*2zu7UuNexkam2aHg.png"
class="graf-image" data-image-id="0*2zu7UuNexkam2aHg.png"
data-width="521" data-height="310" />
</figure>

[https://tryhackme.com/room/networkservices2](https://tryhackme.com/room/networkservices2){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/networkservices2"
rel="noopener ugc nofollow noopener" target="_blank"}

**Room link:**
[https://tryhackme.com/room/networkservices2](https://tryhackme.com/room/networkservices2){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/networkservices2"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Hello and welcome!

This room is a sequel to the first network services room. Similarly, it
will explore a few more common Network Service vulnerabilities and
misconfigurations that you're likely to find in CTFs, and some
penetration test scenarios.

I would encourage you to complete the first network services room
([https://tryhackme.com/room/networkservices](https://tryhackme.com/room/networkservices){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/networkservices"
rel="noopener ugc nofollow noopener" target="_blank"}) before attempting
this one.

As with the previous room, it is definitely worth having a basic
knowledge of Linux before attempting this room. If you think you'll need
some help with this, try completing the 'Learn Linux' room
[(https://tryhackme.com/room/zthlinux)](https://tryhackme.com/room/zthlinux){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/zthlinux"
rel="noopener ugc nofollow noopener" target="_blank"}

Before we get started:

1.  [Connect to the TryHackMe OpenVPN Server (See
    [https://tryhackme.com/access](https://tryhackme.com/access){.markup--anchor
    .markup--li-anchor data-href="https://tryhackme.com/access"
    rel="noopener ugc nofollow noopener" target="_blank"} for
    help!)]{#54c5}
2.  [Make sure you're sitting comfortably, and have a cup of Tea, Coffee
    or Water close!]{#97f4}

Lets get started!

**N.B.** This is not a room on WiFi access hacking or hijacking, rather
how to gain unauthorized access to a machine by exploiting network
services. If you are interested in WiFi hacking, I suggest checking out
WiFi Hacking 101 by NinjaJc01
([https://tryhackme.com/room/wifihacking101](https://tryhackme.com/room/wifihacking101){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/wifihacking101"
rel="noopener ugc nofollow noopener" target="_blank"})

### Task 2: Understanding NFS {#0f77 .graf .graf--h3 .graf-after--p name="0f77"}

**What is NFS?**

NFS stands for "Network File System" and allows a system to share
directories and files with others over a network. By using NFS, users
and programs can access files on remote systems almost as if they were
local files. It does this by mounting all, or a portion of a file system
on a server. The portion of the file system that is mounted can be
accessed by clients with whatever privileges are assigned to each file.

**How does NFS work?**

We don't need to understand the technical exchange in too much detail to
be able to exploit NFS effectively- however if this is something that
interests you, I would recommend this resource:
[https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html](https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html){.markup--anchor
.markup--p-anchor
data-href="https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html"
rel="noopener ugc nofollow noopener" target="_blank"}

First, the client will request to mount a directory from a remote host
on a local directory just the same way it can mount a physical device.
The mount service will then act to connect to the relevant mount daemon
using RPC.

The server checks if the user has permission to mount whatever directory
has been requested. It will then return a file handle which uniquely
identifies each file and directory that is on the server.

If someone wants to access a file using NFS, an RPC call is placed to
NFSD (the NFS daemon) on the server. This call takes parameters such as:

- [The file handle]{#6095}
- [The name of the file to be accessed]{#d334}
- [The user's, user ID]{#33b6}
- [The user's group ID]{#d9ae}

These are used in determining access rights to the specified file. This
is what controls user permissions, I.E read and write of files.

**What runs NFS?**

Using the NFS protocol, you can transfer files between computers running
Windows and other non-Windows operating systems, such as Linux, MacOS or
UNIX.

A computer running Windows Server can act as an NFS file server for
other non-Windows client computers. Likewise, NFS allows a Windows-based
computer running Windows Server to access files stored on a non-Windows
NFS server.

**More Information:**

Here are some resources that explain the technical implementation, and
working of, NFS in more detail than I have covered here.

[https://www.datto.com/library/what-is-nfs-file-share](https://www.datto.com/library/what-is-nfs-file-share){.markup--anchor
.markup--p-anchor
data-href="https://www.datto.com/library/what-is-nfs-file-share"
rel="noopener ugc nofollow noopener" target="_blank"}\
[http://nfs.sourceforge.net/](http://nfs.sourceforge.net/){.markup--anchor
.markup--p-anchor data-href="http://nfs.sourceforge.net/"
rel="noopener ugc nofollow noopener" target="_blank"}\
[https://wiki.archlinux.org/index.php/NFS](https://wiki.archlinux.org/index.php/NFS){.markup--anchor
.markup--p-anchor data-href="https://wiki.archlinux.org/index.php/NFS"
rel="noopener ugc nofollow noopener" target="_blank"}

What does NFS stand for?

> ***Answer: Network File System***

What process allows an NFS client to interact with a remote directory as
though it was a physical device?

> ***Answer: Mounting***

What does NFS use to represent files and directories on the server?

> ***Answer: file handle***

What protocol does NFS use to communicate between the server and client?

> ***Answer: RPC***

What two pieces of user data does the NFS server take as parameters for
controlling user permissions? Format: parameter 1 / parameter 2

> ***Answer: user id / group id***

Can a Windows NFS server share files with a Linux client? (Y/N)

> ***Answer: Y***

Can a Linux NFS server share files with a MacOS client? (Y/N)

> ***Answer: Y***

What is the latest version of NFS? \[released in 2016, but is still up
to date as of 2020\] This will require external research.

> ***Answer: 4.2***

### Task 3: Enumerating NFS {#f883 .graf .graf--h3 .graf-after--blockquote name="f883"}

**What is Enumeration?**

Enumeration is defined as "a process which establishes an active\
connection to the target hosts to discover potential attack vectors in\
the system, and the same can be used for further exploitation of the\
system." --- [Infosec
Institute](https://resources.infosecinstitute.com/what-is-enumeration/){.markup--anchor
.markup--p-anchor
data-href="https://resources.infosecinstitute.com/what-is-enumeration/"
rel="noopener ugc nofollow noopener" target="_blank"}. It is a critical
phase when considering how to enumerate and exploit a remote machine- as
the information you will use to inform your attacks will come from this
stage

**Requirements**

In order to do more advanced enumeration of\
the NFS server, and shares- we're going to need a few tools. The first\
of which is key to interacting with any NFS share from your local\
machine- nfs-common.

**NFS-Common**

It is important to\
have this package installed on any machine that uses NFS, either as\
client or\
server. It includes programs such as: lockd, statd, showmount, nfsstat,\
gssd,\
idmapd and mount.nfs. Primarily, we are concerned with "showmount" and\
"mount.nfs" as these are going to be most useful to us when it comes to\
extracting information from the NFS share. If you'd like more\
information about this package, feel free to read:
[https://packages.ubuntu.com/xenial/nfs-common](https://packages.ubuntu.com/xenial/nfs-common){.markup--anchor
.markup--p-anchor
data-href="https://packages.ubuntu.com/xenial/nfs-common"
rel="noopener ugc nofollow noopener" target="_blank"}.\
You can install nfs-common using "*sudo apt install nfs-common*",\
it is part of the default repositories for most Linux distributions-\
such as the Kali Remote Machine that is provided to TryHackMe\
subscribers.

**Port Scanning**

Port scanning has been covered many times before, so I'll only cover the
basics that you need for this room here. If you'd like to learn more
about nmap in more detail please have a look at the
[nmap](https://tryhackme.com/room/furthernmap){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/furthernmap"
rel="noopener ugc nofollow noopener" target="_blank"} room.

The first step of enumeration is to\
conduct a port scan, to find out as much information as you can about\
the services, open ports and operating system of the target\
machine. You can go as in depth as you like on this, however I suggest\
using **nmap** with the **-A** and **-p-** tags.

**Mounting NFS shares**

Your client's system needs a directory where all the content shared by\
the host server in the export folder can be accessed. You can create\
this folder anywhere on your system. Once you've created this mount
point, you can use the "mount" command to connect the NFS share to the
mount point on your machine. Like so:

sudo mount -t nfs IP:share /tmp/mount/ -nolock

Let's break this down

**Tag** **Function** sudo Run as root mount Execute the mount command -t
nfs Type of device to mount, then specifying that it's NFS IP:share The
IP Address of the NFS server, and the name of the share we wish to mount
-nolock Specifies not to use NLM locking

Now we understand our tools, lets get started!

Conduct a thorough port scan scan of your choosing, how many ports are
open?

Port 22, 111, 2049, 37069, 39969, 41047, 48707 are open

> ***Answer: 7***

Which port contains the service we're looking to enumerate?

> ***Answer: 2049***

Now, use /usr/sbin/showmount -e \[IP\] to list the NFS shares, what is
the name of the visible share?

<figure id="4976" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*asC_pKDMmpugJCSa.png"
class="graf-image" data-image-id="0*asC_pKDMmpugJCSa.png"
data-width="357" data-height="102" />
</figure>

> ***Answer: /home***

Time to mount the share to our local machine!

First, use "*mkdir /tmp/mount*" to create a directory on your machine to
mount the share to. This is in the /tmp directory- so be aware that it
will be removed on restart.

Then, use the mount command we broke down earlier to mount the NFS share
to your local machine. Change directory to where you mounted the share-
what is the name of the folder inside?

``` {#2605 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mkdir /tmp/mount
mount -t nfs 10.10.108.156:home /tmp/mount -nolock
```

<figure id="00df" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Twx9U4FU3QCr9D6w.png"
class="graf-image" data-image-id="0*Twx9U4FU3QCr9D6w.png"
data-width="602" data-height="220" />
</figure>

> ***Answer: cappucino***

Have a look inside this directory, look at the files. Looks like we're
inside a user's home directory...

Interesting! Let's do a bit of research now, have a look through the
folders. Which of these folde**rs** could cont**a**in keys that would
give us remote access to the server?

<figure id="7bdb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_A_KFj-1Jm5g40fC.png"
class="graf-image" data-image-id="0*_A_KFj-1Jm5g40fC.png"
data-width="724" data-height="360" />
</figure>

> ***Answer: .ssh***

Which of these keys is most useful to us?

<figure id="474b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RMTkCc_M6Uvs5vEe.png"
class="graf-image" data-image-id="0*RMTkCc_M6Uvs5vEe.png"
data-width="585" data-height="237" />
</figure>

> ***Answer: id_rsa***

Copy this file to a different location your local machine, and change
the permissions to "600" using "chmod 600 \[file\]".

Assuming we were right about what type of directory this is, we can
pretty easily work out the name of the user this key corresponds to.

Can we log into the machine using *ssh -i \<key-file\>
\<username\>@\<ip\>* ? (Y/N)

<figure id="0062" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1HTfNzc3qWrxxqvV.png"
class="graf-image" data-image-id="0*1HTfNzc3qWrxxqvV.png"
data-width="477" data-height="115" />
</figure>

<figure id="da48" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*gVhyXSG8RM548wnM.png"
class="graf-image" data-image-id="0*gVhyXSG8RM548wnM.png"
data-width="726" data-height="319" />
</figure>

> ***Answer: Y***

### Task 4: Exploiting NFS {#8cf7 .graf .graf--h3 .graf-after--blockquote name="8cf7"}

**We're done, right?**

Not quite, if you have a low privilege shell on any machine and you
found that a machine has an NFS share you might be able to use that to
escalate privileges, depending on how it is configured.

**What is root_squash?**

By default, on NFS shares- Root Squashing is enabled, and prevents
anyone connecting to the NFS share from having root access to the NFS
volume. Remote root users are assigned a user "nfsnobody" when
connected, which has the least local privileges. Not what we want.
However, if this is turned off, it can allow the creation of SUID bit
files, allowing a remote user root access to the connected system.

**SUID**

So, what are files with the SUID bit set? Essentially, this means that
the file or files can be run with the permissions of the file(s)
owner/group. In this case, as the super-user. We can leverage this to
get a shell with these privileges!

**Method**

This sounds complicated, but really- provided you're familiar with how
SUID files work, it's fairly easy to understand. We're able to upload
files to the NFS share, and control the permissions of these files. We
can set the permissions of whatever we upload, in this case a bash shell
executable. We can then log in through SSH, as we did in the previous
task- and execute this executable to gain a root shell!

**The Executable**

Due to compatibility reasons, we'll use a standard Ubuntu Server 18.04
bash executable, the same as the server's- as we know from our nmap
scan. You can download it
[here](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Networks%202/bash){.markup--anchor
.markup--p-anchor
data-href="https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Networks%202/bash"
rel="noopener ugc nofollow noopener" target="_blank"}.

**Mapped Out Pathway:**

If this is still hard to follow, here's a step by step of the actions
we're taking, and how they all tie together to allow us to gain a root
shell:

NFS Access -\>\
Gain Low Privilege Shell -\>\
Upload Bash Executable to the NFS share -\>\
Set SUID Permissions Through NFS Due To Misconfigured Root Squash -\>\
Login through SSH -\>\
Execute SUID Bit Bash Executable -\>\
ROOT ACCESS

First we are going to download the bash shell

***download the file located here as stated in the task***
[***https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Networks%202/bash***](https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Networks%202/bash){.markup--anchor
.markup--p-anchor
data-href="https://github.com/TheRealPoloMints/Blog/blob/master/Security%20Challenge%20Walkthroughs/Networks%202/bash"
rel="noopener ugc nofollow noopener" target="_blank"}

The we are going to copy the bash by typing in **cp bash
*/tmp/mount/cappucino*** now we are giving the root right to the file
and copy it over to the share.

<figure id="1430" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*C47i-5jOi-g0G2Nd.png"
class="graf-image" data-image-id="0*C47i-5jOi-g0G2Nd.png"
data-width="354" data-height="315" />
</figure>

**Question 1**. Now, we're going to add the SUID bit permission to the
bash executable we just copied to the share using "sudo chmod
+\[permission\] bash". What letter do we use to set the SUID bit set
using chmod?

> ***Answer: s***

**Question 2**. Let's do a sanity check, let's check the permissions of
the "bash" executable using "ls -la bash". What does the permission set
look like? Make sure that it ends with -sr-x.

> ***Answer: -rwsr-sr-x***

**Question 3**. Great! If all's gone well you should have a shell as
root! What's the root flag?

<figure id="a670" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TM8FFpI7PdkXMw_U.png"
class="graf-image" data-image-id="0*TM8FFpI7PdkXMw_U.png"
data-width="357" data-height="195" />
</figure>

### Task 5: Understanding SMTP {#e4f5 .graf .graf--h3 .graf-after--figure name="e4f5"}

**What is SMTP?**

SMTP stands for "Simple Mail Transfer Protocol". It is utilised to
handle the sending of emails. In order to support email services, a
protocol pair is required, comprising of SMTP and POP/IMAP. Together
they allow the user to send outgoing mail and retrieve incoming mail,
respectively.

The SMTP server performs three basic functions:

- [It verifies who is sending emails through the SMTP server.]{#245a}
- [It sends the outgoing mail]{#f146}
- [If the outgoing mail can't be delivered it sends the message back to
  the sender]{#ff69}

Most people will have encountered SMTP when configuring a new email
address on some third-party email clients, such as Thunderbird; as when
you configure a new email client, you will need to configure the SMTP
server configuration in order to send outgoing emails.

**POP and IMAP**

POP, or "Post Office Protocol" and IMAP, "Internet Message Access
Protocol" are both email protocols who are responsible for the transfer
of email between a client and a mail server. The main differences is in
POP's more simplistic approach of downloading the inbox from the mail
server, to the client. Where IMAP will synchronise the current inbox,
with new mail on the server, downloading anything new. This means that
changes to the inbox made on one computer, over IMAP, will persist if
you then synchronise the inbox from another computer. The POP/IMAP
server is responsible for fulfiling this process.

**How does SMTP work?**

Email delivery functions much the same as the physical mail delivery
system. The user will supply the email (a letter) and a service (the
postal delivery service), and through a series of steps- will deliver it
to the recipients inbox (postbox). The role of the SMTP server in this
service, is to act as the sorting office, the email (letter) is picked
up and sent to this server, which then directs it to the recipient.

We can map the journey of an email from your computer to the recipient's
like this:

<figure id="bfd2" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*rmVVrcF7nA3BreiD"
class="graf-image" data-image-id="0*rmVVrcF7nA3BreiD" data-width="875"
data-height="436" />
</figure>

1\. The mail user agent, which is either your email client or an
external program. connects to the SMTP server of your domain, e.g.
smtp.google.com. This initiates the SMTP handshake. This connection
works over the SMTP port- which is usually 25. Once these connections
have been made and validated, the SMTP session starts.

2\. The process of sending mail can now begin. The client first submits
the sender, and recipient's email address- the body of the email and any
attachments, to the server.

3\. The SMTP server then checks whether the domain name of the recipient
and the sender is the same.

4\. The SMTP server of the sender will make a connection to the
recipient's SMTP server before relaying the email. If the recipient's
server can't be accessed, or is not available- the Email gets put into
an SMTP queue.

5\. Then, the recipient's SMTP server will verify the incoming email. It
does this by checking if the domain and user name have been recognised.
The server will then forward the email to the POP or IMAP server, as
shown in the diagram above.

6\. The E-Mail will then show up in the recipient's inbox.

This is a very simplified version of the process, and there are a lot of
sub-protocols, communications and details that haven't been included. If
you're looking to learn more about this topic, this is a really friendly
to read breakdown of the finer technical details- I actually used it to
write this breakdown:

[https://computer.howstuffworks.com/e-mail-messaging/email3.htm](https://computer.howstuffworks.com/e-mail-messaging/email3.htm){.markup--anchor
.markup--p-anchor
data-href="https://computer.howstuffworks.com/e-mail-messaging/email3.htm"
rel="noopener ugc nofollow noopener" target="_blank"}

**What runs SMTP?**

SMTP Server software is readily available on Windows server platforms,
with many other variants of SMTP being available to run on Linux.

**More Information:**

Here is a resource that explain the technical implementation, and
working of, SMTP in more detail than I have covered here.

[https://www.afternerd.com/blog/smtp/](https://www.afternerd.com/blog/smtp/){.markup--anchor
.markup--p-anchor data-href="https://www.afternerd.com/blog/smtp/"
rel="noopener ugc nofollow noopener" target="_blank"}

What does SMTP stand for?

> ***Answer: Simple Mail Transfer Protocol***

What does SMTP handle the sending of?

> ***Answer: emails***

What is the first step in the SMTP process?

> ***Answer: SMTP handshake***

What is the default SMTP port?

> ***Answer: 25***

Where does the SMTP server send the email if the recipient's server is
not available?

> ***Answer: smtp queue***

On what server does the Email ultimately end up on?

> ***Answer: POP/IMAP***

Can a Linux machine run an SMTP server? (Y/N)

> ***Answer: Y***

Can a Windows machine run an SMTP server? (Y/N)

> ***Answer: Y***

### Task 6: Enumerating SMTP {#a97a .graf .graf--h3 .graf-after--blockquote name="a97a"}

**Enumerating Server Details**

Poorly configured or vulnerable mail servers can often provide an
initial foothold into a network, but prior to launching an attack, we
want to fingerprint the server to make our targeting as precise as
possible. We're going to use the "*smtp_version*" module in MetaSploit
to do this. As its name implies, it will scan a range of IP addresses
and determine the version of any mail servers it encounters.

**Enumerating Users from SMTP**

The SMTP service has two internal commands that allow the enumeration of
users: VRFY (confirming the names of valid users) and EXPN (which
reveals the actual address of user's aliases and lists of e-mail
(mailing lists). Using these SMTP commands, we can reveal a list of
valid users

We can do this manually, over a telnet connection- however Metasploit
comes to the rescue again, providing a handy module appropriately called
"*smtp_enum*" that will do the legwork for us! Using the module is a
simple matter of feeding it a host or range of hosts to scan and a
wordlist containing usernames to enumerate.

**Requirements**

As we're going to be using Metasploit for this, it's important that you
have Metasploit installed. It is by default on both Kali Linux and
Parrot OS; however, it's always worth doing a quick update to make sure
that you're on the latest version before launching any attacks. You can
do this with a simple "sudo apt update", and accompanying upgrade- if
any are required.

**Alternatives**

It's worth noting that this enumeration technique will work for the
majority of SMTP configurations; however there are other, non-metasploit
tools such as smtp-user-enum that work even better for enumerating
OS-level user accounts on Solaris via the SMTP service. Enumeration is
performed by inspecting the responses to VRFY, EXPN, and RCPT TO
commands.

This technique could be adapted in future to work against other
vulnerable SMTP daemons, but this hasn't been done as of the time of
writing. It's an alternative that's worth keeping in mind if you're
trying to distance yourself from using Metasploit e.g. in preparation
for OSCP.

Now we've covered the theory. Let's get going!

First, lets run a port scan against the target machine, same as last
time. What port is SMTP running on?

<figure id="e395" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5YAIV8aZ5_d71ibM.png"
class="graf-image" data-image-id="0*5YAIV8aZ5_d71ibM.png"
data-width="733" data-height="334" />
</figure>

> ***Answer: 25***

Okay, now we know what port we should be targeting, let's start up
Metasploit. What command do we use to do this?

If you would like some more help, or practice using, Metasploit,
Darkstar has an amazing room on Metasploit that you can check out here:

::: {#19bd .graf .graf--mixtapeEmbed .graf-after--p}
[**TryHackMe \| Cyber Security Training**\
*TryHackMe is a free online platform for learning cyber security, using
hands-on exercises and labs, all through
your...*tryhackme.com](https://tryhackme.com/r/room/rpmetasploit?source=post_page-----c9b81ea4add6-------------------------------- "https://tryhackme.com/r/room/rpmetasploit?source=post_page-----c9b81ea4add6--------------------------------"){.markup--anchor
.markup--mixtapeEmbed-anchor
data-href="https://tryhackme.com/r/room/rpmetasploit?source=post_page-----c9b81ea4add6--------------------------------"}[](https://tryhackme.com/r/room/rpmetasploit?source=post_page-----c9b81ea4add6--------------------------------){.js-mixtapeImage
.mixtapeImage .u-ignoreBlock media-id="d2895c872cce4f2675fb1ab5021d0fd9"
thumbnail-img-id="0*_RlbIjYqDE-dmKKb"
style="background-image: url(https://cdn-images-1.medium.com/fit/c/160/160/0*_RlbIjYqDE-dmKKb);"}
:::

> ***Answer: msfconsole***

Let's search for the module "smtp_version", what's it's full module
name?

<figure id="667e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bl1LEVMVZDaOU-mm.png"
class="graf-image" data-image-id="0*bl1LEVMVZDaOU-mm.png"
data-width="875" data-height="216" />
</figure>

> ***Answer: auxiliary/scanner/smtp/smtp_version***

Great, now- select the module and list the options. How do we do this?

<figure id="1f45" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kEb2B3LB4EMIZWFD.png"
class="graf-image" data-image-id="0*kEb2B3LB4EMIZWFD.png"
data-width="767" data-height="315" />
</figure>

> ***Answer: options***

Have a look through the options, does everything seem correct? What is
the option we need to set?

> ***Answer: RHOSTS***

Set that to the correct value for your target machine. Then run the
exploit. What's the system mail name?

<figure id="4722" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yKy3mBvbBNwJ3N7O.png"
class="graf-image" data-image-id="0*yKy3mBvbBNwJ3N7O.png"
data-width="846" data-height="218" />
</figure>

> ***Answer: polosmtp.home***

What Mail Transfer Agent (MTA) is running the SMTP server? This will
require some external research.

> ***Answer: Postfix***

Good! We've now got a good amount of information on the target system to
move onto the next stage. Let's search for the module "*smtp_enum*",
what's it's full module name?

<figure id="62f3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*t7u2OvsrZ9MCijvV.png"
class="graf-image" data-image-id="0*t7u2OvsrZ9MCijvV.png"
data-width="875" data-height="329" />
</figure>

> ***Answer: auxiliary/scanner/smtp/smtp_enum***

We're going to be using the *"top-usernames-shortlist.txt"* wordlist
from the Usernames subsection of seclists (/usr/share/seclists/Usernames
if you have it installed).

Seclists is an amazing collection of wordlists. If you're running Kali
or Parrot you can install seclists with: "sudo apt install seclists"
Alternatively, you can download the repository from
[here](https://github.com/danielmiessler/SecLists){.markup--anchor
.markup--p-anchor data-href="https://github.com/danielmiessler/SecLists"
rel="noopener ugc nofollow noopener" target="_blank"}.

What option do we need to set to the wordlist's path?

<figure id="4551" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pVOMghEBFm0jwaqz.png"
class="graf-image" data-image-id="0*pVOMghEBFm0jwaqz.png"
data-width="875" data-height="331" />
</figure>

> ***Answer: USER_FILE***

Once we've set this option, what is the other essential paramater we
need to set?

> ***Answer: RHOSTS***

Now, set the THREADS parameter to 16 and run the exploit, this may take
a few minutes, so grab a cup of tea, coffee, water. Keep yourself
hydrated!

Okay! Now that's finished, what username is returned?

<figure id="c96c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oiIlmvTuxVWfJEJY.png"
class="graf-image" data-image-id="0*oiIlmvTuxVWfJEJY.png"
data-width="875" data-height="145" />
</figure>

> ***Answer: administrator***

### Task 7: Exploiting SMTP {#3fb8 .graf .graf--h3 .graf-after--blockquote name="3fb8"}

**Brute force SSH**

``` {#5187 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
hydra -t 16 -l administrator -P rockyou.txt -vV 10.10.93.163 ssh
```

<figure id="f982" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Dj5VK9BL9v_2VRG9.png"
class="graf-image" data-image-id="0*Dj5VK9BL9v_2VRG9.png"
data-width="872" data-height="334" />
</figure>

The password will show up. Now we can use that password to initiated an
ssh connection to the server to get what is in smtp.txt

<figure id="0237" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vq10Ip_XdgT1jXuq.png"
class="graf-image" data-image-id="0*vq10Ip_XdgT1jXuq.png"
data-width="610" data-height="619" />
</figure>

<figure id="0feb" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*wl_wuQnzDyALp2dg.png"
class="graf-image" data-image-id="0*wl_wuQnzDyALp2dg.png"
data-width="417" data-height="127" />
</figure>

### Task 8: Understanding MySQL {#8e70 .graf .graf--h3 .graf-after--figure name="8e70"}

**What is MySQL?**

In its simplest definition, MySQL is a relational database management
system (RDBMS) based on Structured Query Language (SQL). Too many
acronyms? Lets break it down:

**Database:**

A database is simply a persistent, organised collection of structured
data

**RDBMS:**

A software or service used to create and manage databases based on a
relational model. The word "relational" just means that the data stored
in the dataset is organized as tables. Every table relates in some way
to each other's "primary key" or other "key" factors.

**SQL:**

MYSQL is just a brand name for one of the most popular RDBMS software
implementations. As we know, it uses a client-server model. But how does
the client and server communicate? They use a language, specifically the
Structured Query Language (SQL).

Many other products, such as PostgreSQL and Microsoft SQL server have
the word SQL in them. This similarly signifies that this is a product
utilising the Structured Query Language syntax.

**How does MySQL work?**

MySQL, as an RDBMS, is made up of the server and utility programs that
help in the administration of mySQL databases.

The server handles all database instructions like creating editing and
accessing data. It takes, and manages these requests and communicates
using the MySQL protocol. This whole process can be broken down into
these stages:

1.  [MySQL creates a database for storing and manipulating data,
    defining the relationship of each table.]{#d3e2}
2.  [Clients make requests by making specific statements in SQL.]{#7d26}
3.  [The server will respond to the client with whatever information has
    been requested]{#e088}

**What runs MySQL?**

MySQL can run on various platforms, whether it's Linux or windows. It is
commonly used as a back end database for many prominent websites and
forms an essential component of the LAMP stack, which includes: Linux,
Apache, MySQL, and PHP.

**More Information:**

Here are some resources that explain the technical implementation, and
working of, MySQL in more detail than I have covered here:

[https://dev.mysql.com/doc/dev/mysql-server/latest/PAGE_SQL_EXECUTION.html](https://dev.mysql.com/doc/dev/mysql-server/latest/PAGE_SQL_EXECUTION.html){.markup--anchor
.markup--p-anchor
data-href="https://dev.mysql.com/doc/dev/mysql-server/latest/PAGE_SQL_EXECUTION.html"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://www.w3schools.com/php/php_mysql_intro.asp](https://www.w3schools.com/php/php_mysql_intro.asp){.markup--anchor
.markup--p-anchor
data-href="https://www.w3schools.com/php/php_mysql_intro.asp"
rel="noopener ugc nofollow noopener" target="_blank"}

What type of software is MySQL?

> ***Answer: relational database management system***

What language is MySQL based on?

> ***Answer: SQL***

What communication model does MySQL use?

> ***Answer: client-server***

What is a common application of MySQL?

> ***Answer: back end database***

What major social network uses MySQL as their back-end database? This
will require further research.

> ***Answer: Facebook***

### Task 9: Enumerating MySQL {#a8ab .graf .graf--h3 .graf-after--blockquote name="a8ab"}

**When you would begin attacking MySQL**

MySQL is likely not going to be the first point of call when it comes to
getting initial information about the server. You can, as we have in
previous tasks, attempt to brute-force default account passwords if you
really don't have any other information- however in most CTF scenarios,
this is unlikely to be the avenue you're meant to pursue.

**The Scenario**

Typically, you will have gained some initial credentials from
enumerating other services, that you can then use to enumerate, and
exploit the MySQL service. As this room focuses on exploiting and
enumerating the network service, for the sake of the scenario, we're
going to assume that you found the **credentials: "root:password"**
while enumerating subdomains of a web server. After trying the login
against SSH unsuccessfully, you decide to try it against MySQL.

**Requirements**

You're going to want to have MySQL installed on your system, in order to
connect to the remote MySQL server. In case this isn't already
installed, you can install it using "sudo apt install MySQL". Don't
worry- this won't install the server package on your system- just the
client.

Again, we're going to be using Metasploit for this, it's important that
you have it Metasploit installed, as it is by default on both Kali Linux
and Parrot OS.

**Alternatives**

As with the previous task, it's worth noting that everything we're going
to be doing using Metasploit can also be done either manually, or with a
set of non-metasploit tools such as nmap's mysql-enum script:
[https://nmap.org/nsedoc/scripts/mysql-enum.html](https://nmap.org/nsedoc/scripts/mysql-enum.html){.markup--anchor
.markup--p-anchor
data-href="https://nmap.org/nsedoc/scripts/mysql-enum.html"
rel="noopener ugc nofollow noopener" target="_blank"} or
[https://www.exploit-db.com/exploits/23081](https://www.exploit-db.com/exploits/23081){.markup--anchor
.markup--p-anchor data-href="https://www.exploit-db.com/exploits/23081"
rel="noopener ugc nofollow noopener" target="_blank"}. I recommend after
you complete this room, you go back and attempt it manually to make sure
you understand the process that is being used to display the information
you acquire.

Okay, enough talk. Let's get going!

As always, let's start out with a port scan, so we know what port the
service we're trying to attack is running on. What port is MySQL using?

<figure id="f773" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*avMeMelV2dU39ToL.png"
class="graf-image" data-image-id="0*avMeMelV2dU39ToL.png"
data-width="621" data-height="294" />
</figure>

> ***Answer: 3306***

Good, now- we think we have a set of credentials. Let's double check
that by manually connecting to the MySQL server. We can do this using
the command "*mysql -h \[IP\] -u \[username\] -p*"

Okay, we know that our login credentials work. Lets quit out of this
session with "exit" and launch up Metasploit.

We're going to be using the "mysql_sql" module.

<figure id="5b66" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*k62LMmoPndxU59ef.png"
class="graf-image" data-image-id="0*k62LMmoPndxU59ef.png"
data-width="787" data-height="303" />
</figure>

Search for, select and list the options it needs. What three options do
we need to set? (in descending order).

**credentials: "root:password"**

<figure id="3c0a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MpFGUatjwf16055Q.png"
class="graf-image" data-image-id="0*MpFGUatjwf16055Q.png"
data-width="683" data-height="442" />
</figure>

> ***Answer: PASSWORD/RHOSTS/USERNAME***

Run the exploit. By default it will test with the "select module()"
command, what result does this give you?

<figure id="aa8b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OXKD3Tle38__fEME.png"
class="graf-image" data-image-id="0*OXKD3Tle38__fEME.png"
data-width="678" data-height="156" />
</figure>

> ***Answer: 5.7.29--0ubuntu0.18.04.1***

Great! We know that our exploit is landing as planned. Let's try to gain
some more ambitious information. Change the "sql" option to "show
databases". how many databases are returned?

<figure id="3791" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kM9ij30cz8Wa_mcH.png"
class="graf-image" data-image-id="0*kM9ij30cz8Wa_mcH.png"
data-width="662" data-height="275" />
</figure>

> ***Answer: 4***

### Task 10: Exploiting MySQL {#63f1 .graf .graf--h3 .graf-after--blockquote name="63f1"}

**What do we know?**

Let's take a sanity check before moving on to try and exploit the
database fully, and gain more sensitive information than just database
names. We know:

1\. MySQL server credentials

2\. The version of MySQL running

3\. The number of Databases, and their names.

**Key Terminology**

In order to understand the exploits we're going to use next- we need to
understand a few key terms.

**Schema:**

*In MySQL, physically, a* schema *is synonymous with a* database*. You
can substitute the keyword "SCHEMA" instead of DATABASE in MySQL SQL
syntax, for example using CREATE SCHEMA instead of CREATE DATABASE. It's
important to understand this relationship because some other database
products draw a distinction. For example, in the Oracle Database
product, a* schema *represents only a part of a database: the tables and
other objects owned by a single user.*

**Hashes:**

Hashes are, very simply, the product of a cryptographic algorithm to
turn a variable length input into a fixed length output.

In MySQL hashes can be used in different ways, for instance to index
data into a hash table. Each hash has a unique ID that serves as a
pointer to the original data. This creates an index that is
significantly smaller than the original data, allowing the values to be
searched and accessed more efficiently

However, the data we're going to be extracting are password hashes which
are simply a way of storing passwords not in plaintext format.

Lets get cracking.

First, let's search for and select the "mysql_schemadump" module. What's
the module's full name?

<figure id="cf53" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NOLGSWBrPv__fBBY.png"
class="graf-image" data-image-id="0*NOLGSWBrPv__fBBY.png"
data-width="875" data-height="475" />
</figure>

> ***Answer: auxiliary/scanner/mysql/mysql_schemadump***

Great! Now, you've done this a few times by now so I'll let you take it
from here. Set the relevant options, run the exploit. What's the name of
the last table that gets dumped?

<figure id="d3dd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DhFHXIBpq2Vn9w4D.png"
class="graf-image" data-image-id="0*DhFHXIBpq2Vn9w4D.png"
data-width="671" data-height="131" />
</figure>

<figure id="4892" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*JlfwOxSkbvvm7ciM.png"
class="graf-image" data-image-id="0*JlfwOxSkbvvm7ciM.png"
data-width="613" data-height="317" />
</figure>

> ***Answer: x\$waits_global_by_latency***

Awesome, you have now dumped the tables, and column names of the whole
database. But we can do one better... search for and select the
"mysql_hashdump" module. What's the module's full name?

<figure id="03a0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*L1jYRNsMhMNaF-Fc.png"
class="graf-image" data-image-id="0*L1jYRNsMhMNaF-Fc.png"
data-width="875" data-height="444" />
</figure>

> ***Answer: auxiliary/scanner/mysql/mysql_hashdump***

Again, I'll let you take it from here. Set the relevant options, run the
exploit. What non-default user stands out to you?

<figure id="811f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*p5qhSNtuywBOKL56.png"
class="graf-image" data-image-id="0*p5qhSNtuywBOKL56.png"
data-width="875" data-height="263" />
</figure>

> ***Answer: carl***

Another user! And we have their password hash. This could be very
interesting. Copy the hash string in full, like: bob:\*HASH to a text
file on your local machine called "hash.txt".

What is the user/hash combination string?

> ***Answer:
> carl:\*EA\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*1***

<figure id="4413" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*lJQrbzAZAbJ472t2.png"
class="graf-image" data-image-id="0*lJQrbzAZAbJ472t2.png"
data-width="759" data-height="290" />
</figure>

Awesome. Password reuse is not only extremely dangerous, but extremely
common. What are the chances that this user has reused their password
for a different service?

<figure id="1fa6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZYcCOjK0gOeAOcLj.png"
class="graf-image" data-image-id="0*ZYcCOjK0gOeAOcLj.png"
data-width="800" data-height="598" />
</figure>

What's the contents of MySQL.txt

<figure id="8614" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ayOSWBDkvtSLiBVG.png"
class="graf-image" data-image-id="0*ayOSWBDkvtSLiBVG.png"
data-width="459" data-height="127" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#3479 .graf .graf--h3 .graf-after--figure name="3479"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#b4d3 .graf .graf--h3 .graf-after--p name="b4d3"}

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
.h-card} on [August 29, 2024](https://medium.com/p/9e0855df66ef).

[Canonical
link](https://medium.com/@bevijaygupta/network-services-2-tryhackme-writeup-nfs-smtp-mysql-9e0855df66ef){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
