---
title: "THREAT INTELLIGENCE Tryhackme Writeup b2f196d1e3f8"
platform: Medium
original_file: 2024-08-19_THREAT-INTELLIGENCE-Tryhackme-Writeup-b2f196d1e3f8.md
---

# THREAT INTELLIGENCE Tryhackme Writeup b2f196d1e3f8

::: {}
# THREAT INTELLIGENCE Tryhackme Writeup {#threat-intelligence-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "THREAT INTELLIGENCE"
:::

::::::: {.section .e-content field="body"}
:::::: {#7e3f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### THREAT INTELLIGENCE Tryhackme Writeup {#35ba .graf .graf--h3 .graf--leading .graf--title name="35ba"}

**This is a Writeup of Tryhackme room "THREAT INTELLIGENCE"**

<figure id="76b1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AqTL0_z1_pi40mol.png"
class="graf-image" data-image-id="0*AqTL0_z1_pi40mol.png"
data-width="446" data-height="244" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/threatintelligence](https://tryhackme.com/room/threatintelligence){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/threatintelligence"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Task 1: Understanding a Threat Intelligence blog post on a recent attack {#fe50 .graf .graf--h3 .graf-after--p name="fe50"}

**THREAT INTELLIGENCE: SUNBURST**

This lab will try to walk an SOC Analyst through the steps that they
would take to assist in breach mitigations and identifying important
data from a Threat Intelligence report.

Lets try to define some of the words that we will encounter:

**Red Team Tools:** Red team tools are a set of programs that offensive
security teams will use in pentesting engagements to assist a company in
determining flaws in their procedures, policies, frameworks, tools,
configurations, and workflows. A Red Team may try to crack user
passwords, takeover company infrastructure like apis, routers,
firewalls, IPS/IDS, Printer servers, Mail Servers, Active Directory
Servers, basically ANYTHING they can get their digital hands on. Some
common frameworks and OS used to study for Sec+/Sans/OSCP/CEH include
Kali, Parrot, and metasploit

**APT:** Advanced Persistant Threat is a nation-state funded hacker
organization which participates in international espionage and crime.
Humanity is far into the fourth industrial revolution whether we know it
or not. Robotics, AI, and Cyberwar are now considered a norm and there
are many things you can do as an individual to protect yourself and your
data (Pi-Hole, OpenDNS, GPG).

**IoT (Internet of Things):** This is now any electronic device which
you may consider a PLC (Programmable Logic Controller). Any PC,
Computer, Smart device (Refridgerator, doorbell, camera) which has an
IPv4 or IPv6 is likely accessible from the public net. In many
challenges you may use Shodan to search for interesting devices. The IoT
(Internet of Things) has us all connected in ways which we never
imagined possible and the changing technological landscape is evolving
faster than policies and privacies can keep up with.

**Zero-Day Exploit:** A vulnerability discovered in a system or
carefully crafted exploit which does not have a released software patch
and there has not been a specific use of this particular exploit.
(Stuxnet)

**Blue Team:** Blue team will work with their organizations Developers,
Operations team, IT Operations, DevOps, and Networking to communicate
important information from security disclosures, threat intelligence,
blog posts, and other resources to update procedures, processes, and
protocols. A lot of Blue Teams worm within an SIEM which can utilize
Open Source tools (ELK) or purchase powerful enterprise solutions
(SPLUNK).

You can find additional learning materials in the free ATT&CK MITRE
room:
[https://tryhackme.com/room/mitre](https://tryhackme.com/room/mitre){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/mitre"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 2: Review the FireEye Threat Intel on the SUNBURST Malware {#f888 .graf .graf--h3 .graf-after--p name="f888"}

Given a threat report from FireEye attack either a sample of the
malware, wireshark pcap, or SIEM identify the important data from an
Incident Response point of view.

[https://www.fireeye.com/blog/threat-research/2020/12/unauthorized-access-of-fireeye-red-team-tools.html](https://www.fireeye.com/blog/threat-research/2020/12/unauthorized-access-of-fireeye-red-team-tools.html){.markup--anchor
.markup--p-anchor
data-href="https://www.fireeye.com/blog/threat-research/2020/12/unauthorized-access-of-fireeye-red-team-tools.html"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://www.fireeye.com/blog/threat-research/2020/12/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor.html](https://www.fireeye.com/blog/threat-research/2020/12/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor.html){.markup--anchor
.markup--p-anchor
data-href="https://www.fireeye.com/blog/threat-research/2020/12/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor.html"
rel="noopener ugc nofollow noopener" target="_blank"}

Read the FireEye Blog and search around the internet for additional
resources. After you familiarize yourself with the attack continue.

### Task 3: Analyze Threat Intelligence {#6f07 .graf .graf--h3 .graf-after--p name="6f07"}

**Q.1: After reading the report what did FireEye name the APT?**

> ***Answer:*** *Executive Summary section tell us the APT
> name :****UNC2452***

**Q.2: FireEye released some information to help security orgranizations
Blue Team to detect the tools which have been leaked. What 'multiple
languages' can you find the rules? \[Ans Format:
\*\*\*\*\*\|\*\*\*\*\|\*\*\*\|\*\*\*\*\*\* \]**

> ***Answer:*** *From this*
> [*GitHub*](https://github.com/fireeye/sunburst_countermeasures){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://github.com/fireeye/sunburst_countermeasures"
> rel="noopener ugc nofollow noopener" target="_blank"} *page:*
> ***Snort\|Yara\|IOC\|ClamAV***

**Q.3: Which dll file was used to create the backdoor?**

> ***Answer:*** *From Summary-\>SUNBURST Backdoor Section*
> ***SolarWinds.Orion.Core.BusinessLayer.dll***

**Q.4: What is the MD5 sum of this file?**

> ***Answer:*** *From In-Depth Malware Analysis Section:*
> ***b91ce2fa41029f6955bff20079468448***

**Q.5: Authorized system administrators commonly perform tasks which
ultimately led to how was the malware was delivered and installed into
the network. What is the file extension of the software which contains
the delivery of the dll file mentioned earlier?**

> ***Answer:*** *From Delivery and Installation section :* ***msp***

**Q.6: A C2 Framework will Beacon out to the botmaster after some amount
of time. This particular malware sample was purposely crafted to evade
common sandboxing techniques by using a longer than normal time with a
large jitter interval as well. How long does the malware stay hidden on
infected machines before beginning the beacon? Min Time \| Max Time \|
Unit of Measure for time \[Flag Format: \*\*\|\*\*\|\*\*\*\* \]**

> ***Answer:*** *From Delivery and Installation
> section :****12\|14\|days***

**Q.7: Can you find the IoCs for host-based and network-based detection
of the C2? The flag is the name of the classification which the first 3
network IP address blocks belong to?**

**Answer:** *This was a tricky one.*

*From Network Command and Control (C2) section the first 3 network IP
address blocks were:*

- [*10.0.0.0/8*]{#69b6}
- [*172.16.0.0/12*]{#aefb}
- [*192.168.0.0/16*]{#4f16}

*These are all private address ranges and the name of the classification
as given as a hint was bit confusion but after wrapping your head around
it the answer was "*[***RFC
1918***](https://tools.ietf.org/html/rfc1918){.markup--anchor
.markup--p-anchor data-href="https://tools.ietf.org/html/rfc1918"
rel="noopener ugc nofollow noopener" target="_blank"}*"*

**Q.8: In the snort rules you can find a number of messages reffering to
Backdoor.SUNBURST and Backdoor.BEACON. Only one of these domains
resolves to a fake organization posing as an online college. What is the
quoted domain name in the content field for this organization?**

> ***Answer:*** *From this*
> [*GitHub*](https://github.com/fireeye/sunburst_countermeasures/blob/main/all-snort.rules){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://github.com/fireeye/sunburst_countermeasures/blob/main/all-snort.rules"
> rel="noopener ugc nofollow noopener" target="_blank"} *link about
> sunburst snort rules:* ***digitalcollege.org***

**Q.9: Stenography was used to obfuscate the commands and data over the
network connection to the C2. If I wanted to change registry values on a
remote machine which number command would the attacker use?**

> ***Answer:*** *From Steganography-\>Supported Commands
> section-\>SetRegistryValue to write:* ***14***

**Q.10: How was that payload encoded?**

> ***Answer:*** *From Network Command and Control (C2) section:*
> ***base64***

**Q.11: What is the name of the program which dispatches the jobs?**

> ***Answer:*** *From Steganography Section:* ***JobExecutionEngine***

**Q.12: How many Mitre Attack techniques were used?**

> ***Answer:*** *Count from MITRE ATT&CK Techniques Observed section:*
> ***17***

**Q.13: According to Solarwinds response only a certain number of
machines fall vulnerable to this attack. What is the number of
potentially affected machines?**

> ***Answer:*** *From this* [*Wikipedia
> link*](https://en.wikipedia.org/wiki/Supply_chain_attack){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://en.wikipedia.org/wiki/Supply_chain_attack"
> rel="noopener ugc nofollow noopener" target="_blank"}*-\>SolarWinds
> section:* ***18,000***

**Q.14: FireEye recommends a number of items to do immediately if you
are an administrator of an affected machine. What is the name of the new
recommended patch release?**

> ***Answer:*** *From Immediate Mitigation Recommendations section:*
> ***2020.2.1 HF 1***

### Task 4: Additional Resources {#a2e7 .graf .graf--h3 .graf-after--blockquote name="a2e7"}

After ingesting the threat intelligence the SOC team will work to update
the vulnerabilities using tools like Yara, Suricata, Snort, and ELK for
example.

You can learn more at this TryHackMe Room:
[https://tryhackme.com/room/yara](https://tryhackme.com/room/yara){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/yara"
rel="noopener ugc nofollow noopener" target="_blank"}

Additional Resources:

FireEyeBlog Accessed Red Team Tools:
[https://www.fireeye.com/blog/threat-research/2020/12/unauthorized-access-of-fireeye-red-team-tools.html](https://www.fireeye.com/blog/threat-research/2020/12/unauthorized-access-of-fireeye-red-team-tools.html){.markup--anchor
.markup--p-anchor
data-href="https://www.fireeye.com/blog/threat-research/2020/12/unauthorized-access-of-fireeye-red-team-tools.html"
rel="noopener ugc nofollow noopener" target="_blank"}

FireEyeBlog Solarwinds malware analysis:
[https://www.fireeye.com/blog/threat-research/2020/12/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor.html](https://www.fireeye.com/blog/threat-research/2020/12/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor.html){.markup--anchor
.markup--p-anchor
data-href="https://www.fireeye.com/blog/threat-research/2020/12/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor.html"
rel="noopener ugc nofollow noopener" target="_blank"}

SolarWinds Advisory:
[https://www.solarwinds.com/securityadvisory](https://www.solarwinds.com/securityadvisory){.markup--anchor
.markup--p-anchor
data-href="https://www.solarwinds.com/securityadvisory"
rel="noopener ugc nofollow noopener" target="_blank"}

Sans:
[https://www.sans.org/webcasts/emergency-webcast-about-solarwinds-supply-chain-attack-118015](https://www.sans.org/webcasts/emergency-webcast-about-solarwinds-supply-chain-attack-118015){.markup--anchor
.markup--p-anchor
data-href="https://www.sans.org/webcasts/emergency-webcast-about-solarwinds-supply-chain-attack-118015"
rel="noopener ugc nofollow noopener" target="_blank"}

SOC Rule Updates for IOC:
[https://github.com/fireeye/red_team_tool_countermeasures](https://github.com/fireeye/red_team_tool_countermeasures){.markup--anchor
.markup--p-anchor
data-href="https://github.com/fireeye/red_team_tool_countermeasures"
rel="noopener ugc nofollow noopener" target="_blank"}

SOC Rule Updates for IOC:
[https://github.com/fireeye/sunburst_countermeasures](https://github.com/fireeye/sunburst_countermeasures){.markup--anchor
.markup--p-anchor
data-href="https://github.com/fireeye/sunburst_countermeasures"
rel="noopener ugc nofollow noopener" target="_blank"}

SOC Rule Updates for IOC:
[https://github.com/fireeye/sunburst_countermeasures/blob/64266c2c2c5bbbe4cc8452bde245ed2c6bd94792/all-snort.rules](https://github.com/fireeye/sunburst_countermeasures/blob/64266c2c2c5bbbe4cc8452bde245ed2c6bd94792/all-snort.rules){.markup--anchor
.markup--p-anchor
data-href="https://github.com/fireeye/sunburst_countermeasures/blob/64266c2c2c5bbbe4cc8452bde245ed2c6bd94792/all-snort.rules"
rel="noopener ugc nofollow noopener" target="_blank"}

Gov Security Disclosure:
[https://www.sec.gov/ix?doc=/Archives/edgar/data/1739942/000162828020017451/swi-20201214.htm](https://www.sec.gov/ix?doc=%2FArchives%2Fedgar%2Fdata%2F1739942%2F000162828020017451%2Fswi-20201214.htm){.markup--anchor
.markup--p-anchor
data-href="https://www.sec.gov/ix?doc=%2FArchives%2Fedgar%2Fdata%2F1739942%2F000162828020017451%2Fswi-20201214.htm"
rel="noopener ugc nofollow noopener" target="_blank"}

Microsoft Blog:
[https://msrc-blog.microsoft.com/2020/12/13/customer-guidance-on-recent-nation-state-cyber-attacks/](https://msrc-blog.microsoft.com/2020/12/13/customer-guidance-on-recent-nation-state-cyber-attacks/){.markup--anchor
.markup--p-anchor
data-href="https://msrc-blog.microsoft.com/2020/12/13/customer-guidance-on-recent-nation-state-cyber-attacks/"
rel="noopener ugc nofollow noopener" target="_blank"}

Wired:
[https://www.wired.com/story/russia-solarwinds-supply-chain-hack-commerce-treasury/](https://www.wired.com/story/russia-solarwinds-supply-chain-hack-commerce-treasury/){.markup--anchor
.markup--p-anchor
data-href="https://www.wired.com/story/russia-solarwinds-supply-chain-hack-commerce-treasury/"
rel="noopener ugc nofollow noopener" target="_blank"}

TrustedSec:
[https://www.trustedsec.com/blog/solarwinds-orion-and-unc2452-summary-and-recommendations/](https://www.trustedsec.com/blog/solarwinds-orion-and-unc2452-summary-and-recommendations/?utm_content=149091396&utm_medium=social&utm_source=twitter&hss_channel=tw-403811306){.markup--anchor
.markup--p-anchor
data-href="https://www.trustedsec.com/blog/solarwinds-orion-and-unc2452-summary-and-recommendations/?utm_content=149091396&utm_medium=social&utm_source=twitter&hss_channel=tw-403811306"
rel="noopener ugc nofollow noopener" target="_blank"}

Splunk SIEM:
[https://www.splunk.com/en_us/blog/security/sunburst-backdoor-detections-in-splunk.html](https://www.splunk.com/en_us/blog/security/sunburst-backdoor-detections-in-splunk.html){.markup--anchor
.markup--p-anchor
data-href="https://www.splunk.com/en_us/blog/security/sunburst-backdoor-detections-in-splunk.html"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://www.fedscoop.com/solarwinds-federal-footprint-nightmare/](https://www.fedscoop.com/solarwinds-federal-footprint-nightmare/){.markup--anchor
.markup--p-anchor
data-href="https://www.fedscoop.com/solarwinds-federal-footprint-nightmare/"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://docs.netgate.com/pfsense/en/latest/network/addresses.html](https://docs.netgate.com/pfsense/en/latest/network/addresses.html){.markup--anchor
.markup--p-anchor
data-href="https://docs.netgate.com/pfsense/en/latest/network/addresses.html"
rel="noopener ugc nofollow noopener" target="_blank"}

[BHIS Weekly Security
Talk](https://www.youtube.com/watch?v=QZOW0itnyLU&t=1710s){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com/watch?v=QZOW0itnyLU&t=1710s"
rel="noopener ugc nofollow noopener" target="_blank"}

### Promote and Collaborate on Cybersecurity Insights {#64f8 .graf .graf--h3 .graf-after--p name="64f8"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#6053 .graf .graf--h3 .graf-after--p name="6053"}

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
.h-card} on [August 19, 2024](https://medium.com/p/b2f196d1e3f8).

[Canonical
link](https://medium.com/@bevijaygupta/threat-intelligence-tryhackme-writeup-b2f196d1e3f8){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
