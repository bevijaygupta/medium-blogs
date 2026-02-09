---
title: "Port Scanning for Bug Bounties 1b660ea41483"
platform: Medium
original_file: 2024-09-01_Port-Scanning-for-Bug-Bounties-1b660ea41483.md
---

# Port Scanning for Bug Bounties 1b660ea41483

::: {}
# Port Scanning for Bug Bounties {#port-scanning-for-bug-bounties .p-name}
:::

::: {.section .p-summary field="subtitle"}
1\. Introduction
:::

::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#5b3d .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Port Scanning for Bug Bounties {#3743 .graf .graf--h3 .graf--leading .graf--title name="3743"}

<figure id="b391" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*i5JT_qzlj9eTLBNn"
class="graf-image" data-image-id="0*i5JT_qzlj9eTLBNn" data-width="838"
data-height="363" data-is-featured="true" />
</figure>

### 1. Introduction {#d4f9 .graf .graf--h3 .graf-after--figure name="d4f9"}

Port scanning is one of the most fundamental techniques used in bug
bounty hunting and penetration testing. It involves probing a target
system to identify open ports, which can then be analyzed for
vulnerabilities. Understanding how to perform effective port scans is
crucial for any aspiring bug bounty hunter.

In this guide, we'll delve into the various methods of port scanning,
the tools you can use, and how to interpret the results to find
potential security weaknesses.
:::
::::
::::::

