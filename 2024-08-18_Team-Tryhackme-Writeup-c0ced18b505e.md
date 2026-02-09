::: {}
# Team Tryhackme Writeup {#team-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/teamcw Note: This room is Free
:::

::::::: {.section .e-content field="body"}
:::::: {#388c .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Team Tryhackme Writeup {#bcf1 .graf .graf--h3 .graf--leading .graf--title name="bcf1"}

<figure id="07ac" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*vdsSmONqwcUl_TG-.png"
class="graf-image" data-image-id="0*vdsSmONqwcUl_TG-.png"
data-width="481" data-height="271" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/teamcw](https://tryhackme.com/room/teamcw){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/teamcw"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Enumeration {#9382 .graf .graf--h3 .graf-after--p name="9382"}

Add Target to /etc/hosts file

``` {#3257 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo "10.10.132.103      team.thm" >> /etc/hosts
```

<figure id="114b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*7pdBu7nzf-lVvn8t.png"
class="graf-image" data-image-id="0*7pdBu7nzf-lVvn8t.png"
data-width="588" data-height="458" />
</figure>

Open Ports is

FTP 21

SSH 22

**HTTP 80**

<figure id="e352" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CXWhdLjXX1xTvWmx.png"
class="graf-image" data-image-id="0*CXWhdLjXX1xTvWmx.png"
data-width="875" data-height="415" />
</figure>

### Gobuster {#4f00 .graf .graf--h3 .graf-after--figure name="4f00"}

``` {#3840 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://team.thm/ -w directory-list-2.3-medium.txt -x php,html,txt
```

<figure id="b95b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*0qCUfwgvnci1kTaP.png"
class="graf-image" data-image-id="0*0qCUfwgvnci1kTaP.png"
data-width="506" data-height="221" />
</figure>

Lets check robots.txt file

<figure id="fdb7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3KvJy8_wcUxSfnJ0.png"
class="graf-image" data-image-id="0*3KvJy8_wcUxSfnJ0.png"
data-width="383" data-height="94" />
</figure>

maybe its username but for what FTP Or SSH

**Subdomain Brute Force**

``` {#e1fc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
wfuzz -c --hw 977 -u http://team.thm -H "Host: FUZZ.team.thm" -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

<figure id="f20f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*L5DNsDCH8V0JhdzB.png"
class="graf-image" data-image-id="0*L5DNsDCH8V0JhdzB.png"
data-width="743" data-height="198" />
</figure>

Looking at the result from wfuzz we get one extra virtual host which i
added to my hosts file

<figure id="7056" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*g9Oe_qZG9y6tpnQl.png"
class="graf-image" data-image-id="0*g9Oe_qZG9y6tpnQl.png"
data-width="639" data-height="246" />
</figure>

And tried to navigating to the virtual host

<figure id="f1a2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fm9EFOgnTe1B7s_O.png"
class="graf-image" data-image-id="0*fm9EFOgnTe1B7s_O.png"
data-width="406" data-height="156" />
</figure>

Clicking on the place holder link we see that it uses some sort of
include to included the teamshare.php file

<figure id="6570" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jMP2bzl-iYR628jg.png"
class="graf-image" data-image-id="0*jMP2bzl-iYR628jg.png"
data-width="649" data-height="111" />
</figure>

Lets Chaeck **LFI vulnerability**

<figure id="b19a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*V5SsOGWCYSL1zW-n.png"
class="graf-image" data-image-id="0*V5SsOGWCYSL1zW-n.png"
data-width="697" data-height="304" />
</figure>

We now certain that the web application has a file inclusion
vulnerability. With this vulnerability two things comes in mind:

1.  [We may have to use that LFI vulnerability to get remote code
    execution though various methods eg. remote file inclusion, php
    wrappers(**expect://,php://input)** code execution, log poisoning,
    leaked phpinfo file etc.]{#6e5c}
2.  [Utilize this vulnerability to read some sensitive files that will
    lead to us compromising the box]{#b7e3}

Lets Try to Fetch **User.txt**

<figure id="be6d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*05vEL47ArZzrNiT2.png"
class="graf-image" data-image-id="0*05vEL47ArZzrNiT2.png"
data-width="704" data-height="109" />
</figure>

First i decided to run intruder(which is fuzzer build in to BurpSuite)
with a wordlist to check for common files on Linux systems

<figure id="ceed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NJckI9AbdrtjMY8M.png"
class="graf-image" data-image-id="0*NJckI9AbdrtjMY8M.png"
data-width="622" data-height="347" />
</figure>

The wordlist i used was from Seclists.

``` {#d95a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
SecLists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt
```

<figure id="1e94" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Q6DO1_75Sb358yms.png"
class="graf-image" data-image-id="0*Q6DO1_75Sb358yms.png"
data-width="532" data-height="533" />
</figure>

<figure id="d0f9" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*F-W1f4ePswdux-jz.png"
class="graf-image" data-image-id="0*F-W1f4ePswdux-jz.png"
data-width="572" data-height="555" />
</figure>

Without Burp Suite

``` {#59ad .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
curl "http://dev.team.thm/script.php?page=/etc/ssh/sshd_config"
```

<figure id="5266" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*rs1Qz4pDxtmVCwrs.png"
class="graf-image" data-image-id="0*rs1Qz4pDxtmVCwrs.png"
data-width="753" data-height="246" />
</figure>

We get a SSH private key for the user Dale.

I copied the key to my kali and edited to remove the pound signs and the
gave it the write permission using the command

``` {#a880 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
chmod 600 dale.key
ssh
```

And tried logging into the box using the key

<figure id="8c76" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6V2RAx1b0pdUT4Xs.png"
class="graf-image" data-image-id="0*6V2RAx1b0pdUT4Xs.png"
data-width="848" data-height="260" />
</figure>

### Privilege Escalation {#c48a .graf .graf--h3 .graf-after--figure name="c48a"}

Running sudo -l we see that we can run a particular bash script as the
user Gyles

<figure id="e5f5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0emAbypx27izPl3x.png"
class="graf-image" data-image-id="0*0emAbypx27izPl3x.png"
data-width="574" data-height="316" />
</figure>

Looking at the script we see that there are three possible places where
we can inject system commands on the script

Check the content of file **/home/gyles/admin_checks**

<figure id="ff43" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nKtR7YbKe9kigkmv.png"
class="graf-image" data-image-id="0*nKtR7YbKe9kigkmv.png"
data-width="600" data-height="371" />
</figure>

I'll be injecting in the error variable since we see that the variable
is directly passed to a system call

<figure id="d4ce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*E7JT-gUzygcnfgOK.png"
class="graf-image" data-image-id="0*E7JT-gUzygcnfgOK.png"
data-width="795" data-height="230" />
</figure>

now we have a shell as the gyles' user. Looking at the user's home
directory we see that the author left the .bash_history meaning we can
trace what the author did while he was creating the box

<figure id="401b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HYdc1i8mbAxSPDXO.png"
class="graf-image" data-image-id="0*HYdc1i8mbAxSPDXO.png"
data-width="725" data-height="331" />
</figure>

Looking through the file we see a file in /usr/local/share called
main_backup.sh being edited

``` {#f3d6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat .bash_history
```

<figure id="e2e5" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*9uriACpaEEtBYwK6.png"
class="graf-image" data-image-id="0*9uriACpaEEtBYwK6.png"
data-width="381" data-height="464" />
</figure>

We also see some mention of crontabs meaning there might be a cronjob
running

Looking at the file's permission we see that its only writable by root
and members in the admin group. And the gyles user is in the admin group
as seen in the screenshot below meaning we have access to modify the
file's contents

<figure id="4f3b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iibgs_uBnMj2PzM8.png"
class="graf-image" data-image-id="0*iibgs_uBnMj2PzM8.png"
data-width="791" data-height="134" />
</figure>

Looking at the file with a vim text editor we see that it's a bash
script that copies some backups i decided to edit the file and add a
reverse shell since i knew that there was a cronjob being executed

<figure id="b701" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3tgJoqWQWg3FKMLj.png"
class="graf-image" data-image-id="0*3tgJoqWQWg3FKMLj.png"
data-width="550" data-height="105" />
</figure>

Next i did set up a netcat listener

<figure id="f30b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yGtNpUrZWp8PdcGk.png"
class="graf-image" data-image-id="0*yGtNpUrZWp8PdcGk.png"
data-width="812" data-height="180" />
</figure>

BOOM ! We got root shell

<figure id="a59c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*k-sPP_E8HsqI2pHo.png"
class="graf-image" data-image-id="0*k-sPP_E8HsqI2pHo.png"
data-width="297" data-height="160" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#a570 .graf .graf--h3 .graf-after--figure name="a570"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#c7bc .graf .graf--h3 .graf-after--p name="c7bc"}

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
.h-card} on [August 18, 2024](https://medium.com/p/c0ced18b505e).

[Canonical
link](https://medium.com/@bevijaygupta/team-tryhackme-writeup-c0ced18b505e){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
