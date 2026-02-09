::: {}
# Understanding Nmap Scan with Wireshark {#understanding-nmap-scan-with-wireshark .p-name}
:::

::: {.section .p-summary field="subtitle"}
In this article, you will learn how to capture network packet using
Wireshark when an attacker is scanning target using NMAP port
scanning...
:::

::::::: {.section .e-content field="body"}
:::::: {#849a .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Understanding Nmap Scan with Wireshark {#14c9 .graf .graf--h3 .graf--leading .graf--title name="14c9"}

In this article, you will learn how to capture network packet using
Wireshark when an attacker is scanning target using NMAP port scanning
method. Here you will notice that how Wireshark captured different
network traffic packet for open and close ports.

<figure id="7ce9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EOuWYn-oNlYsJyJN.png"
class="graf-image" data-image-id="0*EOuWYn-oNlYsJyJN.png"
data-width="875" data-height="494" data-is-featured="true" />
</figure>

> ***Note: The Below Practical is performed with the IP address***

> ***192.168.43.251 = Metasploitable 2 Machine (Target)***

> ***192.168.43.72 = Attacker (Kali)***

[**Download Metasploitable 2
Machine**](https://download.vulnhub.com/metasploitable/metasploitable-linux-2.0.0.zip){.markup--anchor
.markup--p-anchor
data-href="https://download.vulnhub.com/metasploitable/metasploitable-linux-2.0.0.zip"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://download.vulnhub.com/metasploitable/metasploitable-linux-2.0.0.zip](https://download.vulnhub.com/metasploitable/metasploitable-linux-2.0.0.zip){.markup--anchor
.markup--p-anchor
data-href="https://download.vulnhub.com/metasploitable/metasploitable-linux-2.0.0.zip"
rel="noopener ugc nofollow noopener" target="_blank"}

### TCP Scan {#6fc4 .graf .graf--h3 .graf-after--p name="6fc4"}

Tcp scan will scan for TCP port like port 22, 21, 23, 445 etc and ensure
for listening port (open) through 3-way handshake connection between the
source and destination port. If the port is open then source made
request with **SYN** packet, a response destination sent **SYN, ACK**
packet and then source sent **ACK** packets, at last source again sent
**RST, ACK** packets.

<figure id="de59" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KI-SgiKzgVOMAQ-T.png"
class="graf-image" data-image-id="0*KI-SgiKzgVOMAQ-T.png"
data-width="409" data-height="204" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#ba9e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sT -p 445 192.168.43.251
```

From the given image you can observe the result that port **445** is
**open**.

<figure id="d881" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*agLoci7OmWqypIsB.png"
class="graf-image" data-image-id="0*agLoci7OmWqypIsB.png"
data-width="665" data-height="251" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark.

You will notice that it has captured the same sequence of the flag as
described above:

- [Source sent SYN packet to the destination]{#3873}
- [Destination sent SYN, ACK to source]{#f119}
- [Source sent ACK packet to the destination]{#efa3}
- [Source again sent RST, ACK to destination]{#b929}

<figure id="72bc" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*NZOhjwyRocU3YgiY.png"
class="graf-image" data-image-id="0*NZOhjwyRocU3YgiY.png"
data-width="875" data-height="164" />
</figure>

Let's figure out network traffic for the close port. According to a
given image, it is showing if scanning port is closed then 3-way
handshake connection would be not possible between source and
destination.

Source sent SYN pack and if the port is close the receiver will be sent
a response through RST, ACK.

<figure id="9391" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cJcH34NwhsvVe-yX.png"
class="graf-image" data-image-id="0*cJcH34NwhsvVe-yX.png"
data-width="408" data-height="204" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#8255 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sT -p 3389 192.168.43.251
```

From the given image you can observe the result that port **3389** is
**closed**.

<figure id="fb90" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fTARIDMj8qyvjGm6.png"
class="graf-image" data-image-id="0*fTARIDMj8qyvjGm6.png"
data-width="658" data-height="244" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark.

You will notice that it has captured the same sequence of the flag as
described above:

- [Source sent SYN packet to the destination]{#0af5}
- [Destination sent RST, ACK packet to the source]{#710d}

<figure id="1514" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*y8ncURKkvyB9Wj6U.png"
class="graf-image" data-image-id="0*y8ncURKkvyB9Wj6U.png"
data-width="696" data-height="110" />
</figure>

### Stealth Scan {#a9f1 .graf .graf--h3 .graf-after--figure name="a9f1"}

SYN scan is the default and most popular scan option for good reasons.
It can be performed quickly, scanning thousands of ports per second on a
fast network not hampered by restrictive firewalls. It is also
relatively typical and stealthy since it never completes TCP
connections.

The port is also considered open if an SYN packet (without the ACK flag)
is received in response.

This technique is often referred to as half-open scanning because you
don't open a full TCP connection. You send an SYN packet as if you are
going to open a real connection and then wait for a response. An SYN,
ACK indicates the port is listening (open)

<figure id="7d31" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FC2L8nPGpuSuzUJK.png"
class="graf-image" data-image-id="0*FC2L8nPGpuSuzUJK.png"
data-width="412" data-height="206" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#f780 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sS -p 22 192.168.43.251
```

From the given image you can observe the result that port **22** is
**open.**

<figure id="0761" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5grw320Aic87phF6.png"
class="graf-image" data-image-id="0*5grw320Aic87phF6.png"
data-width="661" data-height="243" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent SYN packets to the destination]{#6963}
- [Destination sent SYN, ACK packets to the source]{#6883}
- [Source sent RST packets to the destination]{#84ef}

<figure id="c653" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*6hQUH15ki_r6Z7i9.png"
class="graf-image" data-image-id="0*6hQUH15ki_r6Z7i9.png"
data-width="875" data-height="115" />
</figure>

Now figure out traffic for close port using stealth scan. When source
sent SYN packet on the specific port then if the port is closed then the
destination will reply by sending RST packet.

<figure id="a6ee" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UwndUcAwIQojPMUE.png"
class="graf-image" data-image-id="0*UwndUcAwIQojPMUE.png"
data-width="417" data-height="201" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#4581 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sS -p 3389 192.168.43.251
```

From the given image you can observe the result that port **3389** is
**closed.**

<figure id="ef11" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PCd3Gl803opHCK1H.png"
class="graf-image" data-image-id="0*PCd3Gl803opHCK1H.png"
data-width="660" data-height="246" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent SYN packets to the destination]{#8d44}
- [Destination sent RST, ACK packets to the destination]{#d54d}

<figure id="4bc1" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*LTrsaWEBCdjGOipM.png"
class="graf-image" data-image-id="0*LTrsaWEBCdjGOipM.png"
data-width="875" data-height="99" />
</figure>

### Fin Scan {#47cf .graf .graf--h3 .graf-after--figure name="47cf"}

A FIN packet is used to terminate the TCP connection between the source
and destination port typically after the data transfer is complete. In
the place of an SYN packet, Nmap starts a FIN scan by using a FIN
packet. If the port is open then no response will come from destination
port when FIN packet is sent through source port.

**Fin-Scan are only workable in Linux machines and does not work on the
latest version of windows**

<figure id="36e8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qWVzP7XL9urRxfMm.png"
class="graf-image" data-image-id="0*qWVzP7XL9urRxfMm.png"
data-width="407" data-height="206" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#3a7d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sF -p 22 192.168.43.251
```

From the given image you can observe the result that port **22** is
**open.**

<figure id="d29f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*75vVDRFq1AUvZwPb.png"
class="graf-image" data-image-id="0*75vVDRFq1AUvZwPb.png"
data-width="666" data-height="249" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent FIN packets to the destination]{#9578}
- [Destination sent no reply to the source]{#6f2f}

<figure id="a9e7" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*zQYzGhEGvNw7a1fp.png"
class="graf-image" data-image-id="0*zQYzGhEGvNw7a1fp.png"
data-width="875" data-height="105" />
</figure>

Similarly, if Fin scan is performed against any close then source port
will be sent FIN packet to specific port and destination will reply by
sending RST, ACK packets.

<figure id="ab17" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zWgrFt039XMyrZuQ.png"
class="graf-image" data-image-id="0*zWgrFt039XMyrZuQ.png"
data-width="407" data-height="199" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#3901 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sF -p 3389 192.168.43.251
```

From the given image you can observe the result that port **3389** is
**closed.**

<figure id="8211" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1D75V7CJucPAwpL1.png"
class="graf-image" data-image-id="0*1D75V7CJucPAwpL1.png"
data-width="663" data-height="243" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent SYN packets to the destination]{#2df0}
- [Destination sent RST packets to the destination]{#4381}

<figure id="fb5e" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*UXLqGe7xP1-yk8lY.png"
class="graf-image" data-image-id="0*UXLqGe7xP1-yk8lY.png"
data-width="875" data-height="111" />
</figure>

### Null Scan {#5b87 .graf .graf--h3 .graf-after--figure name="5b87"}

A Null Scan is a series of TCP packets which hold a sequence number of
"zeros" (0000000) and since there are none flags set, the destination
will not know how to reply the request. It will discard the packet and
no reply will be sent, which indicate that the port is open.

**Null Scan is only workable in Linux machines and does not work on
latest version of windows**

<figure id="e33f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GQ2WrKK2anpapRmb.png"
class="graf-image" data-image-id="0*GQ2WrKK2anpapRmb.png"
data-width="404" data-height="201" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#c3f5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sN -p 22 192.168.43.251
```

From the given image you can observe the result that port **22** is
**open.**

<figure id="de19" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*khlxpgZTonhxcrP0.png"
class="graf-image" data-image-id="0*khlxpgZTonhxcrP0.png"
data-width="661" data-height="252" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent Null packets to the destination]{#6f24}
- [Destination sent no reply to the source]{#f9e4}

<figure id="08b6" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*GbNoAcxMQawLr4jM.png"
class="graf-image" data-image-id="0*GbNoAcxMQawLr4jM.png"
data-width="823" data-height="97" />
</figure>

If the port is closed, the Destination will send an RST, ACK packet in
response when source send null packets on a specific port

<figure id="cad4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2IAQ1UHgggriS4ax.png"
class="graf-image" data-image-id="0*2IAQ1UHgggriS4ax.png"
data-width="415" data-height="204" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#ecda .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sN -p 3389 192.168.43.251
```

From the given image you can observe the result that port **3389** is
**closed.**

<figure id="07cc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6qrZTuZ6PS6wAvfa.png"
class="graf-image" data-image-id="0*6qrZTuZ6PS6wAvfa.png"
data-width="656" data-height="251" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent Null (none) packets to the destination]{#7681}
- [Destination sent RST, ACK to source]{#9157}

<figure id="6c4b" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*8lxxbcjcvQG60Rov.png"
class="graf-image" data-image-id="0*8lxxbcjcvQG60Rov.png"
data-width="875" data-height="98" />
</figure>

### UDP Scan {#0111 .graf .graf--h3 .graf-after--figure name="0111"}

UDP scan works by sending a UDP packet to every destination port; it is
a connectionless protocol. For some common ports such as 53 and 161, a
protocol-specific payload is sent to increase the response rate, a
service will respond with a UDP packet, proving that it is open. If no
response is received after retransmissions, the port is classified as
open\|filtered. This means that the port could be open, or perhaps
packet filters are blocking the communication.

<figure id="40b6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sqZUmk3Zm5xD4t6P.png"
class="graf-image" data-image-id="0*sqZUmk3Zm5xD4t6P.png"
data-width="413" data-height="210" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#7009 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sU -p 53 192.168.43.251
```

From the given image you can observe the result that port **161** is
**open.**

<figure id="8de4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7yzXQQafPV16AV9i.png"
class="graf-image" data-image-id="0*7yzXQQafPV16AV9i.png"
data-width="649" data-height="249" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent UDP packets to the destination]{#ba29}
- [Destination sent UDP packet with some data to the source]{#49fc}

<figure id="3ada" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*7esLq7HXjg5Mc_f1.png"
class="graf-image" data-image-id="0*7esLq7HXjg5Mc_f1.png"
data-width="875" data-height="113" />
</figure>

Similarly, if source sent UDP packet on a close port to the destination
then destination sent a reply with ICMP packet port unreachable with an
appropriate error.

<figure id="7943" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vR23xm4R_oqL_eUE.png"
class="graf-image" data-image-id="0*vR23xm4R_oqL_eUE.png"
data-width="415" data-height="204" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#7387 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sU -p 161 192.168.43.251
```

From the given image you can observe the result that port **53** is
**closed.**

<figure id="a9a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*l0uvkxt8fb4wZKWm.png"
class="graf-image" data-image-id="0*l0uvkxt8fb4wZKWm.png"
data-width="652" data-height="249" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent UDP packets to the destination]{#43c2}
- [Destination sent ICMP packet port unreachable to the source]{#9139}

<figure id="6161" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*Vkfu7LiPaGqigu6Z.png"
class="graf-image" data-image-id="0*Vkfu7LiPaGqigu6Z.png"
data-width="875" data-height="97" />
</figure>

### Xmas Scan {#4089 .graf .graf--h3 .graf-after--figure name="4089"}

These scans are designed to manipulate the PSH, URG and FIN flags of the
TCP header, Sets the FIN, PSH, and URG flags, lighting the packet up
like a Christmas tree. When source sent FIN, PUSH, and URG packet to a
specific port and if the port is open then destination will discard the
packets and will not send any reply to the source.

**Xmas Scan is only workable in Linux machines and does not work on the
latest version of windows**

<figure id="8862" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JA0RKatZ9-8z6pIu.png"
class="graf-image" data-image-id="0*JA0RKatZ9-8z6pIu.png"
data-width="413" data-height="203" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#5179 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sX -p 22 192.168.43.251
```

From the given image you can observe the result that port **22** is
**open.**

<figure id="5daa" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2wcWP3HCvnfZWN5r.png"
class="graf-image" data-image-id="0*2wcWP3HCvnfZWN5r.png"
data-width="669" data-height="257" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent FIN, PUSH and URG packets to the destination]{#ee78}
- [Destination sent no reply to the source]{#eca8}

<figure id="165b" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*SwTEq3e3CzgzexUk.png"
class="graf-image" data-image-id="0*SwTEq3e3CzgzexUk.png"
data-width="875" data-height="110" />
</figure>

Similarly, if source sent FIN, PUSH and URG packets to a specific port
and if the port is closed then destination will be sent RST, ACK packets
to the source.

<figure id="e04d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DsJB-QqCtBLwU1px.png"
class="graf-image" data-image-id="0*DsJB-QqCtBLwU1px.png"
data-width="411" data-height="196" />
</figure>

Type following NMAP command for TCP scan as well as start Wireshark on
another hand to capture the sent Packet.

``` {#73c5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -sX -p 3389 192.168.43.251
```

From the given image you can observe the result that port **3389** is
**closed.**

<figure id="6d42" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*myzxD9xJ9lpixfYp.png"
class="graf-image" data-image-id="0*myzxD9xJ9lpixfYp.png"
data-width="667" data-height="257" />
</figure>

Look over the sequence of packet transfer between source and destination
captured through Wireshark

- [Source sent FIN, PUSH and URG packets to the destination]{#2761}
- [Destination RST, ACK packet to the source]{#5308}

<figure id="8b83" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*Xcmup_JGEhMTnOAH.png"
class="graf-image" data-image-id="0*Xcmup_JGEhMTnOAH.png"
data-width="875" data-height="117" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#3d07 .graf .graf--h3 .graf-after--figure name="3d07"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#8fe5 .graf .graf--h3 .graf-after--p name="8fe5"}

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
.h-card} on [August 29, 2024](https://medium.com/p/f649645dc5b1).

[Canonical
link](https://medium.com/@bevijaygupta/understanding-nmap-scan-with-wireshark-f649645dc5b1){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
