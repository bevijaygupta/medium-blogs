---
title: "Baron Samedit Tryhackme Writeup 2da96185e5dc"
platform: Medium
original_file: 2024-08-23_Baron-Samedit-Tryhackme-Writeup-2da96185e5dc.md
---

# Baron Samedit Tryhackme Writeup 2da96185e5dc

::: {}
# Baron Samedit Tryhackme Writeup {#baron-samedit-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/sudovulnssamedit Note: This room
is free
:::

::::::: {.section .e-content field="body"}
:::::: {#bdd0 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Baron Samedit Tryhackme Writeup {#8d67 .graf .graf--h3 .graf--leading .graf--title name="8d67"}

<figure id="a957" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZORGVX_z1bDMgAXV.png"
class="graf-image" data-image-id="0*ZORGVX_z1bDMgAXV.png"
data-width="470" data-height="259" data-is-featured="true" />
</figure>

**Room link:**
[**https://tryhackme.com/room/sudovulnssamedit**](https://tryhackme.com/room/sudovulnssamedit){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/sudovulnssamedit"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

In January 2021, [Qualys](https://qualys.com/){.markup--anchor
.markup--p-anchor data-href="https://qualys.com/"
rel="noopener ugc nofollow noopener" target="_blank"} released a [blog
post](https://blog.qualys.com/vulnerabilities-research/2021/01/26/cve-2021-3156-heap-based-buffer-overflow-in-sudo-baron-samedit){.markup--anchor
.markup--p-anchor
data-href="https://blog.qualys.com/vulnerabilities-research/2021/01/26/cve-2021-3156-heap-based-buffer-overflow-in-sudo-baron-samedit"
rel="noopener ugc nofollow noopener" target="_blank"} detailing a
terrifying new vulnerability in the Unix sudo program.

Specifically, this was a heap buffer overflow allowing any user to
escalate privileges to root --- no misconfigurations required. This
exploit works with the default settings, for any user regardless of sudo
permissions, which makes it all the scarier. The vulnerability has been
patched, but affects any unpatched version of the sudo program from
1.8.2--1.8.31p2 and 1.9.0--1.9.5p1, meaning that it's been around for
the last ten years.

The program was very quickly patched (with patched versions making their
way into repositories soon after), so this exploit will no longer work
on up-to-date targets; however, it is still incredibly powerful.

As with **CVE-2019--18634** (which we saw in the [**second sudovulns
room**](https://tryhackme.com/room/sudovulnsbof){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/sudovulnsbof"
rel="noopener ugc nofollow noopener" target="_blank"}**),** this
vulnerability is a buffer overflow in the sudo program; however, this
time the vulnerability is a *heap* buffer overflow, as opposed to the
*stack* buffer overflow we saw before. The stack is a very regimented
section of memory which stores various important aspects of a program.
The heap, on the other hand, is reserved for dynamic allocation of
memory, allowing for more flexibility in how values and constructs are
created and accessed by a program. As with the previous room, we will
not go into a huge amount of detail about how this works in the
interests of keeping the content beginner friendly. All we really need
to understand is that this vulnerability is incredibly powerful, and
extremely wide-reaching

login over SSH using these credentials:

- [**Username:** tryhackme]{#1178}
- [**Password:** tryhackme]{#c391}

The command will be:\
**ssh tryhackme@10.10.231.160**

<figure id="5f7a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kuBhAPEcfjQEbt-9.png"
class="graf-image" data-image-id="0*kuBhAPEcfjQEbt-9.png"
data-width="820" data-height="410" />
</figure>

**Question 1**. After compiling the exploit, what is the name of the
executable created

<figure id="fc12" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4oU_qmoGEkFLUgEj.png"
class="graf-image" data-image-id="0*4oU_qmoGEkFLUgEj.png"
data-width="709" data-height="300" />
</figure>

> ***Answer: sudo-hax-me-a-sandwich***

now let's run exploit

<figure id="bcc3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kSHRA0mw4H2k_s0m.png"
class="graf-image" data-image-id="0*kSHRA0mw4H2k_s0m.png"
data-width="730" data-height="340" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#2f5b .graf .graf--h3 .graf-after--figure name="2f5b"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#c083 .graf .graf--h3 .graf-after--p name="c083"}

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
.h-card} on [August 23, 2024](https://medium.com/p/2da96185e5dc).

[Canonical
link](https://medium.com/@bevijaygupta/baron-samedit-tryhackme-writeup-2da96185e5dc){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
