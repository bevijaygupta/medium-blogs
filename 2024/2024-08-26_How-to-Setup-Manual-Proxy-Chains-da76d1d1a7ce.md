::: {}
# How to Setup Manual Proxy Chains {#how-to-setup-manual-proxy-chains .p-name}
:::

::: {.section .p-summary field="subtitle"}
How To Setup Manual Proxychains
:::

::::::: {.section .e-content field="body"}
:::::: {#9fbd .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### How to Setup Manual Proxy Chains {#9d44 .graf .graf--h3 .graf--leading .graf--title name="9d44"}

<figure id="1c2b" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*sgUA0_Ei3k2Hj1ew.jpg"
class="graf-image" data-image-id="0*sgUA0_Ei3k2Hj1ew.jpg"
data-width="640" data-height="360" data-is-featured="true" />
</figure>

### How To Setup Manual Proxychains {#54d4 .graf .graf--h3 .graf-after--figure name="54d4"}

**Proxy Server** --- the proxy server is a server application that goes
about as a delegate between a client requesting an asset and the server
giving that asset. It uses to hide the real identity on the internet.

<figure id="2733" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BZIq2i9znofJVyuP.png"
class="graf-image" data-image-id="0*BZIq2i9znofJVyuP.png"
data-width="788" data-height="443" />
</figure>

working of the proxy server**proxychains** --- Proxychains is an
open-source tool for Linux frameworks and comes pre-installed with Kali
Linux, the device diverts TCP connections through intermediaries like
TOR, SOCKS4, SOCKS5, and HTTP (S) and it permits us to chain proxy
servers. With proxychains, we can shroud the IP address of the source
traffic and keep away from IDS and firewalls.

<figure id="b6a3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*e-EPor2LipbOoFJq.jpg"
class="graf-image" data-image-id="0*e-EPor2LipbOoFJq.jpg"
data-width="788" data-height="443" />
</figure>

working of the proxychains**Tor **--- Tor stands for The Onion Router.
It is an open-source tool for hiding your real identity. And maintain
anonymity. Tor is developed by the United States Naval Research
Laboratory employees, mathematician Paul Syverson, and computer
scientists Michael G. Reed and David Goldschlag. The reason for the
development of the TOR is to protect U.S. intelligence online
communications.

<figure id="a685" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YZLaRwn4-WSR6g6s.png"
class="graf-image" data-image-id="0*YZLaRwn4-WSR6g6s.png"
data-width="788" data-height="476" />
</figure>

**How to install TOR?**

Step 1: Switch to ROOT user

su

<figure id="e71c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NKRN-AVxZqyeLEfw.png"
class="graf-image" data-image-id="0*NKRN-AVxZqyeLEfw.png"
data-width="265" data-height="95" />
</figure>

Step 2: installing TOR

apt-get install tor

<figure id="a8b1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9DQyuFi3iKzXXds-.png"
class="graf-image" data-image-id="0*9DQyuFi3iKzXXds-.png"
data-width="507" data-height="129" />
</figure>

If TOR Successfully installs then, Start the TOR service. with "service"
command

Step 3: Start TOR service

service tor start

<figure id="c7d1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*b9GdTOZeIaqPr2cM.png"
class="graf-image" data-image-id="0*b9GdTOZeIaqPr2cM.png"
data-width="253" data-height="62" />
</figure>

Step 4: check the TOR service status

service tor status

<figure id="58c4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dElL8wUeSkTPsKZd.png"
class="graf-image" data-image-id="0*dElL8wUeSkTPsKZd.png"
data-width="788" data-height="203" />
</figure>

**Configure proxy chains**

Step 4: open "proxychains.conf" file which is present in "etc" folder

nano /etc/proxychains.conf

<figure id="cc03" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LYlVi20DDQFNIfPl.png"
class="graf-image" data-image-id="0*LYlVi20DDQFNIfPl.png"
data-width="648" data-height="894" />
</figure>

Step 5: Remove comment from Dynamic chain

<figure id="13f6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YZoQjF2iVwtPHHo_.png"
class="graf-image" data-image-id="0*YZoQjF2iVwtPHHo_.png"
data-width="498" data-height="208" />
</figure>

Step 6: Add comment to Strict chain and Random chain

<figure id="f2c6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nwoxq1hFafQUnXuS.png"
class="graf-image" data-image-id="0*nwoxq1hFafQUnXuS.png"
data-width="502" data-height="240" />
</figure>

Step 7: Remove comment from Proxy DNS requests

<figure id="d58f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*afj-5iVXxMMChIaF.png"
class="graf-image" data-image-id="0*afj-5iVXxMMChIaF.png"
data-width="349" data-height="49" />
</figure>

Step 8: write **socks5 127.0.0.1 9050** in the last line of the proxy
list

<figure id="506b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EWJTdoQxyMZiinyS.png"
class="graf-image" data-image-id="0*EWJTdoQxyMZiinyS.png"
data-width="200" data-height="112" />
</figure>

Step 9: Press **Ctrl + O** to save the file and press **Ctrl + x** to
exit the nano editor

Step 10: Restart the TOR

service tor restart

<figure id="5d22" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pVxySXQSBZogynD5.png"
class="graf-image" data-image-id="0*pVxySXQSBZogynD5.png"
data-width="261" data-height="54" />
</figure>

Now you can run any tool with proxychain just typing "proxychains"
before the tool name

proxychains firefox bing.com

<figure id="c7b8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OP-tUYbFD0ub0yzn.png"
class="graf-image" data-image-id="0*OP-tUYbFD0ub0yzn.png"
data-width="788" data-height="304" />
</figure>

**Note**: --- You can check DNS leaks just visit the website
dnsleaktest.com

### Promote and Collaborate on Cybersecurity Insights {#1cab .graf .graf--h3 .graf-after--p name="1cab"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#6f27 .graf .graf--h3 .graf-after--p name="6f27"}

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
.h-card} on [August 26, 2024](https://medium.com/p/da76d1d1a7ce).

[Canonical
link](https://medium.com/@bevijaygupta/how-to-setup-manual-proxy-chains-da76d1d1a7ce){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
