---
title: "The Great Escape Tryhackme Writeup 0dd289a1ae17"
platform: Medium
original_file: 2024-08-24_The-Great-Escape-Tryhackme-Writeup-0dd289a1ae17.md
---

# The Great Escape Tryhackme Writeup 0dd289a1ae17

::: {}
# The Great Escape Tryhackme Writeup {#the-great-escape-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "The Great Escape"
:::

::::::: {.section .e-content field="body"}
:::::: {#b81f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### The Great Escape Tryhackme Writeup {#15e0 .graf .graf--h3 .graf--leading .graf--title name="15e0"}

**This is a Writeup of Tryhackme room "The Great Escape"**

<figure id="c4e6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2xZg4fOucs_j-d04.png"
class="graf-image" data-image-id="0*2xZg4fOucs_j-d04.png"
data-width="490" data-height="256" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/malstrings](https://tryhackme.com/room/malstrings){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malstrings"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Docker, Networks, and Container Escapes; Oh My! {#8255 .graf .graf--h3 .graf-after--p name="8255"}

I wanted to explore the concept of a Docker Escape. Docker is an
extremely useful tool which allows us to isolate applications from each
other and the host OS without having to resort to virtual machines.
Properly configured it can be very secure, though miscommunications can
introduce massive security holes, which we shall soon see.

### Enumeration {#5800 .graf .graf--h3 .graf-after--p name="5800"}

<figure id="2153" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*-H2YQVjyX4cib_KA.png"
class="graf-image" data-image-id="0*-H2YQVjyX4cib_KA.png"
data-width="418" data-height="250" />
</figure>

Let's take a look at the web server for now.

<figure id="f191" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2KXpB07Zlx62_mIS.png"
class="graf-image" data-image-id="0*2KXpB07Zlx62_mIS.png"
data-width="761" data-height="596" />
</figure>

On the homepage, we see an admin section. Clicking into it there's a
login form. Trying something like `admin:password`{.markup--code
.markup--p-code} calls an api which returns a
`401: Unauthorized`{.markup--code .markup--p-code} response. Moreover,
trying to register a new user throws an error saying signups are
disabled.

<figure id="47a8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OPEZZnRD7FXyf1Ub.png"
class="graf-image" data-image-id="0*OPEZZnRD7FXyf1Ub.png"
data-width="660" data-height="332" />
</figure>

Perhaps we can brute force the login?

### Brute Force Login {#b6f8 .graf .graf--h3 .graf-after--p name="b6f8"}

``` {#5059 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="wasm"}
hydra -l admin -P /usr/share/wordlists/rockyou.txt 'http-post://$TARGET_IP/api/login/:{"username"\:"^USER^","password"\:"^PASS^"}:H=Content-Type\:application/json:F=ERROR'
```

Getting a lot of 503 errors

### Directory Scanning {#199b .graf .graf--h3 .graf-after--p name="199b"}

<figure id="e83e" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*KjkIQ1a9kONnnmyw.png"
class="graf-image" data-image-id="0*KjkIQ1a9kONnnmyw.png"
data-width="494" data-height="101" />
</figure>

Hint is indicate the file name is "well known" create wordlist

``` {#6f2e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
wellknown
well-known
.well-known
.wellknown
WELLKNOWN
Wellknown
WEllknown
WeLlknwn
WELLknown
......
......
etc
```

### Gobuster {#5b19 .graf .graf--h3 .graf-after--pre name="5b19"}

<figure id="57f5" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*H0SJIttbbLHENmjH.png"
class="graf-image" data-image-id="0*H0SJIttbbLHENmjH.png"
data-width="875" data-height="400" />
</figure>

So this means that everything we try returns a `200`{.markup--code
.markup--p-code} status.

Armed with this information, we know that 200 response codes are bad,
but other response codes (such as a 302) maybe indicate a directory is
present. Let's rerun our Gobuster command, but we'll specify which
response codes we want returned.

Checking the help page, we can see that Gobuster accepts the following
response codes; **"200,204,301,302,307,401,403"**.

Remove status code 200

``` {#0037 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://10.10.211.97/ -w /usr/share/wordlists/dirb/common.txt -s "204,301,302,307,401,403"
```

<figure id="7776" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*i8y3cmr02gL7eeBd.png"
class="graf-image" data-image-id="0*i8y3cmr02gL7eeBd.png"
data-width="875" data-height="374" />
</figure>

Gobuster didn't work on
[http://10.10.207.227/.well-known](http://10.10.207.227/.well-known){.markup--anchor
.markup--p-anchor data-href="http://10.10.207.227/.well-known"
rel="noopener ugc nofollow noopener" target="_blank"}

so we try dirb

<figure id="bda8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PamL2LzZDX2xXNLk.png"
class="graf-image" data-image-id="0*PamL2LzZDX2xXNLk.png"
data-width="683" data-height="427" />
</figure>

So here we found security.txt file

<figure id="3496" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3kAv7n6s2rJJl8NZ.png"
class="graf-image" data-image-id="0*3kAv7n6s2rJJl8NZ.png"
data-width="581" data-height="239" />
</figure>

Using curl, we can get the first flag:

<figure id="4403" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2Po7lhh9VBZWa-_y.png"
class="graf-image" data-image-id="0*2Po7lhh9VBZWa-_y.png"
data-width="449" data-height="159" />
</figure>

Another common file on servers is the `robots.txt`{.markup--code
.markup--p-code} file. Our nmap scan showed us the presence of this file
with a few disallowed entries, let's take a closer look:

<figure id="7045" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RmPwjQrOsaIige-4.png"
class="graf-image" data-image-id="0*RmPwjQrOsaIige-4.png"
data-width="437" data-height="164" />
</figure>

We already know about the api route, but what's this
`exif-util`{.markup--code .markup--p-code} thing? Let's take a look:

<figure id="0907" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1YCQQrJk4o6jecED.png"
class="graf-image" data-image-id="0*1YCQQrJk4o6jecED.png"
data-width="726" data-height="338" />
</figure>

The upload functionality did not helped much.

### From URL Checking if the URL parameter is vulnerable to SSRF {#2170 .graf .graf--h3 .graf-after--p name="2170"}

Port 8080 was found by brute forcing common ports.

<figure id="66a3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ykp41xQb_08QC9cL.png"
class="graf-image" data-image-id="0*ykp41xQb_08QC9cL.png"
data-width="599" data-height="551" />
</figure>

The url called a new route

<figure id="3f04" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*M9s-Hl2MBmqXgWoO.png"
class="graf-image" data-image-id="0*M9s-Hl2MBmqXgWoO.png"
data-width="588" data-height="225" />
</figure>

``` {#fc48 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/api/exif?url=http:%2F%2F127.0.0.1:8080
```

This also did not lead me to any where so not the another entry in the
robots file can be used

/\*.bak.txt

I bruteforced the for the well known files and found

<figure id="6d75" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-kPFRLMevlldf8MP.png"
class="graf-image" data-image-id="0*-kPFRLMevlldf8MP.png"
data-width="875" data-height="325" />
</figure>

**exif-util.bak.txt**

<figure id="8ee8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NJ0G4yA31Sp8d4RB.png"
class="graf-image" data-image-id="0*NJ0G4yA31Sp8d4RB.png"
data-width="527" data-height="391" />
</figure>

<figure id="8501" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Y_0vpqU1J7B3mZgZ.png"
class="graf-image" data-image-id="0*Y_0vpqU1J7B3mZgZ.png"
data-width="639" data-height="111" />
</figure>

Now we found a new host api-dev-backup which should be a docker
container. Since this is a development backup I tried different
injection techniques. At last found a command injection

``` {#367d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://10.10.193.190/api/exif?url=http://api-dev-backup:8080/exif?url=/etc/passwd
```

<figure id="26af" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*cP3ioPs2uaruzgf6.png"
class="graf-image" data-image-id="0*cP3ioPs2uaruzgf6.png"
data-width="875" data-height="279" />
</figure>

Banned words which means there must be some filter going on

Let's try other commands

<figure id="b21e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KcFeIS-x32-a19W1.png"
class="graf-image" data-image-id="0*KcFeIS-x32-a19W1.png"
data-width="869" data-height="186" />
</figure>

Which means something is running. it read id command as file name . Lets
try other payloads

<figure id="24f5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DXNzWisxoEjchyw8.png"
class="graf-image" data-image-id="0*DXNzWisxoEjchyw8.png"
data-width="875" data-height="197" />
</figure>

And we successfully executed the command. We are root, but just on the
docker container.

I tried to get a reverse shell but was unsuccessful. It looks like the
all the outgoing traffic is blocked by the firewall. So, I manually
started going through the container.

<figure id="6fb7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*q9IXq33Em9fGTrAI.png"
class="graf-image" data-image-id="0*q9IXq33Em9fGTrAI.png"
data-width="623" data-height="434" />
</figure>

here we found git Let's enumerate this

<figure id="a982" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8xz3uv-5Tm0wexQb.png"
class="graf-image" data-image-id="0*8xz3uv-5Tm0wexQb.png"
data-width="643" data-height="598" />
</figure>

We can see that are three commits. So, lets check those out.

<figure id="0908" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wF6EtYYuTrMEaJTv.png"
class="graf-image" data-image-id="0*wF6EtYYuTrMEaJTv.png"
data-width="618" data-height="537" />
</figure>

We found **root Flag**

Just knock on port 42,1337,10420,6969,63000

<figure id="9f33" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hj2fW92r2fx8yJd6.png"
class="graf-image" data-image-id="0*hj2fW92r2fx8yJd6.png"
data-width="341" data-height="271" />
</figure>

the default docker port is **2375** Let's check if it is or not

<figure id="e65f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8KDR8ODs4AyLk5-R.png"
class="graf-image" data-image-id="0*8KDR8ODs4AyLk5-R.png"
data-width="754" data-height="423" />
</figure>

The next 2 steps I give might be unnecessary but I did it anyways where
I added the machine IP with the docker port to tell docker to trust this
instance and then restarted it

``` {#e204 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo vim /etc/docker/daemon.json
```

<figure id="50e3" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*qaousob4NbWB1bFW.png"
class="graf-image" data-image-id="0*qaousob4NbWB1bFW.png"
data-width="532" data-height="81" />
</figure>

I restarted my docker service by stopping it and then starting it again
after waiting for at least 30 seconds.

``` {#8095 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
sudo systemctl stop docker
<Wait 30 seconds>
sudo systemctl start docker
```

<figure id="3f0a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*JIYMWRZzuoS2gNtf.png"
class="graf-image" data-image-id="0*JIYMWRZzuoS2gNtf.png"
data-width="875" data-height="226" />
</figure>

We can successfully list the docker images using the API.

### Getting root shell {#f358 .graf .graf--h3 .graf-after--p name="f358"}

Here I have created a container from `frontend`{.markup--code
.markup--p-code} image on an interactive mode executing
`sh`{.markup--code .markup--p-code} binary. The root file system of the
host will be mounted on the `/mnt`{.markup--code .markup--p-code}
directory of the container and the root of the container is changed to
`/mnt`{.markup--code .markup--p-code}.

<figure id="b16d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Vd-ZRJ8Z2GbBon3e.png"
class="graf-image" data-image-id="0*Vd-ZRJ8Z2GbBon3e.png"
data-width="819" data-height="326" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#fdd3 .graf .graf--h3 .graf-after--figure name="fdd3"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#364d .graf .graf--h3 .graf-after--p name="364d"}

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
.h-card} on [August 24, 2024](https://medium.com/p/0dd289a1ae17).

[Canonical
link](https://medium.com/@bevijaygupta/the-great-escape-tryhackme-writeup-0dd289a1ae17){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
