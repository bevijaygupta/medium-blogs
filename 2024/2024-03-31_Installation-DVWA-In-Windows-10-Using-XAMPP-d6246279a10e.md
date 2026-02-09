---
title: "Installation DVWA In Windows 10 Using XAMPP d6246279a10e"
platform: Medium
original_file: 2024-03-31_Installation-DVWA-In-Windows-10-Using-XAMPP-d6246279a10e.md
---

# Installation DVWA In Windows 10 Using XAMPP d6246279a10e

::: {}
# Installation DVWA In Windows 10 Using XAMPP {#installation-dvwa-in-windows-10-using-xampp .p-name}
:::

::: {.section .p-summary field="subtitle"}
How To Setup DVWA In Windows 10 Using XAMPP
:::

::::::: {.section .e-content field="body"}
:::::: {#a7ac .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Installation DVWA In Windows 10 Using XAMPP {#f207 .graf .graf--h3 .graf--leading .graf--title name="f207"}

### **How To Setup DVWA In Windows 10 Using XAMPP** {#4ce8 .graf .graf--h3 .graf-after--h3 name="4ce8"}

Before, installation of DVWA we need to what is DVWA and why we use
DVWA?\
Damn Vulnerable Web Application (DVWA) is a PHP/MySQL web application
that is damn vulnerable. Its main goal is to be an aid for security
professionals to test their skills and tools in a legal environment,
help web developers better understand the processes of securing web
applications, and to aid both students & teachers to learn about web
application security in a controlled classroom environment.

The aim of DVWA is to practice some of the most common web
vulnerabilities, with various levels of difficulty, with a simple
straightforward interface. Please note, there are both documented and
undocumented vulnerabilities with this software. This is intentional.
You are encouraged to try and discover as many issues as possible.

Download DVWA
\>[http://www.dvwa.co.uk/](http://www.dvwa.co.uk/){.markup--anchor
.markup--p-anchor data-href="http://www.dvwa.co.uk/" rel="noopener"
target="_blank"}\
Download and install XAMPP on your computer

XAMPP is a free and open-source cross-platform web server solution stack
package developed by Apache Friends, consisting mainly of the Apache
HTTP Server, MariaDB database, and interpreters for scripts written in
the PHP and Perl programming languages

Download Link
\>[https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html){.markup--anchor
.markup--p-anchor
data-href="https://www.apachefriends.org/download.html" rel="noopener"
target="_blank"}

Open XAMPP and start 'Apache and MySQL'

<figure id="c6ad" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*81SASXuyS07ndAi2.png"
class="graf-image" data-image-id="0*81SASXuyS07ndAi2.png"
data-width="619" data-height="402" data-is-featured="true" />
</figure>

Extract DVWA downloaded file in htdocs that will be available in
C:\\xampp

<figure id="3400" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RrDfiyP0F0uLXZZQ.png"
class="graf-image" data-image-id="0*RrDfiyP0F0uLXZZQ.png"
data-width="564" data-height="420" />
</figure>

Open htdocs folder and rename 'DVWA-master' to 'dvwa'

And Open your Browser then type 127.0.0.1/dvwa. It will show this type
of error "DVWA System error --- config file not found. Copy
config/config.inc.php.dist to config/config.inc.php and configure to
your environment."

<figure id="4e7c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*--CoPtuWOFAAyiq0.png"
class="graf-image" data-image-id="0*--CoPtuWOFAAyiq0.png"
data-width="611" data-height="60" />
</figure>

A filename 'config.inc.php.dist ' rename it to 'config.inc.php' it will
be available in C:\\xampp\\htdocs\\dvwa\\config

<figure id="e827" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SxZKMqgd0-tKjIzR.png"
class="graf-image" data-image-id="0*SxZKMqgd0-tKjIzR.png"
data-width="611" data-height="63" />
</figure>

Now, again type '127.0.0.1/dvwa' in url of the browser,

<figure id="721e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JXSOb6fAq5xoTDwv.png"
class="graf-image" data-image-id="0*JXSOb6fAq5xoTDwv.png"
data-width="605" data-height="323" />
</figure>

<figure id="626a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*X3fuiLdN6BeGhFNI.png"
class="graf-image" data-image-id="0*X3fuiLdN6BeGhFNI.png"
data-width="596" data-height="184" />
</figure>

Click on 'Create/Reset Database'

<figure id="7320" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*unrdKvt91TLdBJGA.png"
class="graf-image" data-image-id="0*unrdKvt91TLdBJGA.png"
data-width="334" data-height="111" />
</figure>

It will show this type of error\
Now, you need to edit the config file that you rename earlier step,

Then open it by Notepad and in the password tab, clear the password or
make the password empty by remove the default password and give the
username as root. (its user database user id, password).

<figure id="94ad" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-uujfmHIbZGk-VRY.png"
class="graf-image" data-image-id="0*-uujfmHIbZGk-VRY.png"
data-width="607" data-height="219" />
</figure>

Now , again click on 'Create / Reset Database'

<figure id="fdcd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xC8aeI8z0BFBhxdx.png"
class="graf-image" data-image-id="0*xC8aeI8z0BFBhxdx.png"
data-width="599" data-height="186" />
</figure>

You will see this type of output,

<figure id="99a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YSxTqhTH8TXfaIbI.png"
class="graf-image" data-image-id="0*YSxTqhTH8TXfaIbI.png"
data-width="606" data-height="403" />
</figure>

Click on 'Login' or it will automatically redirect to login page,

<figure id="5906" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KCvGYAdJM9Dtaz6E.png"
class="graf-image" data-image-id="0*KCvGYAdJM9Dtaz6E.png"
data-width="497" data-height="407" />
</figure>

The default username is 'admin' and password is 'password'.

<figure id="aeae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qXNLiKiOcdHOv1F-.png"
class="graf-image" data-image-id="0*qXNLiKiOcdHOv1F-.png"
data-width="601" data-height="415" />
</figure>

**Great**, you successfully installed DVWA in your windows 10.

### About the Author: {#6faf .graf .graf--h3 .graf-after--p name="6faf"}

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
.h-card} on [March 31, 2024](https://medium.com/p/d6246279a10e).

[Canonical
link](https://medium.com/@bevijaygupta/installation-dvwa-in-windows-10-using-xampp-d6246279a10e){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
