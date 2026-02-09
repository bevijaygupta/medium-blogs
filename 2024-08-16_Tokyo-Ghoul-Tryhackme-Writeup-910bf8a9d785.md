::: {}
# Tokyo Ghoul Tryhackme Writeup {#tokyo-ghoul-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Tokyo Ghoul"
:::

::::::: {.section .e-content field="body"}
:::::: {#2c52 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Tokyo Ghoul Tryhackme Writeup {#ef22 .graf .graf--h3 .graf--leading .graf--title name="ef22"}

**This is a Writeup of Tryhackme room "Tokyo Ghoul"**

<figure id="4d45" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*P3Oz1-8J1mrkpZib.png"
class="graf-image" data-image-id="0*P3Oz1-8J1mrkpZib.png"
data-width="498" data-height="283" data-is-featured="true" />
</figure>

**Room link:**
[https://www.tryhackme.com/room/tokyoghoul666](https://www.tryhackme.com/room/tokyoghoul666){.markup--anchor
.markup--p-anchor
data-href="https://www.tryhackme.com/room/tokyoghoul666"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Enumeration {#f759 .graf .graf--h3 .graf-after--p name="f759"}

<figure id="30e1" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*BBGQ8l94J1vXq-GC.png"
class="graf-image" data-image-id="0*BBGQ8l94J1vXq-GC.png"
data-width="548" data-height="407" />
</figure>

<figure id="3820" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*5OdFler9yP0zd_Fx.png"
class="graf-image" data-image-id="0*5OdFler9yP0zd_Fx.png"
data-width="634" data-height="240" />
</figure>

So We have 3 ports

FTP-21 anonymous login allowed

SSH-22

HTTP-80

**Q.1:** How many ports are open ?

> ***Answer: 3***

**Q.2:** What is the OS used ?

> ***Answer: ubuntu***

**Q.3:** Did you find the note that the others ghouls gave you? where
did you find it ?

<figure id="51cb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cdzFvA8FkOn5zTmk.png"
class="graf-image" data-image-id="0*cdzFvA8FkOn5zTmk.png"
data-width="802" data-height="308" />
</figure>

> ***Answer: jasonroom.html***

Log into FTP server

<figure id="30e0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NlBUGoCGexBgAZA1.png"
class="graf-image" data-image-id="0*NlBUGoCGexBgAZA1.png"
data-width="663" data-height="404" />
</figure>

Download these files

<figure id="53e3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vU2ATUayBUOn0dou.png"
class="graf-image" data-image-id="0*vU2ATUayBUOn0dou.png"
data-width="720" data-height="525" />
</figure>

Lets check these files

<figure id="670a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ICuomJdKllfISDEG.png"
class="graf-image" data-image-id="0*ICuomJdKllfISDEG.png"
data-width="766" data-height="192" />
</figure>

The file wait for a paraphrase , lets try any string as password to
check what it will return in output. so its says use "**rabina2 -z"** to
pull it

<figure id="98fc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cRh6BKclpAkonptI.png"
class="graf-image" data-image-id="0*cRh6BKclpAkonptI.png"
data-width="821" data-height="298" />
</figure>

Boom it show me password of file. lets use password

<figure id="7b03" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EM-DqPOjzPJX_6mw.png"
class="graf-image" data-image-id="0*EM-DqPOjzPJX_6mw.png"
data-width="761" data-height="187" />
</figure>

The program gaved us another string i think this is the password of the
picture so i used steghide

<figure id="c855" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1N4wyoDrTeLdUyVY.png"
class="graf-image" data-image-id="0*1N4wyoDrTeLdUyVY.png"
data-width="520" data-height="284" />
</figure>

This is morsecode lets decode it

<figure id="1d5d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*y-unJS1Sf7jfhJuo.png"
class="graf-image" data-image-id="0*y-unJS1Sf7jfhJuo.png"
data-width="624" data-height="279" />
</figure>

the morsecode give us hex string lets decode it

<figure id="9cf1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3XmpAMDaWELabElC.png"
class="graf-image" data-image-id="0*3XmpAMDaWELabElC.png"
data-width="571" data-height="379" />
</figure>

[http://string-functions.com/hex-string.aspx](http://string-functions.com/hex-string.aspx){.markup--anchor
.markup--p-anchor
data-href="http://string-functions.com/hex-string.aspx"
rel="noopener ugc nofollow noopener" target="_blank"}

The hex string give us base64 string lets decode it

<figure id="4d38" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Gyua3Tg4IoItdcEa.png"
class="graf-image" data-image-id="0*Gyua3Tg4IoItdcEa.png"
data-width="452" data-height="81" />
</figure>

We found hidden directory Lets visit hidden directory

``` {#d75c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
http://10.10.59.18/**********/
```

<figure id="55ad" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*zgiCSJPo94TpHb4o.png"
class="graf-image" data-image-id="0*zgiCSJPo94TpHb4o.png"
data-width="875" data-height="438" />
</figure>

### dirb {#9ca2 .graf .graf--h3 .graf-after--figure name="9ca2"}

<figure id="29e7" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*4ah6TbC4J2PvaRRJ.png"
class="graf-image" data-image-id="0*4ah6TbC4J2PvaRRJ.png"
data-width="561" data-height="346" />
</figure>

we found another subdirectory

<figure id="e18d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*mXOpGDQh6ksRD3GW.png"
class="graf-image" data-image-id="0*mXOpGDQh6ksRD3GW.png"
data-width="875" data-height="472" />
</figure>

after clicking on "**yes"** i saw this parameter who call a file in the
server

index.php?view=flower.gif

maybe we can change it to get back and get the /etc/passwd

<figure id="b30b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DF-3aE16kNSsh8nQ.png"
class="graf-image" data-image-id="0*DF-3aE16kNSsh8nQ.png"
data-width="718" data-height="179" />
</figure>

but we know now that there is a vulnerability there so we need to bypass
it using html url encoding

``` {#4dd6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
?view=%2F%2E%2E%2F%2E%2E%2F%2E%2E%2Fetc%2Fpasswd
```

<figure id="3e75" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*FmyuoEEQ7W4pHlax.png"
class="graf-image" data-image-id="0*FmyuoEEQ7W4pHlax.png"
data-width="807" data-height="484" />
</figure>

Boom we got the /etc/passwd with a username:**kamishiro** and a hash ,
i'll crack this hash using john

first thing we put the hash in a file

<figure id="a2f7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aQ2EgGwA3IpNGDjz.png"
class="graf-image" data-image-id="0*aQ2EgGwA3IpNGDjz.png"
data-width="563" data-height="301" />
</figure>

Now we have ssh credential

**SSH and User.txt**

``` {#0c47 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh kamishiro@10.10.59.18
```

<figure id="debb" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*dUYD9Xe97MakwxNl.png"
class="graf-image" data-image-id="0*dUYD9Xe97MakwxNl.png"
data-width="615" data-height="147" />
</figure>

### Privillage esculation {#97cf .graf .graf--h3 .graf-after--figure name="97cf"}

<figure id="edd7" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*MKBcaCNFKvdR2uol.png"
class="graf-image" data-image-id="0*MKBcaCNFKvdR2uol.png"
data-width="616" data-height="200" />
</figure>

we have access as root to execute jail.py , so let's see what is this

<figure id="918a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hfzdi1N5EVcULZWX.png"
class="graf-image" data-image-id="0*hfzdi1N5EVcULZWX.png"
data-width="814" data-height="333" />
</figure>

the script won't let us execute commands who read internal files and we
can'nt edit this file , we should escape this to read the root flag
using [using Built-in
functions](https://docs.python.org/3/library/functions.html){.markup--anchor
.markup--p-anchor
data-href="https://docs.python.org/3/library/functions.html"
rel="noopener ugc nofollow noopener" target="_blank"}:

``` {#b2e5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="less"}
__builtins__.__dict__['__IMPORT__'.lower()]('OS'.lower()).__dict__['SYSTEM'.lower()]('cat /root/root.txt')
```

<figure id="1cdd" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*d5TMK6gn6sf6scS4.png"
class="graf-image" data-image-id="0*d5TMK6gn6sf6scS4.png"
data-width="825" data-height="177" />
</figure>

Boom ! we got root flag

### Promote and Collaborate on Cybersecurity Insights {#9f1e .graf .graf--h3 .graf-after--p name="9f1e"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#fa60 .graf .graf--h3 .graf-after--p name="fa60"}

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
.h-card} on [August 16, 2024](https://medium.com/p/910bf8a9d785).

[Canonical
link](https://medium.com/@bevijaygupta/tokyo-ghoul-tryhackme-writeup-910bf8a9d785){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
