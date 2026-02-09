::: {}
# OSCP Enumeration Cheat Sheet {#oscp-enumeration-cheat-sheet .p-name}
:::

::: {.section .p-summary field="subtitle"}
Enumeration is one of the most critical phases in any penetration
testing or ethical hacking exercise. It involves gathering as much...
:::

::::::: {.section .e-content field="body"}
:::::: {#c972 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### OSCP Enumeration Cheat Sheet {#2651 .graf .graf--h3 .graf--leading .graf--title name="2651"}

<figure id="d4cd" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*NAiuLX47E8yOBRlj"
class="graf-image" data-image-id="0*NAiuLX47E8yOBRlj" data-width="939"
data-height="375" data-is-featured="true" />
</figure>

Enumeration is one of the most critical phases in any penetration
testing or ethical hacking exercise. It involves gathering as much
information as possible about the target system, laying the groundwork
for further exploitation. For those preparing for the Offensive Security
Certified Professional (OSCP) certification, mastering enumeration
techniques is essential to identify vulnerabilities and potential attack
vectors. This cheat sheet is designed to be your go-to resource for
enumeration, organized to help you succeed in the OSCP exam and
real-world engagements.

### What Is Enumeration? {#cae5 .graf .graf--h3 .graf-after--p name="cae5"}

Enumeration is the process of actively gathering detailed information
about a target system. It goes beyond passive reconnaissance by
interacting directly with the target. The goal is to uncover usernames,
hostnames, shares, services, operating systems, and other details that
could lead to a successful compromise.

### Why Enumeration Is Crucial for OSCP: {#70e3 .graf .graf--h3 .graf-after--p name="70e3"}

1.  [**Discovery of Attack Vectors:** Enumeration helps identify
    weaknesses in systems and services.]{#32c1}
2.  [**Preparation for Exploitation:** Detailed knowledge about a target
    increases the chances of a successful exploit.]{#119b}
3.  [**Pivoting and Privilege Escalation:** Insights from enumeration
    can be used to move laterally or escalate privileges within a
    network.]{#172b}

### Preparation for Enumeration {#dc02 .graf .graf--h3 .graf-after--li name="dc02"}

Before diving into enumeration, ensure that you have the following tools
and resources ready:

1.  [**Kali Linux or Parrot Security OS:** Pre-installed with most tools
    required for enumeration.]{#d057}
2.  [**VPN Configuration File:** Connect securely to the OSCP lab
    environment.]{#aeb1}
3.  [**Notetaking Tool:** Tools like CherryTree, OneNote, or Joplin for
    documenting findings.]{#fd36}
4.  [**Network Mapping:** Tools like Nmap and Netdiscover to identify
    targets.]{#e26f}
5.  [**A Structured Workflow:** Follow a logical progression from
    discovery to in-depth enumeration.]{#b91f}

### Phases of Enumeration {#599a .graf .graf--h3 .graf-after--li name="599a"}

### 1. Network Enumeration {#1c4d .graf .graf--h3 .graf-after--h3 name="1c4d"}

Network enumeration identifies live hosts, services, and open ports. Use
the following tools and commands:

#### Nmap --- The Swiss Army Knife {#3f51 .graf .graf--h4 .graf-after--p name="3f51"}

Nmap is one of the most versatile tools for network enumeration. Here
are some commonly used commands:

- [**Basic Scan:**]{#280b}
- [`nmap -sC -sV -oN basic_scan.txt <target-ip>`{.markup--code
  .markup--li-code}]{#71ba}
- [`-sC`{.markup--code .markup--li-code}: Run default scripts.]{#556d}
- [`-sV`{.markup--code .markup--li-code}: Version detection.]{#a600}
- [`-oN`{.markup--code .markup--li-code}: Output results to a
  file.]{#fcb6}

**Aggressive Scan:**

- [`nmap -A -oN aggressive_scan.txt <target-ip>`{.markup--code
  .markup--li-code}]{#da36}
- [Includes OS detection, script scanning, and traceroute.]{#713c}
- [**Specific Ports:**]{#073c}
- [`nmap -p 80,443,8080 -oN specific_ports.txt <target-ip>`{.markup--code
  .markup--li-code}]{#f1c2}

**All Ports Scan:**

- [`nmap -p- -oN all_ports.txt <target-ip>`{.markup--code
  .markup--li-code}]{#51d7}
- [Scans all 65,535 ports.]{#da05}

#### Netdiscover {#245e .graf .graf--h4 .graf-after--li name="245e"}

Identify live hosts on the network:

``` {#6c98 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="go"}
netdiscover -r <network-range>
```

#### Ping Sweep {#263c .graf .graf--h4 .graf-after--pre name="263c"}

Check for live hosts:

``` {#2191 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
fping -a -g <network-range>
```

### 2. Service Enumeration {#e4d5 .graf .graf--h3 .graf-after--pre name="e4d5"}

Once open ports are identified, focus on the services running on those
ports. Common tools include:

#### HTTP/HTTPS Services {#08b8 .graf .graf--h4 .graf-after--p name="08b8"}

- [**Nikto:**]{#bbc8}
- [`nikto -h http://<target-ip>`{.markup--code .markup--li-code}]{#042c}
- [**Gobuster (Directory Brute-forcing):**]{#bdbe}
- [`gobuster dir -u http://<target-ip> -w /usr/share/wordlists/dirb/common.txt`{.markup--code
  .markup--li-code}]{#101e}
- [**WhatWeb:** Identify web technologies:]{#f7ce}
- [`whatweb <target-ip>`{.markup--code .markup--li-code}]{#8dd8}

#### SMB Services {#6625 .graf .graf--h4 .graf-after--li name="6625"}

- [**Enum4Linux:**]{#6d21}
- [`enum4linux -a <target-ip>`{.markup--code .markup--li-code}]{#17fc}
- [**smbclient:**]{#5939}
- [`smbclient -L //<target-ip> -U ""`{.markup--code
  .markup--li-code}]{#180c}
- [**CrackMapExec:**]{#77b3}
- [`crackmapexec smb <target-ip> --shares`{.markup--code
  .markup--li-code}]{#d444}

#### FTP Services {#b54d .graf .graf--h4 .graf-after--li name="b54d"}

- [**Anonymous Login Check:**]{#5c91}
- [`ftp <target-ip>`{.markup--code .markup--li-code}]{#ca90}
- [Use `anonymous`{.markup--code .markup--li-code} as the username and
  leave the password blank.]{#5d1c}
- [**Banner Grabbing:**]{#cd5f}
- [`nc -nv <target-ip> 21`{.markup--code .markup--li-code}]{#db21}

#### SSH Services {#1909 .graf .graf--h4 .graf-after--li name="1909"}

- [**Check for Weak Credentials:**]{#9705}
- [`hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://<target-ip>`{.markup--code
  .markup--li-code}]{#c8d0}

### 3. OS Enumeration {#ae34 .graf .graf--h3 .graf-after--li name="ae34"}

Identifying the operating system can narrow down your attack strategy:

- [**Nmap OS Detection:**]{#2bee}
- [`nmap -O <target-ip>`{.markup--code .markup--li-code}]{#3cc7}

**Xprobe2:**

- [`xprobe2 -v <target-ip>`{.markup--code .markup--li-code}]{#d72f}
- [**TTL Analysis:** Use TTL values in ping responses to guess the
  OS:]{#d01d}
- [**Linux:** TTL \~64]{#2ae4}
- [**Windows:** TTL \~128]{#e65e}

### 4. Vulnerability Enumeration {#d94e .graf .graf--h3 .graf-after--li name="d94e"}

After identifying services, search for known vulnerabilities:

#### SearchSploit: {#5583 .graf .graf--h4 .graf-after--p name="5583"}

Locate exploits from Exploit-DB:

``` {#fbfe .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
searchsploit <service-name> <version>
```

#### Nmap NSE Scripts: {#04ea .graf .graf--h4 .graf-after--pre name="04ea"}

Run specific scripts to enumerate vulnerabilities:

``` {#c886 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap --script vuln <target-ip>
```

#### Online Resources: {#1150 .graf .graf--h4 .graf-after--pre name="1150"}

- [**CVE Details:** Use sites like [CVE
  Details](https://www.cvedetails.com){.markup--anchor
  .markup--li-anchor data-href="https://www.cvedetails.com"
  rel="noopener" target="_blank"} to search for vulnerabilities.]{#b80b}
- [**Rapid7 Database:** Search for Metasploit modules.]{#a60d}

### 5. Database Enumeration {#1c8f .graf .graf--h3 .graf-after--li name="1c8f"}

If database services are exposed, enumerate them for potential access.

#### MySQL: {#33aa .graf .graf--h4 .graf-after--p name="33aa"}

- [Check for Default Login:]{#5aba}
- [`mysql -u root -p -h <target-ip>`{.markup--code
  .markup--li-code}]{#b769}
- [Enumerate Databases:]{#e4b1}
- [`SHOW DATABASES;`{.markup--code .markup--li-code}]{#d612}

#### PostgreSQL: {#db6c .graf .graf--h4 .graf-after--li name="db6c"}

- [Connect to Database:]{#de98}
- [`psql -h <target-ip> -U postgres`{.markup--code
  .markup--li-code}]{#037b}
- [List Databases]{#b83d}
- [`\l`{.markup--code .markup--li-code}]{#037c}

### 6. Password Cracking and User Enumeration {#0214 .graf .graf--h3 .graf-after--li name="0214"}

#### Hydra: {#45a7 .graf .graf--h4 .graf-after--h3 name="45a7"}

Brute-force login credentials:

``` {#7ce9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
hydra -L usernames.txt -P passwords.txt <protocol>://<target-ip>
```

#### John the Ripper: {#5d94 .graf .graf--h4 .graf-after--pre name="5d94"}

Crack password hashes:

``` {#12a0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
john --wordlist=/usr/share/wordlists/rockyou.txt <hash-file>
```

#### CrackMapExec: {#d9b0 .graf .graf--h4 .graf-after--pre name="d9b0"}

Brute-force SMB credentials:

``` {#ab55 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
crackmapexec smb <target-ip> -u users.txt -p passwords.txt
```

### 7. Privileged Access and Post-Enumeration {#26a1 .graf .graf--h3 .graf-after--pre name="26a1"}

After successful exploitation, enumerate further to escalate privileges
or move laterally:

#### LinPEAS: {#c58e .graf .graf--h4 .graf-after--p name="c58e"}

Automate privilege escalation enumeration:

``` {#221c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
./linpeas.sh
```

#### Windows Exploitation: {#9bbf .graf .graf--h4 .graf-after--pre name="9bbf"}

Use tools like WinPEAS or manually enumerate for:

- [Unquoted Service Paths]{#d988}
- [Weak Registry Permissions]{#749f}
- [Stored Credentials]{#4c9f}

#### Linux Exploitation: {#ace3 .graf .graf--h4 .graf-after--li name="ace3"}

- [**Check for SUID Binaries:**]{#53f9}
- [`find / -perm -u=s -type f 2>/dev/null`{.markup--code
  .markup--li-code}]{#f14e}

**Kernel Exploits:**

- [`uname -r searchsploit linux kernel <version>`{.markup--code
  .markup--li-code}]{#c836}

### Tips for OSCP Enumeration {#f678 .graf .graf--h3 .graf-after--li name="f678"}

1.  [**Stick to the Scope:** Avoid scanning out-of-scope IPs.]{#e039}
2.  [**Document Everything:** Maintain detailed notes of findings and
    commands used.]{#e793}
3.  [**Time Management:** Don't spend too long on any one enumeration
    technique.]{#53fb}
4.  [**Know Your Tools:** Master the tools mentioned above to use them
    effectively under time constraints.]{#8d67}
5.  [**Practice:** Set up vulnerable VMs like Hack The Box, VulnHub, or
    TryHackMe to hone your enumeration skills.]{#ec8e}

### Conclusion {#89dd .graf .graf--h3 .graf-after--li name="89dd"}

Enumeration is a foundational skill for any penetration tester and a
critical component of the OSCP exam. By systematically applying the
techniques and tools outlined in this cheat sheet, you can uncover
valuable information about your target, paving the way for successful
exploitation. Consistent practice and a methodical approach will not
only prepare you for the OSCP but also set you apart as a skilled
cybersecurity professional. Happy hacking!

### Promote and Collaborate on Cybersecurity Insights {#f6b7 .graf .graf--h3 .graf-after--p name="f6b7"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#3909 .graf .graf--h3 .graf-after--p name="3909"}

[Vijay
Gupta](https://www.youtube.com%2F@www.youtube.com/@bevijaygupta){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com%2F@www.youtube.com/@bevijaygupta"
rel="noopener ugc nofollow noopener" target="_blank"} is a cybersecurity
enthusiast with several years of experience in cyber security, [cyber
crime forensics
investigation](https://www.amazon.com/dp/B0CW4L574N){.markup--anchor
.markup--p-anchor data-href="https://www.amazon.com/dp/B0CW4L574N"
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
.h-card} on [December 23, 2024](https://medium.com/p/1b8c2d04e8bc).

[Canonical
link](https://medium.com/@bevijaygupta/oscp-enumeration-cheat-sheet-1b8c2d04e8bc){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
