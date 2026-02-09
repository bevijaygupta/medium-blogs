::: {}
# Bebop Tryhackme Writeup {#bebop-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/bebop
:::

::::::: {.section .e-content field="body"}
:::::: {#828c .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Bebop Tryhackme Writeup {#22e5 .graf .graf--h3 .graf--leading .graf--title name="22e5"}

<figure id="ef02" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*NMRjhLKb-JH3Ulyf.png"
class="graf-image" data-image-id="0*NMRjhLKb-JH3Ulyf.png"
data-width="435" data-height="229" />
</figure>

**Room link:**
[https://tryhackme.com/room/bebop](https://tryhackme.com/room/bebop){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/bebop"
rel="noopener ugc nofollow noopener" target="_blank"}

**Note:** **This room is for Premium Members Only. who purchased THM
premium membership.**

Bebop is a quick box that exemplifies exactly how insecure some drone
operating systems are. This box shouldn't take very long to
root --- it's really not particularly challenging (which is slightly
worrying given it's based off real drone software). Of much more
interest is the overarching concept: drone hacking. If you haven't
already watched the video embedded into the THM room, I would highly
recommend it; it's really interesting (and hilarious in places). I'll
include an embed of the video below, before properly beginning the
write-up:

\<iframe width="704\" height="360\"
src="[https://www.youtube.com/embed/5CzURm7OpAA](https://www.youtube.com/embed/5CzURm7OpAA){.markup--anchor
.markup--p-anchor data-href="https://www.youtube.com/embed/5CzURm7OpAA"
rel="noopener ugc nofollow noopener" target="_blank"}\" frameborder="0\"
allow="accelerometer; autoplay; clipboard-write; encrypted-media;
gyroscope; picture-in-picture" allowfullscreen\>\</iframe\>

**Question 1**. What is your codename?

> ***Answer: pilot***

### Enumeration: {#e1a6 .graf .graf--h3 .graf-after--blockquote name="e1a6"}

As per normal, the first thing we're going to do with this box is run an
nmap scan. A basic service scan is more than enough for our purposes:

<figure id="d272" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*j5r6EAUO2dOH3snE.png"
class="graf-image" data-image-id="0*j5r6EAUO2dOH3snE.png"
data-width="721" data-height="379" />
</figure>

We have two ports open here: port 22 (SSH) and port 23 (telnet). These
two services do essentially the same thing (giving you the ability to
remotely access a command line on the machine), but SSH is significantly
more secure; so, funnily enough, we're trying telnet first.

### Exploitation: {#dcc5 .graf .graf--h3 .graf-after--p name="dcc5"}

At the start of the room we're given a codename: **pilot**. Let's try
logging in with that:

<figure id="2045" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QZM0IxJWQUsjsF1q.png"
class="graf-image" data-image-id="0*QZM0IxJWQUsjsF1q.png"
data-width="794" data-height="640" />
</figure>

Before we go any further, we can actually already answer three of the
four quiz questions. We logged in as ***pilot***, so it would make sense
for that to be the low privileged user. We logged in using ***telnet***,
so that's the answer to the third question. The answer to the fourth
question should be staring you in the face, but just to be sure, use the
**uname** command to find the OS:

<figure id="b4f6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gHundTIby-guZF7i.png"
class="graf-image" data-image-id="0*gHundTIby-guZF7i.png"
data-width="267" data-height="83" />
</figure>

The operating system is ***FreeBSD***.

Now the only quiz question left is the second one --- which we can only
get after we've escalated our privileges.

Before we start doing any privesc, let's grab the user flag which is in
pilot's home directory:

<figure id="2490" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0tCK53UMSnXUdebW.png"
class="graf-image" data-image-id="0*0tCK53UMSnXUdebW.png"
data-width="348" data-height="74" />
</figure>

### Privilege Escalation: {#3a65 .graf .graf--h3 .graf-after--figure name="3a65"}

Pretty much the first thing you usually do when aiming for privesc on a
Linux computer is look to see what you can run as sudo (i.e. with
Root/Administrator privileges). FreeBSD is no different. Run
`sudo -l`{.markup--code .markup--p-code} and see if we can run anything
as root:

<figure id="fe6f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GS_y7C5VnzIEztjA.png"
class="graf-image" data-image-id="0*GS_y7C5VnzIEztjA.png"
data-width="556" data-height="111" />
</figure>

We can run BusyBox as root. In case you haven't come across it before,
BusyBox essentially amalgamates lots of different functions into a
single executable file. It's often used in embedded systems to reduce
the disk space and memory required. Let's have a look to see which
commands we can execute through BusyBox on this system:

<figure id="38d6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pGlsWhE_KfCRPiyC.png"
class="graf-image" data-image-id="0*pGlsWhE_KfCRPiyC.png"
data-width="875" data-height="384" />
</figure>

Jackpot! Look in the third last line of the defined functions:

**sh** in defined functions list

We can run `sh`{.markup--code .markup--p-code} through BusyBox.
`sh`{.markup--code .markup--p-code} will give us a shell, meaning that
if we run BusyBox as root (which we can do with our sudo permissions),
*we get a root shell!*

``` {#4797 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo /usr/local/bin/busybox sh
```

<figure id="c9b0" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*CuEgUk4ymwAuES90.png"
class="graf-image" data-image-id="0*CuEgUk4ymwAuES90.png"
data-width="627" data-height="293" />
</figure>

And there we have it. We got root on a drone!

All that's left to do now is answer the last quiz question, and find the
root flag.

The quiz question should be pretty obvious. What binary was used to
escalate privileges? We've just done it: ***BusyBox***.

The root flag is equally easy to find. It's in the root directory, all
you need to do is open it:

### Quiz! {#924a .graf .graf--h3 .graf-after--p name="924a"}

**Question 1**. What is the low privilleged user?

> ***Answer: pilot***

**Question 2.** What binary was used to escalate privillages?

> ***Answer: busybox***

**Question 3.** What service was used to gain an initial shell?

> ***Answer: telnet***

**Question 4.** What Operating System does the drone run?

> ***Answer: FreeBSD***

### Promote and Collaborate on Cybersecurity Insights {#c250 .graf .graf--h3 .graf-after--blockquote name="c250"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#c9f2 .graf .graf--h3 .graf-after--p name="c9f2"}

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
.h-card} on [August 25, 2024](https://medium.com/p/482a90d9515f).

[Canonical
link](https://medium.com/@bevijaygupta/bebop-tryhackme-writeup-482a90d9515f){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
