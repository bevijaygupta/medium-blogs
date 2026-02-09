::: {}
# HeartBleed TryHackme Walkthrough {#heartbleed-tryhackme-walkthrough .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/heartbleed Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#e294 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### HeartBleed TryHackme Walkthrough {#9aae .graf .graf--h3 .graf--leading .graf--title name="9aae"}

<figure id="cb52" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*-Dqd3clAZGjZ-S-w.png"
class="graf-image" data-image-id="0*-Dqd3clAZGjZ-S-w.png"
data-width="514" data-height="226" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/heartbleed](https://tryhackme.com/room/heartbleed){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/heartbleed"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

***Description:***

​SSL issues are still lurking in the wild. Can you exploit this web
servers OpenSSL?

***Related Hosting Links***

- [TryHackMe:]{#9541}
- [Hosted as a subscriber only room at the time of writing.]{#7515}
- [Link:
  [https://tryhackme.com/room/heartbleed](https://tryhackme.com/room/heartbleed){.markup--anchor
  .markup--li-anchor data-href="https://tryhackme.com/room/heartbleed"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#e823}

Once the machine is deployed, let's go ahead and scan it with nmap

``` {#0a7e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sV --script vuln 52.209.186.169
```

<figure id="4704" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*pS0uTRoK46dkaMz4.png"
class="graf-image" data-image-id="0*pS0uTRoK46dkaMz4.png"
data-width="796" data-height="314" />
</figure>

The namp scan shows us that there is ssl-heartbleed Vulnerability here

Let's Try to find module in metasploit

``` {#6529 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
service postgresql start
```

<figure id="a35a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*dBy-eN6uSkGyx7R6.png"
class="graf-image" data-image-id="0*dBy-eN6uSkGyx7R6.png"
data-width="567" data-height="363" />
</figure>

Looks like there is! Let's go ahead and select it for use and check what
options we have to set

<figure id="17a9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fry3SgObpsJq9i6T.png"
class="graf-image" data-image-id="0*fry3SgObpsJq9i6T.png"
data-width="656" data-height="613" />
</figure>

Just need to set RHOST (Remote host) and verbose, let's go ahead and set
those!

<figure id="0d8f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BIC-fscTYmLYh7k3.png"
class="graf-image" data-image-id="0*BIC-fscTYmLYh7k3.png"
data-width="763" data-height="132" />
</figure>

<figure id="85c0" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*e9YE0_mAmHmEqjUx.png"
class="graf-image" data-image-id="0*e9YE0_mAmHmEqjUx.png"
data-width="822" data-height="131" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#b2ec .graf .graf--h3 .graf-after--figure name="b2ec"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#7e45 .graf .graf--h3 .graf-after--p name="7e45"}

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
.h-card} on [September 1, 2024](https://medium.com/p/37bf9c6d2041).

[Canonical
link](https://medium.com/@bevijaygupta/heartbleed-tryhackme-walkthrough-37bf9c6d2041){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
