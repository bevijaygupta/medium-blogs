::: {}
# Intro to ISAC TryHackme {#intro-to-isac-tryhackme .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction:-
:::

::::::: {.section .e-content field="body"}
:::::: {#c09f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Intro to ISAC TryHackme {#ac75 .graf .graf--h3 .graf--leading .graf--title name="ac75"}

<figure id="e794" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*QnP4_XxP6Q2ElQLM.png"
class="graf-image" data-image-id="0*QnP4_XxP6Q2ElQLM.png"
data-width="697" data-height="232" />
</figure>

### Introduction:- {#9773 .graf .graf--h3 .graf-after--figure name="9773"}

Threat Intelligence, also known as TI and Cyber Threat Intelligence also
known as, CTI, is used to provide information about the threat landscape
specifically adversaries and their TTPs. Typically CTI revolves around
APT groups and/or other threats, these can be well-known groups or up
and coming new threats.

Data must be analyzed to be considered threat intelligence. Once
analyzed and actionable, then it becomes threat intelligence. The data
needs context around to become intel.

CTI is a precautionary measure that companies use or contribute to so
that other corporations do not get hit with the same attacks. Of course,
adversaries change their TTPs all the time so the TI landscape is
constantly changing.

### What are ISACs {#4887 .graf .graf--h3 .graf-after--p name="4887"}

According to the National Council of ISACs, "Information Sharing and
Analysis Centers (ISACs) are member-driven organizations, delivering
all-hazards threat and mitigation information to asset owners and
operators". ISACs can be community-centered or vendor-specific. ISACs
include CTI from threat actors as well as mitigation information in the
form of IOCs, YARA rules, etc. ISACs maintain situational awareness by
sharing and collaborating to maintain CTI, through a [National Council
of ISACs](https://www.nationalisacs.org/){.markup--anchor
.markup--p-anchor data-href="https://www.nationalisacs.org/"
rel="noopener ugc nofollow noopener" target="_blank"}.

Below is a list of ISACs that can help a blue team we will only be
showcasing a few in this room.

- [[**US-CERT**](https://us-cert.cisa.gov/){.markup--anchor
  .markup--li-anchor data-href="https://us-cert.cisa.gov/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#40c5}
- [[**AlienVault OTX**](https://otx.alienvault.com/){.markup--anchor
  .markup--li-anchor data-href="https://otx.alienvault.com/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#ac6a}
- [[**ThreatConnect**](https://threatconnect.com/){.markup--anchor
  .markup--li-anchor data-href="https://threatconnect.com/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#cb17}
- [[**MISP**](https://www.misp-project.org/){.markup--anchor
  .markup--li-anchor data-href="https://www.misp-project.org/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#9038}

This room will specifically focus on AlienVault OTX and ThreatConnect;
however, there are many more ISACs that can be used to gather threat
intelligence. I encourage you to go out and research others on your own
to get a good feeling for what you like and what various ISACs can
offer.

### Scenario 1 {#cd92 .graf .graf--h3 .graf-after--p name="cd92"}

Your incident response team has quarantined a suspicious bin file. The
team thinks it is a ransomware variation. Investigate and create
indicators for the file.

You can find the shellcode
*C:\\Users\\Jon\\Documents\\Scenarios\\Scenario 1*

### Scenario 2 {#6b17 .graf .graf--h3 .graf-after--p name="6b17"}

You have been assigned to analyze this week's quarantined files. The
file is thought to be an unknown trojan or a new strain of the emotet
malware. Investigate and create indicators for the file.

You can find the shellcode
*C:\\Users\\Jon\\Documents\\Scenarios\\Scenario 2*

username:**jon** , password: **alqfna22**

``` {#3689 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
xfreerdp /u:"jon" /p:alqfna22 /v:10.10.26.213
```

Run this command in your Terminal to start RDP

<figure id="24f1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1D-WO_tAUPCjAPxP.png"
class="graf-image" data-image-id="0*1D-WO_tAUPCjAPxP.png"
data-width="875" data-height="398" />
</figure>

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

Question 1. What is the name of the file from Scenario 1?

<figure id="b852" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6JxyqnzbVMFhRUXW.png"
class="graf-image" data-image-id="0*6JxyqnzbVMFhRUXW.png"
data-width="805" data-height="451" />
</figure>

> *Answer:* ***29D6161522C7F7F21B35401907C702BDDB05ED47.bin***

Question 2. What is the size of the file from Scenario 1 in bytes?

<figure id="0c9d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fD5NgHUffrKHqeIS.png"
class="graf-image" data-image-id="0*fD5NgHUffrKHqeIS.png"
data-width="374" data-height="472" />
</figure>

> *Answer:* ***96,535***

Question 3. What is the size on disk of the file from Scenario 1 in
bytes?

<figure id="c246" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*W42kKt_sU7Xz-gWX.png"
class="graf-image" data-image-id="0*W42kKt_sU7Xz-gWX.png"
data-width="374" data-height="472" />
</figure>

> *Answer:* ***98,304***

Question 4. What is the MD5 hash of the file from Scenario 1?

Open WinMD5 tool and select Scenario 1 file

<figure id="f760" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*V4UviW--gYBah8Mp.png"
class="graf-image" data-image-id="0*V4UviW--gYBah8Mp.png"
data-width="801" data-height="594" />
</figure>

> *Answer:*
> ***8b\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*6a***

Question 5. What is the name of the file from Scenario 2?

<figure id="777d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sl7BOLKHveY2kEto.png"
class="graf-image" data-image-id="0*sl7BOLKHveY2kEto.png"
data-width="813" data-height="428" />
</figure>

> *Answer:* ***cryptowall.bin***

Question 6. What is the size of the file from Scenario 2 in bytes?

<figure id="9ddc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*voQkZWub7duFiyD5.png"
class="graf-image" data-image-id="0*voQkZWub7duFiyD5.png"
data-width="373" data-height="472" />
</figure>

> *Answer:* ***246,272***

Question 7. What is the size on disk of the file from Scenario 2 in
bytes?

<figure id="3e24" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pg6pxcoVNbF61O7Z.png"
class="graf-image" data-image-id="0*pg6pxcoVNbF61O7Z.png"
data-width="373" data-height="472" />
</figure>

> *Answer:* ***249,856***

Question 8. What is the MD5 hash of the file from Scenario 2?

Now again click on WinMD5 tool and select cryptowall.bin file

<figure id="9277" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ezpaLNisyztuMuA5.png"
class="graf-image" data-image-id="0*ezpaLNisyztuMuA5.png"
data-width="798" data-height="478" />
</figure>

> *Answer:*
> ***47\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*c7***

### Promote and Collaborate on Cybersecurity Insights {#ea81 .graf .graf--h3 .graf-after--blockquote name="ea81"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#aa76 .graf .graf--h3 .graf-after--p name="aa76"}

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
.h-card} on [September 7, 2024](https://medium.com/p/6c57d40f42d0).

[Canonical
link](https://medium.com/@bevijaygupta/intro-to-isac-tryhackme-6c57d40f42d0){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
