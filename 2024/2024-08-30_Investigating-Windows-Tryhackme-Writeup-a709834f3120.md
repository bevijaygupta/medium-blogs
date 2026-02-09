---
title: "Investigating Windows Tryhackme Writeup a709834f3120"
platform: Medium
original_file: 2024-08-30_Investigating-Windows-Tryhackme-Writeup-a709834f3120.md
---

# Investigating Windows Tryhackme Writeup a709834f3120

::: {}
# Investigating Windows Tryhackme Writeup {#investigating-windows-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/investigatingwindows
:::

::::::: {.section .e-content field="body"}
:::::: {#63b1 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Investigating Windows Tryhackme Writeup {#cd22 .graf .graf--h3 .graf--leading .graf--title name="cd22"}

<figure id="0d4a" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*aJca5bl3LDDcjkgU.png"
class="graf-image" data-image-id="0*aJca5bl3LDDcjkgU.png"
data-width="612" data-height="226" data-is-featured="true" />
</figure>

[https://tryhackme.com/room/investigatingwindows](https://tryhackme.com/room/investigatingwindows){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/investigatingwindows"
rel="noopener ugc nofollow noopener" target="_blank"}

**Room link:**
[https://tryhackme.com/room/investigatingwindows](https://tryhackme.com/room/investigatingwindows){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/investigatingwindows"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

This is a challenge that is exactly what is says on the tin, there are a
few challenges around investigating a windows machine that has been
previously compromised.

Connect to the machine using RDP. The credentials the machine are as
follows:

Username: Administrator\
Password: letmein123!

<figure id="7e1e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PBj8DoV3bpU3zLj2.png"
class="graf-image" data-image-id="0*PBj8DoV3bpU3zLj2.png"
data-width="875" data-height="123" />
</figure>

**Question 1**. Whats the version and year of the windows machine?

<figure id="ca1a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WPVVFhHJ2EeLmQZt.png"
class="graf-image" data-image-id="0*WPVVFhHJ2EeLmQZt.png"
data-width="602" data-height="210" />
</figure>

> ***Answer: Windows server 2016***

**Question 2.** Which user logged in last?

> ***Answer: administrator***

**Question 3.** When did John log onto the system last?

Answer format: MM/DD/YYYY H:MM:SS AM/PM

<figure id="1f11" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kJp7lQSn8VeiFwPm.png"
class="graf-image" data-image-id="0*kJp7lQSn8VeiFwPm.png"
data-width="502" data-height="425" />
</figure>

> ***Answer: 03/02/2019 5:48:32 PM***

**Question 4**. What IP does the system connect to when it first starts?

<figure id="d488" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hmUidO7qS-xfDKo7.png"
class="graf-image" data-image-id="0*hmUidO7qS-xfDKo7.png"
data-width="576" data-height="222" />
</figure>

> ***Answer:10.34.2.3***

**Question 5.** What two accounts had administrative privileges (other
than the Administrator user)?

Answer format: username1, username2

Open run command using Ctrl+R and type **lusrmgr.msc**

<figure id="7add" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LmaA7O9O9fjIvxg1.png"
class="graf-image" data-image-id="0*LmaA7O9O9fjIvxg1.png"
data-width="748" data-height="409" />
</figure>

> ***Answer: Jenny, Guest***

**Question 6.** Whats the name of the scheduled task that is malicous.

> ***Answer:Clean file system***

**Question 7.** What file was the task trying to run daily?

<figure id="26dd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6lozGfC1onZKHJDv.png"
class="graf-image" data-image-id="0*6lozGfC1onZKHJDv.png"
data-width="838" data-height="423" />
</figure>

> ***Answer: nc.ps1***

**Question 8.** What port did this file listen locally for?

<figure id="94d2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cv-nrmK5pN29KH5p.png"
class="graf-image" data-image-id="0*cv-nrmK5pN29KH5p.png"
data-width="875" data-height="467" />
</figure>

> ***Answer: 1348***

**Question 9.** When did Jenny last logon?

> ***Answer: never***

**Question 10.** At what date did the compromise take place?

Answer format: MM/DD/YY

> ***Answer: 03/02/2019***

**Question 11.** At what time did Windows first assign special
privileges to a new logon?

Answer format: MM/DD/YYYY HH:MM:SS AM/PM

<figure id="a5df" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NwsQ1vIbAXa2GQSC.png"
class="graf-image" data-image-id="0*NwsQ1vIbAXa2GQSC.png"
data-width="580" data-height="330" />
</figure>

> ***Answer: 03/02/2019 4:04:49 PM***

**Question 12.** What tool was used to get Windows passwords?

> ***Answer: Mimikatz***

**Question 13.** What was the attackers external control and command
servers IP?

<figure id="145c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bpfglh3XoWF95AYl.png"
class="graf-image" data-image-id="0*bpfglh3XoWF95AYl.png"
data-width="875" data-height="367" />
</figure>

> ***Answer: 76.32.97.132***

**Question 14.** What was the extension name of the shell uploaded via
the servers website?

> ***Answer: .jsp***

**Question 15.** What was the last port the attacker opened?

<figure id="b2bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4L8D43n08Ql3rfbz.png"
class="graf-image" data-image-id="0*4L8D43n08Ql3rfbz.png"
data-width="875" data-height="214" />
</figure>

> ***Answer: 1337***

**Question 16.** Check for DNS poisoning, what site was targeted?

<figure id="674c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hrptt3No2vG62jaR.png"
class="graf-image" data-image-id="0*hrptt3No2vG62jaR.png"
data-width="875" data-height="367" />
</figure>

> ***Answer: google.com***

### Promote and Collaborate on Cybersecurity Insights {#55ea .graf .graf--h3 .graf-after--blockquote name="55ea"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#76fb .graf .graf--h3 .graf-after--p name="76fb"}

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
.h-card} on [August 30, 2024](https://medium.com/p/a709834f3120).

[Canonical
link](https://medium.com/@bevijaygupta/investigating-windows-tryhackme-writeup-a709834f3120){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