:::::: {#b292 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 2. Understanding Port Scanning {#3f63 .graf .graf--h3 .graf--leading name="3f63"}

**Port scanning** is the process of sending packets to specific ports on
a networked device to determine which ports are open, closed, or
filtered. Each port on a system corresponds to a particular service, and
identifying which ports are open can reveal valuable information about
the target's attack surface.

Ports are categorized as:

- [**Well-Known Ports** (0--1023): Common services like HTTP (80), HTTPS
  (443), FTP (21), etc.]{#d727}
- [**Registered Ports** (1024--49151): Services registered with IANA,
  like MySQL (3306), etc.]{#92db}
- [**Dynamic or Private Ports** (49152--65535): Typically used for
  client-side communication.]{#08d5}

**Why is port scanning important in bug bounties?**

- [**Identify potential entry points:** Open ports could be running
  vulnerable services.]{#8692}
- [**Understand the attack surface:** Helps in mapping out the system
  architecture.]{#40d9}
- [**Targeted exploitation:** Knowing the service behind a port allows
  for specific attack strategies.]{#1fe5}
:::
::::
::::::

:::::: {#24b1 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 3. Legal and Ethical Considerations {#565c .graf .graf--h3 .graf--leading name="565c"}

Before conducting any port scanning, it's essential to ensure that you
have **explicit permission** from the owner of the target system.
Unauthorized port scanning is illegal and can result in serious legal
consequences. For bug bounty hunters, always adhere to the rules set
forth by the platform or program under which you're operating.
:::
::::
::::::

:::::: {#54d1 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. Types of Port Scanning Techniques {#a184 .graf .graf--h3 .graf--leading name="a184"}

There are several techniques used in port scanning, each with its own
advantages and disadvantages. Understanding these methods is key to
performing effective scans.

#### TCP Connect Scan {#ef05 .graf .graf--h4 .graf-after--p name="ef05"}

**Command:**

``` {#87b2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sT <target>
```

- [**How it works:** This scan completes the TCP three-way handshake
  (SYN, SYN-ACK, ACK) with each port.]{#f5cc}
- [**Advantages:** Reliable; provides accurate results.]{#65ad}
- [**Disadvantages:** Easily detectable by intrusion detection systems
  (IDS) since it establishes a full connection.]{#174e}

#### SYN Scan (Half-Open Scan) {#1e0c .graf .graf--h4 .graf-after--li name="1e0c"}

**Command:**

``` {#080f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sS <target>
```

- [**How it works:** Sends a SYN packet and waits for a SYN-ACK
  response; it doesn't complete the handshake, hence
  "half-open."]{#cbaa}
- [**Advantages:** Faster and stealthier than TCP connect scans; less
  likely to be logged by the target system.]{#823c}
- [**Disadvantages:** Requires privileged access to raw sockets.]{#037c}

#### UDP Scan {#476f .graf .graf--h4 .graf-after--li name="476f"}

**Command:**

``` {#5cce .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sU <target>
```

- [**How it works:** Sends UDP packets to each port and listens for a
  response or an ICMP unreachable message.]{#be56}
- [**Advantages:** Identifies open UDP ports, which are often
  overlooked.]{#be3b}
- [**Disadvantages:** Slower and more difficult to perform than TCP
  scans; unreliable results due to UDP's connectionless nature.]{#dae8}

#### ACK Scan {#3692 .graf .graf--h4 .graf-after--li name="3692"}

**Command:**

``` {#da37 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sA <target>
```

- [**How it works:** Sends an ACK packet and analyzes the response to
  determine if ports are filtered by a firewall.]{#4e14}
- [**Advantages:** Useful for mapping out firewall rules.]{#c6d4}
- [**Disadvantages:** Doesn't identify open ports directly; only
  indicates filtered or unfiltered status.]{#6eff}

#### FIN Scan {#2bf8 .graf .graf--h4 .graf-after--li name="2bf8"}

**Command:**

``` {#618e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sF <target>
```

- [**How it works:** Sends a FIN packet, which is typically ignored by
  open ports but may generate a response from closed ports.]{#145d}
- [**Advantages:** Can bypass certain firewalls and packet
  filters.]{#8b93}
- [**Disadvantages:** Not effective on systems that follow RFC 793,
  which requires sending RST packets in response to a FIN.]{#2ef3}

#### Null Scan {#4a52 .graf .graf--h4 .graf-after--li name="4a52"}

**Command:**

``` {#dc13 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sN <target>
```

- [**How it works:** Sends a packet with no flags set. Similar to FIN
  scans, it relies on the behavior of closed ports sending RST
  responses.]{#840e}
- [**Advantages:** Stealthy and can bypass some IDS.]{#27a5}
- [**Disadvantages:** Ineffective against Windows systems, which respond
  with RST to all null packets.]{#88ff}

#### Xmas Scan {#c9b1 .graf .graf--h4 .graf-after--li name="c9b1"}

**Command:**

``` {#cdbc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sX <target>
```

- [**How it works:** Sends a packet with the FIN, PSH, and URG flags
  set, resembling a "lit up" Christmas tree.]{#7bd7}
- [**Advantages:** Effective against certain systems and can bypass some
  firewalls.]{#6af9}
- [**Disadvantages:** Similar limitations as the FIN and Null scans; not
  effective against Windows systems.]{#30df}
:::
::::
::::::

:::::: {#5142 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Popular Tools for Port Scanning {#25d8 .graf .graf--h3 .graf--leading name="25d8"}

Several tools are commonly used in port scanning, each with unique
features that cater to different scanning needs.

#### Nmap {#b6fd .graf .graf--h4 .graf-after--p name="b6fd"}

Nmap (Network Mapper) is the most widely used port scanning tool, known
for its versatility and power. It supports a wide range of scanning
techniques, including those mentioned above.

#### Masscan {#ec99 .graf .graf--h4 .graf-after--p name="ec99"}

Masscan is known for its speed and ability to scan large networks in a
short amount of time. It can scan the entire IPv4 address space in under
six minutes, making it ideal for large-scale scans.

#### Netcat {#90f7 .graf .graf--h4 .graf-after--p name="90f7"}

Netcat (often referred to as the "Swiss army knife" of networking) can
perform port scanning, banner grabbing, and more. It's a powerful tool
for manual testing.

#### Unicornscan {#150f .graf .graf--h4 .graf-after--p name="150f"}

Unicornscan is an advanced port scanner designed for fast and accurate
reconnaissance. It's less common but provides more granularity in scan
results.
:::
::::
::::::

:::::: {#45a7 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 6. How to Conduct a Port Scan Using Nmap {#6309 .graf .graf--h3 .graf--leading name="6309"}

Nmap is the go-to tool for most bug bounty hunters. Here's how to use it
effectively.

#### Installation {#3e81 .graf .graf--h4 .graf-after--p name="3e81"}

For most Linux distributions, Nmap can be installed using the package
manager:

``` {#8349 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
sudo apt-get install nmap
```

For Windows, download the installer from the official website.

#### Basic Scanning {#33c8 .graf .graf--h4 .graf-after--p name="33c8"}

A basic TCP connect scan can be initiated with:

``` {#8fe8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sT <target>
```

This command will scan the 1000 most common ports on the target.

#### Advanced Scanning Techniques {#1181 .graf .graf--h4 .graf-after--p name="1181"}

To scan all 65,535 ports:

``` {#571b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -p- <target>
```

To perform a SYN scan (stealth scan):

``` {#f782 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sS <target>
```

To scan a specific range of ports:

``` {#1391 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -p 80,443,8080 <target>
```

To perform a UDP scan:

``` {#3aca .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sU <target>
```

#### Output Formats {#1e6e .graf .graf--h4 .graf-after--pre name="1e6e"}

Nmap allows exporting scan results in various formats:

``` {#adff .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -oN normal_output.txt -oX xml_output.xml -oG grepable_output.txt <target>
```

This command will save the scan results in normal, XML, and grepable
formats.
:::
::::
::::::

:::::: {#52f4 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 7. Identifying Open Ports and Services {#02ad .graf .graf--h3 .graf--leading name="02ad"}

After performing a scan, interpreting the results is crucial.

#### Interpreting Nmap Results {#2b29 .graf .graf--h4 .graf-after--p name="2b29"}

Open ports will be listed with their respective state and service:

``` {#aeda .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https
```

- [**STATE:** Indicates whether the port is open, closed, or
  filtered.]{#49d8}
- [**SERVICE:** The service running on the port (e.g., HTTP,
  FTP).]{#5abd}

#### Service Version Detection {#f11a .graf .graf--h4 .graf-after--li name="f11a"}

To identify the version of the service running on an open port:

``` {#7c9e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -sV <target>
```

This command will provide additional information about the service, such
as the software version, which is crucial for identifying potential
vulnerabilities.

#### Operating System Detection {#1d40 .graf .graf--h4 .graf-after--p name="1d40"}

Nmap can also detect the operating system running on the target:

``` {#1bcd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -O <target>
```

This information can help tailor your attack strategy based on known
vulnerabilities associated with that OS.
:::
::::
::::::

:::::: {#8b52 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 8. Analyzing and Exploiting Open Ports {#4e12 .graf .graf--h3 .graf--leading name="4e12"}

Once you've identified open ports and the services running on them, the
next step is to analyze these services for vulnerabilities.

#### Common Vulnerabilities on Open Ports {#bef2 .graf .graf--h4 .graf-after--p name="bef2"}

- [**Port 21 (FTP):** Anonymous login, weak credentials, outdated
  software.]{#b7d8}
- [**Port 22 (SSH):** Weak passwords, outdated software, improper
  configuration.]{#b333}
- [**Port 80/443 (HTTP/HTTPS):** Cross-Site Scripting (XSS), SQL
  Injection, outdated software.]{#8113}
- [**Port 3306 (MySQL):** Weak passwords, SQL Injection.]{#991e}

#### Exploiting Vulnerabilities {#5d6c .graf .graf--h4 .graf-after--li name="5d6c"}

Tools like Metasploit can be used to exploit known vulnerabilities:

``` {#8c73 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST <target>
run
```

This example uses Metasploit to exploit a vulnerability in the vsftpd
FTP server.
:::
::::
::::::

:::::: {#bfee .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 9. Tips and Best Practices for Bug Bounty Hunters {#bcc9 .graf .graf--h3 .graf--leading name="bcc9"}

- [**Understand the target's architecture:** Spend time learning how the
  target system is set up before starting your scans.]{#9238}
- [**Use multiple scanning tools:** Don't rely solely on Nmap; use other
  tools like Masscan or Unicornscan to cross-verify results.]{#7fba}
- [**Be stealthy:** Use SYN scans or slow down your scan to avoid
  detection by IDS.]{#75a2}
- [**Document everything:** Keep detailed notes on your scanning
  process, results, and any vulnerabilities you discover.]{#bada}
- [**Stay ethical:** Only scan systems you have permission to scan, and
  report any vulnerabilities responsibly.]{#89e7}
:::
::::
::::::

:::::: {#6168 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 10. Conclusion {#cb2d .graf .graf--h3 .graf--leading name="cb2d"}

Port scanning is a critical skill for any bug bounty hunter or
penetration tester. By understanding the different scanning techniques,
tools, and how to interpret the results, you can uncover valuable
information about a target's security posture. Remember to always
operate within the bounds of legality and ethics, and use your skills to
contribute positively to the security community.

Happy hunting!

### Promote and Collaborate on Cybersecurity Insights {#a270 .graf .graf--h3 .graf-after--p name="a270"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#263a .graf .graf--h3 .graf-after--p name="263a"}

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
:::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 1, 2024](https://medium.com/p/1b660ea41483).

[Canonical
link](https://medium.com/@bevijaygupta/port-scanning-for-bug-bounties-1b660ea41483){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
