---
title: "The Hacker Methodology Tryhackme Writeup 584edca63405"
platform: Medium
original_file: 2024-08-23_The-Hacker-Methodology-Tryhackme-Writeup-584edca63405.md
---

# The Hacker Methodology Tryhackme Writeup 584edca63405

::: {}
# The Hacker Methodology Tryhackme Writeup {#the-hacker-methodology-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "The Hacker Methodology"
:::

::::::: {.section .e-content field="body"}
:::::: {#d67f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### The Hacker Methodology Tryhackme Writeup {#7470 .graf .graf--h3 .graf--leading .graf--title name="7470"}

**This is a Writeup of Tryhackme room "The Hacker Methodology"**

<figure id="5f21" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Kdmp45inI8RjzGD3.png"
class="graf-image" data-image-id="0*Kdmp45inI8RjzGD3.png"
data-width="476" data-height="257" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/hackermethodology](https://tryhackme.com/room/hackermethodology){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/hackermethodology"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

**What process does a Hacker follow?**

While you might think that a hacker does whatever he/she wants, it is
actually true that professional hackers/penetration tester generally
follow an established process to understand and exploit their targets.
This ensures that there is consistency between how assessments are
performed throughout the industry, and is the methodology that drives
assessments.

**The Process that pentesters follow is summarized in the following
steps:**

1.  [**Reconnaissance**]{#e75b}
2.  [**Enumeration/Scanning**]{#6198}
3.  [**Gaining Access**]{#9b6d}
4.  [**Privilege Escalation**]{#074d}
5.  [**Covering Tracks**]{#5e49}
6.  [**Reporting**]{#fe51}

**In the next sections we will go through each aspect of this process in
more detail.**

**Answer the question below to continue.**

**Q.1** What is the first phase of the Hacker Methodology?

> ***Answer: Reconnaissance***

### Task 2: Reconnaissance Overview {#c09f .graf .graf--h3 .graf-after--blockquote name="c09f"}

The first phase of the Ethical Hacker Methodology is **Reconnaissance.**

**Reconnaissance is all about collecting information about your
target.**

**Generally speaking, reconnaissance usually involves no interaction
with the target(s) or system(s).**

Reconnaissance is a pretty simple concept, think about what tools we can
use on the internet to gather information about people.

What websites and technology come to mind to gather information about a
target organization, technology, or set of individuals?

**In this case, lets use the company: SpaceX. Stop here and take 2
minutes to do some research on SpaceX and note down any websites you
used to conduct research.**

<figure id="bb0a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iUBSMZs-3-3_OOhZ.jpg"
class="graf-image" data-image-id="0*iUBSMZs-3-3_OOhZ.jpg"
data-width="875" data-height="875" />
</figure>

**Where is the place that you started your research about SpaceX?**

Most likely, you started at one of the most useful tools in a Hacker's
possession:

- [**Google**]{#e5b9}

**Google** is an incredibly useful tool, and there is an entire room
([Google Dorking
Room](https://tryhackme.com/room/googledorking){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/googledorking"
rel="noopener ugc nofollow noopener" target="_blank"}) to use it
effectively to conduct research.

You might have also used websites such as **Wikipedia** to understand
the history of SpaceX, used the company's **Twitter/YouTube** to see
their latest news releases or "sizzle-reels", or even **LinkedIn
profile** to research open company positions and/or the company's
organizational structure.

The cool thing is, all of these very simple tools are ***all valid
reconnaissance tools.***

*You might think hackers use special tools to conduct research (and in
some cases that is true), but overall they use simple tools like these
to conduct research.*

Reconnaissance usually involves using *publicly available* tools like
Google to conduct research about your target.

Even though it may seem simple, reconnaissance is the ***single most
important phase of a penetration test.***

**There are some specialized tools that we can utilize but for this
introduction it is good to know the following tools.**

- [**Google (specifically Google Dorking)**]{#033f}
- [**Wikipedia**]{#3d8e}
- [**PeopleFinder.com**]{#90fe}
- [**who.is**]{#7bd7}
- [**sublist3r**]{#2bf1}
- [**hunter.io**]{#631c}
- [**builtwith.com**]{#0423}
- [**wappalyzer**]{#c74f}

**Q.1** Who is the CEO of SpaceX?

> ***Answer: Elon Musk***

**Q.2** Do some research into the tool: sublist3r, what does it list?

> ***Answer: subdomains***

**Q.3** What is it called when you use Google to look for specific
vulnerabilities or to research a specific topic of interest?

> ***Answer: Google Dorking***

### Task 3: Enumeration and Scanning Overview {#3358 .graf .graf--h3 .graf-after--blockquote name="3358"}

**The second phase of the Hacker Methodology is Scanning and
Enumeration.**

This is where a hacker will start interacting with (scanning and
enumerating) the target to attempt to find vulnerabilities related to
the target.

**This is where more specialized tools start to come in to the
arsenal.** Tools like nmap, dirb, metasploit, exploit-db, Burp Suite and
others are very useful to help us try to find vulnerabilities in a
target. (Don't worry about them now, you can get into the nitty-gritty
later)

In the scanning and enumeration phase, the attacker is interacting with
the target to determine its overall **attack surface.**

**The attack surface determines what the target might be vulnerable to
in the Exploitation phase.** These vulnerabilities might be a range of
things: anything from a webpage not being properly locked down, a
website leaking information, SQL Injection, Cross Site Scripting or any
number of other vulnerabilities.

**To simplify --- the enumeration and scanning phase is where we will
try to determine WHAT the target might be vulnerable to.**

For example, one important tool in our arsenal is a tool called **Nmap**
(I recommmend checking out the [nmap
room](https://tryhackme.com/room/rpnmap){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/rpnmap"
rel="noopener ugc nofollow noopener" target="_blank"} after you finish
this room).

<figure id="bd11" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DY9SkUFN_z01ltE7.png"
class="graf-image" data-image-id="0*DY9SkUFN_z01ltE7.png"
data-width="500" data-height="250" />
</figure>

- [**Nmap is a tool which can scan a target and tell us a wide variety
  of things:**]{#aac0}
- [**What ports are open** (if you don't know anything about ports I
  highly recommend watching this:
  [https://www.youtube.com/watch?v=PpsEaqJV_A0](https://www.youtube.com/watch?v=PpsEaqJV_A0){.markup--anchor
  .markup--li-anchor
  data-href="https://www.youtube.com/watch?v=PpsEaqJV_A0"
  rel="noopener ugc nofollow noopener" target="_blank"} and
  [https://www.youtube.com/watch?v=qsZ8Qcm6_8k](https://www.youtube.com/watch?v=qsZ8Qcm6_8k){.markup--anchor
  .markup--li-anchor
  data-href="https://www.youtube.com/watch?v=qsZ8Qcm6_8k"
  rel="noopener ugc nofollow noopener" target="_blank"})]{#35fe}
- [**The operating system of the target** (Windows, Linux, MacOS, etc.
  including what version of the Operating System)]{#7014}
- [**What services are running and what version of the service** (for
  example, just saying FTP (File Transfer Protocol) isn't
  enough --- nmap can attempt to fingerprint and determine the exact
  VERSION of FTP which may enable us to find a specific vulnerability in
  the target)]{#ebc4}

Although that may sound like a lot of information (enough to pwn anyone
and anything, right?) there are other tools that will also be used in
the reconnaissance arsenal.

**Here is a quick sampling of other tools that you can learn on
TryHackMe:**

- [**dirb (used to find commonly-named directories on a website --- like
  how under**
  [**https://www.tesla.com**](https://www.tesla.com/){.markup--anchor
  .markup--li-anchor data-href="https://www.tesla.com/"
  rel="noopener ugc nofollow noopener" target="_blank"} **there is
  also**
  [https://www.tesla.com/about](https://www.tesla.com/about){.markup--anchor
  .markup--li-anchor data-href="https://www.tesla.com/about"
  rel="noopener ugc nofollow noopener" target="_blank"},
  [https://www.tesla.com/model3](https://www.tesla.com/model3){.markup--anchor
  .markup--li-anchor data-href="https://www.tesla.com/model3"
  rel="noopener ugc nofollow noopener" target="_blank"},
  [https://www.tesla.com/modely](https://www.tesla.com/modely){.markup--anchor
  .markup--li-anchor data-href="https://www.tesla.com/modely"
  rel="noopener ugc nofollow noopener" target="_blank"}, and most
  importantly
  [https://www.tesla.com/models](https://www.tesla.com/models){.markup--anchor
  .markup--li-anchor data-href="https://www.tesla.com/models"
  rel="noopener ugc nofollow noopener" target="_blank"} WITH LUDICROUS
  MODE!! ♥)]{#b816}
- [**dirbuster (similar to dirb but with a cooler name, and with a user
  interface)**]{#afaf}
- [**enum4linux (tool used specifically for Linux to find
  vulnerabilities)**]{#2c9f}
- [**metasploit (this tool is mostly used for exploitation, but it also
  has some built-in enumeration tools)**]{#7513}
- [**Burp Suite (this tool can be used to scan a website for
  subdirectories and to intercept network traffic)**]{#4c44}

**Q.1** What does enumeration help to determine about the target?

> ***Answer: attack surface***

**Q.2** Do some reconnaissance about the tool: Metasploit, what company
developed it?

> ***Answer: rapid7***

**Q.3** What company developed the technology behind the tool Burp
Suite?

> ***Answer: portswigger***

### Task 4: Exploitation {#4062 .graf .graf--h3 .graf-after--blockquote name="4062"}

Now that we have talked about the other three phases of a pentest, it is
time to talk about the one that is often portrayed as "the coolest".

In the news, they often talk about "this hack" or "this vulnerability"
but the truth is that usually the "exploitation" phase of a pentest is
not as glamorous as it seems. **The exploitation phase can only be as
good as the recon and enumeration phases before it, if you did not
enumerate all vulnerabilities you may miss an opportunity, or if you did
not look hard enough at the target --- the exploit you have chosen may
fail entirely!**

One common tool used for exploitation is called **Metasploit** which has
many built-in scripts to try to keep life simple.

<figure id="83f5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*utk6my2LQUmTyM8w.png"
class="graf-image" data-image-id="0*utk6my2LQUmTyM8w.png"
data-width="256" data-height="256" />
</figure>

You can also used tools like **Burp Suite** and **SQLMap** to exploit
web applications. There are tools such as **msfvenom (for building
custom payloads), BeEF (browser-based exploitation),** and many many
others.

<figure id="95cf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fTUcQEq6OAMeUOUf.png"
class="graf-image" data-image-id="0*fTUcQEq6OAMeUOUf.png"
data-width="506" data-height="254" />
</figure>

**TryHackMe** has a ton of rooms dedicated to learning the basics of
these tools, and I recommend learning from all of them!

For now, I think you have a good grasp on what "exploitation"
means --- just remember a professional penetration tester never jumps
into the exploitation phase without doing adequate **reconnaissance**
and **enumeration**.

**Q.1** What is one of the primary exploitation tools that pentester(s)
use?

> ***Answer: metasploit***

### Task 5: Privilege Escalation {#e799 .graf .graf--h3 .graf-after--blockquote name="e799"}

After we have gained access to a victim machine via the **exploitation**
phase, the next step is to **escalate privileges** to a higher user
account. The following accounts are what we try to reach as a pentester:

- [**In the Windows world, the target account is usually: Administrator
  or System.**]{#bed3}
- [**In the Linux world, the target account is usually: root**]{#b74f}

As you can tell, discovering what Operating System a device is running
on is very important to determine how we will escalate our privileges
later. Once we gain access as a lower level user, we will try to run
another exploit or find a way to become root or administrator.

**Privilege escalation can take many, many forms, some examples are:**

- [Cracking password hashes found on the target]{#7131}
- [Finding a vulnerable service or version of a service which will allow
  you to escalate privilege THROUGH the service]{#2347}
- [Password spraying of previously discovered credentials (password
  re-use)]{#3ec0}
- [Using default credentials]{#aed9}
- [Finding secret keys or SSH keys stored on a device which will allow
  pivoting to another machine]{#cbb2}
- [Running scripts or commands to enumerate system settings like
  'ifconfig' to find network settings, or the command 'find / -perm\
  -4000 -type f 2\>/dev/null' to see if the user has access to any
  commands they can run as root]{#c9d1}

These are just some examples of how privilege escalation could work and
there are many more ways in which a privilege escalation could take
place. Just think of this section of the methodology as getting to a
higher-level user account or pivoting to another machine with the
ultimate goal to "own" the machine.

**Q.1** In Windows what is usually the other target account besides
Administrator?

> ***Answer: system***

**Q.2** What thing related to SSH could allow you to login to another
machine (even without knowing the username or password)

> ***Answer: keys***

### Task 6: Reporting {#1b8b .graf .graf--h3 .graf-after--blockquote name="1b8b"}

The final phase of the pentest methodology is the reporting phase.

This is one of the most important phases where you will outline
everything that you found. **The reporting phase often includes the
following things:**

- [**The Finding(s) or Vulnerabilities**]{#76aa}
- [**The CRITICALITY of the Finding**]{#3762}
- [**A description or brief overview of how the finding was
  discovered**]{#15ea}
- [**Remediation recommendations to resolve the finding**]{#bdae}

The amount of reporting documentation varies widely by the type of
engagement that the pentester is involved in. A findings report
generally goes in three formats:

- [Vulnerability scan results (a simple listing of
  vulnerabilities)]{#10f3}
- [Findings summary (list of the findings as outlined above)]{#ede8}
- [Full formal report.]{#b4e9}

**As stated before there are many varying levels of documentation for a
final written report. Here is how each type of reporting would look in
practice:**

- [A vulnerability report usually looks like this:]{#efef}

<figure id="b0bb" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*z64rVBf4xLATgg7N.png"
class="graf-image" data-image-id="0*z64rVBf4xLATgg7N.png"
data-width="842" data-height="666" />
</figure>

- [A findings summary is usually something like this:]{#07ab}
- [**Finding:** SQL Injection in ID Parameter of Cats Page]{#bc81}
- [**Criticality: Critical**]{#8160}
- [**Description:** Placing a payload of *1\' OR '1'='1* into the ID
  parameter of the website allowed the viewing of all cat names in the
  cat Table of the database. Furthermore, a UNION SELECT SQL statement
  allowed the attacker to view all usernames and passwords stored in the
  Accounts table.]{#79e8}
- [**Remediation Recommendation:** Utilize a Prepared SQL statement to
  prevent SQL injection attacks]{#e672}
- [A full formal report sample can be found here:
  [https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report](https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report){.markup--anchor
  .markup--li-anchor
  data-href="https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report"
  rel="noopener ugc nofollow noopener" target="_blank"}**.**]{#7a0d}

The **CyberMentor** has a lot of other good content such as example
resumes, YouTube videos, and some really good Udemy courses
(http://udemy.com/course/practical-ethical-hacking/) that will take you
beyond the basics of this methodology outline.

**Q.1** What would be the type of reporting that involves a full
documentation of all findings within a formal document?

> ***Answer: full formal report***

**Q.2** What is the other thing that a pentester should provide in a
report beyond: the finding name, the finding description, the finding
criticality

> ***Answer: Remediation Recommendation***

### Promote and Collaborate on Cybersecurity Insights {#aff3 .graf .graf--h3 .graf-after--blockquote name="aff3"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#d16a .graf .graf--h3 .graf-after--p name="d16a"}

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
.h-card} on [August 23, 2024](https://medium.com/p/584edca63405).

[Canonical
link](https://medium.com/@bevijaygupta/the-hacker-methodology-tryhackme-writeup-584edca63405){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
