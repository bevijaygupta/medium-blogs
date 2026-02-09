---
title: "Sniper Dz  The Phishing as a Service Platform Behind 140 000  Phishing Sites Exposed fb72464fb9d6"
platform: Medium
original_file: 2025-05-07_Sniper-Dz--The-Phishing-as-a-Service-Platform-Behind-140-000--Phishing-Sites-Exposed-fb72464fb9d6.md
---

# Sniper Dz  The Phishing as a Service Platform Behind 140 000  Phishing Sites Exposed fb72464fb9d6

::: {}
# Sniper Dz: The Phishing-as-a-Service Platform Behind 140,000+ Phishing Sites Exposed {#sniper-dz-the-phishing-as-a-service-platform-behind-140000-phishing-sites-exposed .p-name}
:::

::: {.section .p-summary field="subtitle"}
We have been monitoring a widely popular phishing-as-a-service (PhaaS)
platform named Sniper Dz that primarily targets popular social media...
:::

::::::: {.section .e-content field="body"}
:::::: {#cd6f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Sniper Dz: The Phishing-as-a-Service Platform Behind 140,000+ Phishing Sites Exposed {#b390 .graf .graf--h3 .graf--leading .graf--title name="b390"}

<figure id="6b22" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*BhVXRAiNIeCF-3QA.png"
class="graf-image" data-image-id="0*BhVXRAiNIeCF-3QA.png"
data-width="877" data-height="440" data-is-featured="true" />
</figure>

We have been monitoring a widely popular phishing-as-a-service (PhaaS)
platform named Sniper Dz that primarily targets popular social media
platforms and online services. A large number of phishers could be using
this platform to launch phishing attacks, since the group behind this
kit has thousands of subscribers on its Telegram channel. Our research
revealed over 140,000 phishing websites associated with the Sniper Dz
PhaaS platform over the past year.

For prospective phishers, Sniper Dz offers an online admin panel with a
catalog of phishing pages. Phishers can either host these phishing pages
on Sniper Dz-owned infrastructure or download Sniper Dz phishing
templates to host on their own servers. Surprisingly, Sniper Dz PhaaS
offers these services free of charge to phishers --- perhaps because
Sniper Dz also collects victim credentials stolen by phishers who use
the platform to compensate for the cost of service.

Sniper Dz uses a unique approach of hiding phishing content behind a
public proxy server to launch live phishing attacks. The criminals
behind this platform auto-setup the proxy server to load phishing
content that is hosted on their server. We believe this approach could
be useful in protecting their infrastructure from detection.

Criminals using Sniper Dz often abuse legitimate software-as-a-service
(SaaS) platforms to host phishing websites. When establishing their
infrastructure, these phishers include popular brand names, trends and
even sensitive topics as keywords to lure victims into opening and using
their phishing pages. After stealing credentials from a victim, this
infrastructure can redirect the victim to malicious advertisements
including distribution of potentially unwanted applications or programs
(PUA or PUP) like rogue browser installers.

If you think you might have been compromised or have an urgent matter,
contact the einitial24.com

### Sniper Dz PhaaS Platform {#a287 .graf .graf--h3 .graf-after--p name="a287"}

Sniper Dz is a PhaaS platform that allows prospective phishers to launch
phishing attacks. Sniper Dz offers an admin panel to generate phishing
pages.

Gaining access to this admin panel requires creating an account with an
email address. Once users (or phishers) create an account, they can
access a wide variety of phishing pages targeting popular brands.

Sniper Dz provides two different methods to launch live phishing
attacks.

1.  [Phishing pages hosted on Sniper Dz infrastructure]{#68b2}
2.  [Downloadable phishing templates to host on one's own
    infrastructure]{#de84}

### Phishing Pages Hosted on Sniper Dz Infrastructure {#c777 .graf .graf--h3 .graf-after--li name="c777"}

Sniper Dz can host phishing pages on its own infrastructure and provide
customized links pointed to those pages. Figure 1 shows the Sniper Dz
admin panel page that shares temporary links pointing to live phishing
pages for different brands customized for the registered user. In this
way, a prospective phisher does not have to set up a web server to host
phishing websites and use Sniper Dz's infrastructure to launch phishing
attacks.

<figure id="bbda" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*k8mfvZMTbmc7Rsps.png"
class="graf-image" data-image-id="0*k8mfvZMTbmc7Rsps.png"
data-width="2000" data-height="1630" />
</figure>

Content for these live phishing pages is hidden behind proxy servers to
prevent detection, which we will explain in more detail later in this
article.

### Downloadable Phishing Templates {#84f5 .graf .graf--h3 .graf-after--p name="84f5"}

Sniper Dz also enables phishers to download phishing page templates
offline as HTML files and host them on their own servers. Figure 2 shows
the page to download phishing templates of numerous target brands.
Prospective phishers can simply pick a target brand, download the
associated phishing page, and deploy it on their own servers.

<figure id="b4d5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jGmcmNjjiSz7Q-fM.png"
class="graf-image" data-image-id="0*jGmcmNjjiSz7Q-fM.png"
data-width="2000" data-height="1103" />
</figure>

### Is This Really a Free-of-Charge PhaaS Platform? {#c17f .graf .graf--h3 .graf-after--figure name="c17f"}

Surprisingly, Sniper Dz offers both phishing attack options free of
charge. Normally, PhaaS platforms and phishing kit authors charge money.
Setting up a live phishing attack using PhaaS platforms can cost
hundreds of dollars in monthly subscription fees, as seen with the
Caffeine PhaaS or the Darcula PhaaS.

Why does Sniper Dz provide PhaaS free of charge? Perhaps because Sniper
Dz collects victim credentials stolen by phishers who use their platform
to compensate for the cost of service.

Sniper Dz leaves a backdoor inside the phishing page for tracking and
collecting stolen credentials as we describe later in this article.
Providing this service for free allows Sniper Dz to register more
phishers and obtain more stolen credentials. There are no free lunches.

### Infrastructure and Tactics {#046a .graf .graf--h3 .graf-after--p name="046a"}

This section highlights key infrastructure and tactics employed by
Sniper Dz. We describe evasion tactics such as hiding phishing content
behind public proxy servers and obfuscating phishing content. We also
show how Sniper Dz uses a centralized infrastructure to collect victim
credentials stolen by other phishers and to track victims.

### Hiding Phishing Content Behind Public Proxy Servers {#c871 .graf .graf--h3 .graf-after--p name="c871"}

Sniper Dz abuses a legitimate public proxy server (proxymesh\[.\]com) to
hide its phishing content. Threat actors often abuse, take advantage of
or subvert legitimate products for malicious purposes. This does not
imply that the legitimate product is flawed or malicious.

The group behind Sniper Dz configures this proxy server to automatically
load phishing content from its own server without direct communications.
This technique can help Sniper Dz to protect its backend servers, since
the victim's browser or a security crawler will see the proxy server as
being responsible for loading the phishing payload.

Figure 3 shows how Sniper Dz uses a public proxy server to hide requests
to its web server (dev-cdn370\[.\]pantheonsite\[.\]io) hosting phishing
content. The entry point is a disposable decoy phishing page that
attackers could distribute to victims through emails or social media
platforms. When a victim opens this page, it returns a script to
automatically configure the proxy server.

<figure id="990f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QMEOi_447l7X8b4e.png"
class="graf-image" data-image-id="0*QMEOi_447l7X8b4e.png"
data-width="2000" data-height="936" />
</figure>

Figure 4 shows part of the HTML content of a decoy phishing page that
also includes this script to auto-configure the proxy server. The page
includes an HTTP POST request form to proxymesh\[.\]com/web/index.php.

<figure id="e158" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Tq-20nWVgfVKDdOm.png"
class="graf-image" data-image-id="0*Tq-20nWVgfVKDdOm.png"
data-width="2000" data-height="1469" />
</figure>

This form mimics the request to load an input URL using a proxy provided
by proxymesh\[.\]com. The JavaScript code snippet at the bottom assigns
the "url" field of this form to the location of the phishing content,
then it auto-submits the form to request content from the specified URL.

Eventually, the proxy server loads content from the web server hosting
phishing content. As a result, the victim browser loads the phishing
content through the proxy server without initiating a request to the web
server hosting the phishing content. To detect such backend web servers
hiding behind public proxy servers, defenders need to extract
destination URLs by analyzing the scripts on the phishing pages.

To the best of our knowledge, we are the first to report this behavior
of hiding backend server hosting phishing content behind public proxy
servers.

### Obfuscating Phishing Template Code {#8c29 .graf .graf--h3 .graf-after--p name="8c29"}

The contents of phishing template pages are heavily obfuscated. Figure 5
shows code from an example of a phishing page with obfuscated JavaScript
to render the HTML script.

<figure id="c363" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EKkvXGRNT1iaGNFF.png"
class="graf-image" data-image-id="0*EKkvXGRNT1iaGNFF.png"
data-width="1872" data-height="1178" />
</figure>

For example, it uses String.fromCharCode and unescape functions that we
find attackers commonly use for obfuscating content. This obfuscation
allows it to hide HTML code and critical infrastructure endpoints like
the exfiltration URL.

### Centralized Infrastructure to Exfiltrate Credentials {#4b43 .graf .graf--h3 .graf-after--p name="4b43"}

These phishing pages exfiltrate credentials to a centralized
infrastructure that Sniper Dz owns. Figure 6 shows a Google Chrome
debugger console view of the exfiltration URL raviral\[.\]com/k_fac.php
where email and password are exfiltrated in parameters email and pass.

<figure id="0e87" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8vx3-9C_fAFoJuz9.png"
class="graf-image" data-image-id="0*8vx3-9C_fAFoJuz9.png"
data-width="2000" data-height="1334" />
</figure>

By exfiltrating credentials to a centralized infrastructure it owns,
Sniper Dz can harvest credentials from all of its clients' victims,
including those who fell prey to its phishing templates hosted on other
servers.

For phishers, stolen credentials of victims are displayed on the admin
panel as shown in Figure 7. The admin panel shows the following
information from the time the credentials were exfiltrated:

- [Username]{#c0aa}
- [Password]{#c91d}
- [Template name]{#bba4}
- [Date and time]{#6fb3}
- [Victim's IP address and country]{#6215}

<figure id="538c" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*7fLslMfWa-VsP7e0.png"
class="graf-image" data-image-id="0*7fLslMfWa-VsP7e0.png"
data-width="2000" data-height="1309" />
</figure>

### Tracking Victims and Phishing Templates {#b85a .graf .graf--h3 .graf-after--figure name="b85a"}

Sniper Dz tracks its victims by embedding custom JavaScript and
analytics services. Figure 8 shows a custom tracking script for
raviral\[.\]com/host_style/style/js-track/track.js included on a
phishing page.

<figure id="8ae9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8hM5WarenvwHSC6u.png"
class="graf-image" data-image-id="0*8hM5WarenvwHSC6u.png"
data-width="1738" data-height="766" />
</figure>

This script in turn loads a tracker from a legitimate analytics service.
We surmise that these scripts allow Sniper Dz to track victims that
visit both PhaaS links hosted on Sniper Dz infrastructure as well as
offline phishing templates hosted by phishers on their own
infrastructure.

### Phishing Attacks Using Sniper Dz {#4eb8 .graf .graf--h3 .graf-after--p name="4eb8"}

Since last year, we have discovered over 140,000 phishing webpages
associated with the Sniper Dz PhaaS platform. Figure 9 shows the
discovery of these websites since July 2023.

<figure id="e110" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IFaH9T3Bfuoz9Xxa.png"
class="graf-image" data-image-id="0*IFaH9T3Bfuoz9Xxa.png"
data-width="2000" data-height="814" />
</figure>

Sniper Dz has remained active throughout this period. While its activity
peaked in late 2023, we observed a surge in their activity starting in
July 2024. Geographically, these phishing websites primarily target web
users in the US.

Sniper Dz could have thousands of phishers as customers who are using
its PhaaS platform to launch these phishing attacks. For example, Sniper
Dz operates a Telegram channel t\[.\]me/JokerDzV2 for customer support
that had 7,156 subscribers in August 2024 as shown in Figure 10.

<figure id="4857" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LiqjsXFpVLFqiIN4.png"
class="graf-image" data-image-id="0*LiqjsXFpVLFqiIN4.png"
data-width="1012" data-height="1062" />
</figure>

In fact, one of the tutorial videos on this Telegram channel at

- [t\[.\]me/JokerDzV2/19]{#af79}

had 72,600 views in August 2024 as shown in Figure 10. A large number of
Telegram channel subscribers and video views indicate that a substantial
number of prospective phishers could be using the Sniper Dz PhaaS
platform.

<figure id="aa68" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8SnwIMrUX0VCU1bb.png"
class="graf-image" data-image-id="0*8SnwIMrUX0VCU1bb.png"
data-width="1124" data-height="800" />
</figure>

### Abusing Legitimate SaaS Platforms to Launch Phishing Attacks {#6906 .graf .graf--h3 .graf-after--figure name="6906"}

Most of the Sniper Dz phishing pages we have detected are hosted on
legitimate SaaS platforms. Attackers commonly target legitimate SaaS
platforms because the good reputation of legitimate domains can help
threat actors evade detection from security crawlers. Blogspot was the
most popular target among legitimate SaaS platforms.

Blogspot appears to be more popular because the Sniper Dz admin panel
offers an easy way to convert phishing templates to the Blogger format
as shown below in Figure 12. Sniper Dz also provides a tutorial guide to
enter converted phishing pages into Blogger for hosting on Blogspot.

<figure id="ec5e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Y6aCZh3FLzYsidbx.png"
class="graf-image" data-image-id="0*Y6aCZh3FLzYsidbx.png"
data-width="482" data-height="1000" />
</figure>

### Using Brand Names or Trends/Events as Keywords in Hostnames {#f448 .graf .graf--h3 .graf-after--figure name="f448"}

Sniper Dz authored phishing pages use keywords in hostnames that match
popular brand names and trends or events, including sensitive political
events. These deceptive hostnames can lure victims to these phishing
pages and fall prey to phishing attacks.

### Malicious Redirects and PUP Distribution {#1038 .graf .graf--h3 .graf-after--p name="1038"}

Sniper Dz phishing pages can redirect users to other Sniper Dz owned
websites like raviral\[.\]com after a victim is fooled into giving away
login credentials. Attackers proliferate the raviral\[.\]com website
with malicious advertisements and distribute PUA/PUP-like, suspiciously
labeled ad blockers and other browser extensions.

During one of our test runs, the website triggered download of an
installer for a rogue browser named Artificus as shown in Figure 13.
Artificus is known for its intrusive behavior and we have also reported
on it for being distributed by malicious advertisers.

<figure id="db91" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9YtIZtHVnb-GA3fK.png"
class="graf-image" data-image-id="0*9YtIZtHVnb-GA3fK.png"
data-width="2000" data-height="1139" />
</figure>

### Conclusion {#a3d7 .graf .graf--h3 .graf-after--figure name="a3d7"}

This article provides an in-depth investigation of an online PhaaS
platform named Sniper Dz. Our study finds that a large number of
phishers could be using this platform. We have discovered 140,000
phishing websites in the past year that we can attribute to this PhaaS.

We describe a unique technique employed by Sniper Dz to hide backend
servers hosting phishing content behind public proxy servers. This
technique allows Sniper Dz to protect its hosting infrastructure from
security crawlers. Sniper Dz also uses more commonly known techniques to
evade detections such as obfuscating phishing content and abusing
legitimate SaaS platforms to host phishing pages.

We also found that Sniper Dz phishing pages exfiltrate victim
credentials and track them through a centralized infrastructure. This
could be helping Sniper Dz collect victim credentials stolen by phishers
who use their PhaaS platform.

We hope this blog helps our readers to stay protected from the harmful
effects of this phishing campaign.

### Indicators of Compromise {#5680 .graf .graf--h3 .graf-after--p name="5680"}

Sniper Dz PhaaS Platform:

- [Sniperdz\[.\]com]{#9a66}

Physical location of phishing webpages concealed using proxy servers:

- [dev-cdn370.pantheonsite.io]{#6a8f}

Centralized exfiltration endpoint:

- [raviral\[.\]com/k_fac.php]{#36b6}

Embedded tracker script:

- [raviral\[.\]com/host_style/style/js-track/track.js]{#b696}

Telegram support channel:

- [t\[.\]me/JokerDzV2]{#8b90}

Sniper Dz platform tutorial video:

- [t\[.\]me/JokerDzV2/19]{#9bb2}

Redirection to Sniper Dz-owned websites:

- [raviral\[.\]com]{#a05a}

Examples of phishing websites generated using Sniper Dz:

- [6627c220b5daa507c6cca1c5 --- votedme\[.\]netlify.app]{#f7b9}
- [automaticgiveaway\[.\]000webhostapp\[.\]com]{#05ee}
- [Climbing-green-botany\[.\]glitch\[.\]me]{#137d}
- [facebookbusiness0078\[.\]blogspot.be]{#e103}
- [free-fire-reward-garena-bd-nepazl\[.\]epizy\[.\]com]{#b032}
- [freefirefff\[.\]github\[.\]io]{#7d45}
- [ff-rewards-redeem-codes-org\[.\]github.io]{#7a82}
- [instagram-cutequeen57\[.\]netlify.app]{#4b8b}
- [pubg-tournament-official\[.\]github.io/free-fire-reedeem-code]{#993c}
- [v0tingsystem\[.\]github\[.\]io]{#94eb}

Examples of Sniper Dz Live phishing pages hosted on their own
infrastructure:

- [pro\[.\]riccardomalisano\[.\]com/about/z1to.html?u=ff-insta/?i=\[Redacted_For_Anonymity\]]{#7fd5}
- [pro\[.\]riccardomalisano\[.\]com/about/z2to.html?u=ff-reward/?i=\[Redacted_For_Anonymity\]]{#2003}
- [pro\[.\]riccardomalisano\[.\]com/about/z2to.html?u=ff-spiner/?i=\[Redacted_For_Anonymity\]]{#667e}
- [pro\[.\]riccardomalisano\[.\]com/about/z1to.html?u=eb-log/?i=\[Redacted_For_Anonymity\]]{#823e}
- [pro\[.\]riccardomalisano\[.\]com/about/z1to.html?u=s-mobi/?i=\[Redacted_For_Anonymity\]]{#2df8}

Legitimate public proxy service abused to hide phishing content:

- [proxymesh\[.\]com]{#c2ef}

### Promote and Collaborate on Cybersecurity Insights {#0361 .graf .graf--h3 .graf-after--li name="0361"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#2d3c .graf .graf--h3 .graf-after--p name="2d3c"}

[Vijay
Gupta](https://www.youtube.com%2F@www.youtube.com/@bevijaygupta){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com%2F@www.youtube.com/@bevijaygupta"
rel="noopener ugc nofollow noopener" target="_blank"} is a cybersecurity
enthusiast with several years of experience in cyber security, [cyber
crime forensics
investigation](https://play.google.com/store/books/series?id=_vUpHAAAABDW6M){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/series?id=_vUpHAAAABDW6M"
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
.h-card} on [May 7, 2025](https://medium.com/p/fb72464fb9d6).

[Canonical
link](https://medium.com/@bevijaygupta/sniper-dz-the-phishing-as-a-service-platform-behind-140-000-phishing-sites-exposed-fb72464fb9d6){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
