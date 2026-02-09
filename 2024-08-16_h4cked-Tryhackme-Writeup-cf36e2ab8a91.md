::: {}
# h4cked Tryhackme Writeup {#h4cked-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Hacked"
:::

::::::: {.section .e-content field="body"}
:::::: {#70ef .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### h4cked Tryhackme Writeup {#a451 .graf .graf--h3 .graf--leading .graf--title name="a451"}

**This is a Writeup of Tryhackme room "Hacked"**

<figure id="a233" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8ndtXONB2hVRtCLI.png"
class="graf-image" data-image-id="0*8ndtXONB2hVRtCLI.png"
data-width="423" data-height="252" data-is-featured="true" />
</figure>

**Room link:**
[https://www.tryhackme.com/room/h4cked](https://www.tryhackme.com/room/h4cked){.markup--anchor
.markup--p-anchor data-href="https://www.tryhackme.com/room/h4cked"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

**Q.1:** The attacker is trying to log into a specific service. What
service is this?

<figure id="000a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*f8JpYEumtPjXhqzA.png"
class="graf-image" data-image-id="0*f8JpYEumtPjXhqzA.png"
data-width="502" data-height="108" />
</figure>

> ***Answer: FTP***

**Q.2:** There is a very popular tool by Van Hauser which can be used to
brute force a series of services. What is the name of this tool?

<figure id="9bb7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Mzb2-64VNvbqKPW5.png"
class="graf-image" data-image-id="0*Mzb2-64VNvbqKPW5.png"
data-width="500" data-height="103" />
</figure>

> ***Answer: Hydra***

**Q.3:** The attacker is trying to log on with a specific username. What
is the username?

<figure id="031a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Txa4vKxNQqdXgXaa.png"
class="graf-image" data-image-id="0*Txa4vKxNQqdXgXaa.png"
data-width="496" data-height="105" />
</figure>

<figure id="298f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*kZV0Z1bvkn_o_6v6.png"
class="graf-image" data-image-id="0*kZV0Z1bvkn_o_6v6.png"
data-width="875" data-height="283" />
</figure>

> ***Answer: jenny***

**Q.4:** What is the user's password?

<figure id="8093" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CrfV3EUdAwfDflCG.png"
class="graf-image" data-image-id="0*CrfV3EUdAwfDflCG.png"
data-width="875" data-height="489" />
</figure>

<figure id="27d4" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Fq4h0ezNmx5wFP_w.png"
class="graf-image" data-image-id="0*Fq4h0ezNmx5wFP_w.png"
data-width="643" data-height="184" />
</figure>

**Q.5:** What is the current FTP working directory after the attacker
logged in?

<figure id="e0cf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*O98V74hx9wa38cxM.png"
class="graf-image" data-image-id="0*O98V74hx9wa38cxM.png"
data-width="875" data-height="258" />
</figure>

> ***Answer: /var/www/html***

**Q.6:** The attacker uploaded a backdoor. What is the backdoor's
filename?

<figure id="5988" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GTOgw4850rB17Yo9.png"
class="graf-image" data-image-id="0*GTOgw4850rB17Yo9.png"
data-width="501" data-height="391" />
</figure>

> ***Answer: shell.php***

**Q.7:** The backdoor can be downloaded from a specific URL, as it is
located inside the uploaded file. What is the full URL?

<figure id="87b9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OogNRzH9Td5PiJHi.png"
class="graf-image" data-image-id="0*OogNRzH9Td5PiJHi.png"
data-width="496" data-height="103" />
</figure>

<figure id="2a88" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*-JfCgCU7j7JHqdpn.png"
class="graf-image" data-image-id="0*-JfCgCU7j7JHqdpn.png"
data-width="632" data-height="519" />
</figure>

> ***Answer:***
> [***http://pentestmonkey.net/tools/php-reverse-shell***](http://pentestmonkey.net/tools/php-reverse-shell){.markup--anchor
> .markup--blockquote-anchor
> data-href="http://pentestmonkey.net/tools/php-reverse-shell"
> rel="noopener ugc nofollow noopener" target="_blank"}

**Q.8:** Which command did the attacker manually execute after getting a
reverse shell?

<figure id="792f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*c7dvkltx4GFgLFLN.png"
class="graf-image" data-image-id="0*c7dvkltx4GFgLFLN.png"
data-width="875" data-height="235" />
</figure>

> ***Answer: whoami***

**Q.9:** What is the computer's hostname?

<figure id="6ca9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*H0GkzzHObehr2nXU.png"
class="graf-image" data-image-id="0*H0GkzzHObehr2nXU.png"
data-width="187" data-height="67" />
</figure>

> ***Answer: wir3***

**Q.10:** Which command did the attacker execute to spawn a new TTY
shell?

<figure id="f170" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*97h6dZf43CRtksn-.png"
class="graf-image" data-image-id="0*97h6dZf43CRtksn-.png"
data-width="408" data-height="98" />
</figure>

> ***Answer: python3 -c 'import pty; pty.spawn("/bin/bash")'***

**Q.11:** Which command was executed to gain a root shell?

<figure id="e7e8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vGvudZHDfkMOm1Gs.png"
class="graf-image" data-image-id="0*vGvudZHDfkMOm1Gs.png"
data-width="196" data-height="98" />
</figure>

> ***Answer: sudo su***

**Q.11:** The attacker downloaded something from GitHub. What is the
name of the GitHub project?

<figure id="d6c2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*n1Yp5cxlpY9lALqY.png"
class="graf-image" data-image-id="0*n1Yp5cxlpY9lALqY.png"
data-width="505" data-height="76" />
</figure>

> ***Answer: Reptile***

**Q.12:** The project can be used to install a stealthy backdoor on the
system. It can be very hard to detect. What is this type of backdoor
called?

> ***Answer: rootkit***

Deploy the machine.

The attacker has changed the user's password! Can you replicate the
attacker's steps and read the flag.txt? The flag is located in the
/root/Reptile directory. Remember, you can always look back at the .pcap
file if necessary. Good luck!

Run Hydra (or any similar tool) on the FTP service. The attacker might
not have chosen a complex password. You might get lucky if you use a
common word list.

<figure id="2260" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UzWRjO2EWOcyRrK-.png"
class="graf-image" data-image-id="0*UzWRjO2EWOcyRrK-.png"
data-width="713" data-height="321" />
</figure>

We got password now login into ftp server

<figure id="6c7d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FVpGWu8U-cmCgW-f.png"
class="graf-image" data-image-id="0*FVpGWu8U-cmCgW-f.png"
data-width="696" data-height="372" />
</figure>

upload our new shell.php with our tryhackme ip address

<figure id="9f05" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eZ2KeyMH8EmqliE1.png"
class="graf-image" data-image-id="0*eZ2KeyMH8EmqliE1.png"
data-width="440" data-height="414" />
</figure>

<figure id="1f3e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*z3FUbiw9gYCalrbH.png"
class="graf-image" data-image-id="0*z3FUbiw9gYCalrbH.png"
data-width="692" data-height="292" />
</figure>

Now start netcat listener on kali

``` {#ec91 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvp 4444
```

and visit
[http://10.10.82.175/shell.php](http://10.10.82.175/shell.php){.markup--anchor
.markup--p-anchor data-href="http://10.10.82.175/shell.php"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="3ae6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6HEuGerLcVaSu881.png"
class="graf-image" data-image-id="0*6HEuGerLcVaSu881.png"
data-width="730" data-height="200" />
</figure>

<figure id="0ee6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*gXkQtPhJT6P1n1cD.png"
class="graf-image" data-image-id="0*gXkQtPhJT6P1n1cD.png"
data-width="661" data-height="262" />
</figure>

and we get revershell

**Upgrade shell**

``` {#ec22 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

<figure id="eff3" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*yHVO-yceyIFaiQeN.png"
class="graf-image" data-image-id="0*yHVO-yceyIFaiQeN.png"
data-width="523" data-height="221" />
</figure>

Boom! We got root shell Lets get the flag.txt

<figure id="1568" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gKSVj0MP4545AkW7.png"
class="graf-image" data-image-id="0*gKSVj0MP4545AkW7.png"
data-width="526" data-height="330" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#5ab2 .graf .graf--h3 .graf-after--figure name="5ab2"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#378a .graf .graf--h3 .graf-after--p name="378a"}

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
.h-card} on [August 16, 2024](https://medium.com/p/cf36e2ab8a91).

[Canonical
link](https://medium.com/@bevijaygupta/h4cked-tryhackme-writeup-cf36e2ab8a91){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
