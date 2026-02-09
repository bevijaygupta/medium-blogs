---
title: "40 Methods for Privilege Escalation 51699f2f22cc"
platform: Medium
original_file: 2024-11-16_40-Methods-for-Privilege-Escalation-51699f2f22cc.md
---

# 40 Methods for Privilege Escalation 51699f2f22cc

::: {}
# 40 Methods for Privilege Escalation {#methods-for-privilege-escalation .p-name}
:::

::: {.section .p-summary field="subtitle"}
Privilege escalation is a critical phase in penetration testing, where
an attacker exploits vulnerabilities to gain higher-level...
:::

::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#2fc0 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 40 Methods for Privilege Escalation {#92d5 .graf .graf--h3 .graf--leading .graf--title name="92d5"}

<figure id="3d33" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*9dyAre8FZeDZvauz.png"
class="graf-image" data-image-id="0*9dyAre8FZeDZvauz.png"
data-width="623" data-height="348" data-is-featured="true" />
</figure>

Privilege escalation is a critical phase in penetration testing, where
an attacker exploits vulnerabilities to gain higher-level permissions
within a system or network. For ethical hackers, mastering this skill is
essential to evaluate system security and recommend appropriate
mitigations effectively.

In this guide, we'll dive deep into **40 methods for privilege
escalation**, categorized by platform (Windows, Linux, and others), and
discuss how ethical hackers can use these methods responsibly to
strengthen cybersecurity.
:::
::::
::::::

:::::: {#5f2a .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Understanding Privilege Escalation {#388a .graf .graf--h3 .graf--leading name="388a"}

Privilege escalation occurs when a user gains access to privileges or
permissions beyond what was intended. This can happen in two forms:

1.  [**Vertical Privilege Escalation:** Gaining higher privileges, like
    escalating from a regular user to an administrator.]{#5156}
2.  [**Horizontal Privilege Escalation:** Gaining access to another
    user's account with similar privilege levels.]{#9dda}

### Why It Matters {#cab1 .graf .graf--h3 .graf-after--li name="cab1"}

Understanding privilege escalation is critical for:

- [Identifying vulnerabilities that attackers might exploit.]{#0d74}
- [Testing systems for compliance with security standards.]{#23c6}
- [Educating organizations about effective countermeasures.]{#555c}
:::
::::
::::::

:::::: {#8fc4 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 40 Methods for Privilege Escalation {#41a7 .graf .graf--h3 .graf--leading name="41a7"}

### Part 1: Privilege Escalation on Windows {#6f34 .graf .graf--h3 .graf-after--h3 name="6f34"}

Windows systems often contain misconfigurations and vulnerabilities that
attackers can exploit for privilege escalation.

#### 1. Exploiting Unquoted Service Paths {#efbd .graf .graf--h4 .graf-after--p name="efbd"}

- [Services with unquoted paths can be manipulated to execute malicious
  executables.]{#92d1}
- [Example: Replacing files in
  `C:\Program Files\Some Path With Space\service.exe`{.markup--code
  .markup--li-code}.]{#67d7}

#### 2. Exploiting Weak Folder Permissions {#1549 .graf .graf--h4 .graf-after--li name="1549"}

- [Misconfigured permissions on critical folders allow attackers to
  replace executables or DLLs.]{#0425}

#### 3. Registry Key Manipulation {#38b8 .graf .graf--h4 .graf-after--li name="38b8"}

- [Misconfigured registry keys can be modified to execute arbitrary code
  upon system boot.]{#fff4}
- [Example: Abuse
  `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`{.markup--code
  .markup--li-code}.]{#60a1}

#### 4. DLL Hijacking {#024d .graf .graf--h4 .graf-after--li name="024d"}

- [Placing malicious DLLs in locations where the system expects
  legitimate ones.]{#cc2f}

#### 5. Scheduled Tasks Abuse {#6c46 .graf .graf--h4 .graf-after--li name="6c46"}

- [Creating or modifying scheduled tasks to execute malicious payloads
  with SYSTEM privileges.]{#36a7}

#### 6. Exploiting AlwaysInstallElevated {#6fff .graf .graf--h4 .graf-after--li name="6fff"}

- [A misconfigured policy allowing MSI packages to run with elevated
  privileges.]{#9fd8}

#### 7. Insecure Service Configurations {#279c .graf .graf--h4 .graf-after--li name="279c"}

- [Services configured with weak permissions can be exploited to execute
  malicious binaries.]{#6745}

#### 8. Token Impersonation {#54fa .graf .graf--h4 .graf-after--li name="54fa"}

- [Stealing access tokens of higher-privilege users or processes to
  escalate privileges.]{#112d}

#### 9. SAM and SYSTEM File Extraction {#2f29 .graf .graf--h4 .graf-after--li name="2f29"}

- [Extracting hashes from `SAM`{.markup--code .markup--li-code} and
  `SYSTEM`{.markup--code .markup--li-code} files to crack or
  pass-the-hash attacks.]{#6ce2}

#### 10. Kernel Exploits {#8df6 .graf .graf--h4 .graf-after--li name="8df6"}

- [Exploiting vulnerabilities in the Windows kernel to escalate
  privileges.]{#3236}

#### 11. UAC Bypass {#e0bc .graf .graf--h4 .graf-after--li name="e0bc"}

- [Abuse misconfigured User Account Control (UAC) to bypass privilege
  restrictions.]{#50f7}

#### 12. Credential Dumping {#f77a .graf .graf--h4 .graf-after--li name="f77a"}

- [Using tools like Mimikatz to extract credentials from memory and
  escalate.]{#f8b6}

#### 13. Abusing Remote Desktop {#e8c3 .graf .graf--h4 .graf-after--li name="e8c3"}

- [Leveraging saved credentials or insecure RDP configurations to gain
  higher privileges.]{#d802}

#### 14. Password Spraying {#86a0 .graf .graf--h4 .graf-after--li name="86a0"}

- [Attempting commonly used passwords to escalate privileges.]{#c6bf}

#### 15. Exploiting Writable Services {#1443 .graf .graf--h4 .graf-after--li name="1443"}

- [Modifying services with writable permissions to execute arbitrary
  code.]{#6a5e}

#### 16. GPP (Group Policy Preferences) Abuse {#365a .graf .graf--h4 .graf-after--li name="365a"}

- [Extracting plaintext passwords from GPP XML files on domain
  controllers.]{#e238}

#### 17. Privileged Account Enumeration {#ad3a .graf .graf--h4 .graf-after--li name="ad3a"}

- [Identifying privileged accounts and exploiting weak credentials or
  sessions.]{#c210}

#### 18. Abusing Startup Scripts {#8ef9 .graf .graf--h4 .graf-after--li name="8ef9"}

- [Adding malicious scripts to locations executed at boot or
  login.]{#f5e9}

#### 19. Abusing WMI (Windows Management Instrumentation) {#2f88 .graf .graf--h4 .graf-after--li name="2f88"}

- [Using WMI to execute payloads or modify configurations with elevated
  privileges.]{#8c86}

#### 20. Weak Local Admin Passwords {#d338 .graf .graf--h4 .graf-after--li name="d338"}

- [Brute-forcing or guessing local admin credentials to
  escalate.]{#678d}
:::
::::
::::::

:::::: {#7f8b .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Part 2: Privilege Escalation on Linux {#1e32 .graf .graf--h3 .graf--leading name="1e32"}

Linux privilege escalation often involves exploiting misconfigurations,
permissions, or kernel vulnerabilities.

#### 21. SUID/SGID Executables {#f2f9 .graf .graf--h4 .graf-after--p name="f2f9"}

- [Exploiting binaries with the SUID or SGID bit set to gain elevated
  privileges.]{#6ab4}

#### 22. Exploiting Weak File Permissions {#d951 .graf .graf--h4 .graf-after--li name="d951"}

- [Reading sensitive files like `/etc/shadow`{.markup--code
  .markup--li-code} to crack passwords.]{#3ece}

#### 23. Exploiting Cron Jobs {#847d .graf .graf--h4 .graf-after--li name="847d"}

- [Abusing writable cron job scripts to execute arbitrary commands as
  root.]{#f75d}

#### 24. Kernel Exploits {#2b04 .graf .graf--h4 .graf-after--li name="2b04"}

- [Exploiting vulnerabilities in the Linux kernel to escalate
  privileges.]{#5408}

#### 25. Abusing PATH Variable {#5916 .graf .graf--h4 .graf-after--li name="5916"}

- [Modifying the PATH variable to execute malicious binaries when root
  runs commands.]{#53aa}

#### 26. Privileged Docker Containers {#8666 .graf .graf--h4 .graf-after--li name="8666"}

- [Escaping Docker containers configured with elevated
  privileges.]{#7993}

#### 27. Misconfigured sudo Permissions {#6862 .graf .graf--h4 .graf-after--li name="6862"}

- [Exploiting `sudo`{.markup--code .markup--li-code} configurations to
  run commands as root without a password.]{#b627}
- [Example: `sudo vim`{.markup--code .markup--li-code} can allow shell
  escape.]{#ddab}

#### 28. Exploiting LD_PRELOAD {#75df .graf .graf--h4 .graf-after--li name="75df"}

- [Injecting malicious shared libraries using the
  `LD_PRELOAD`{.markup--code .markup--li-code} environment
  variable.]{#be0e}

#### 29. Overwriting Configuration Files {#f363 .graf .graf--h4 .graf-after--li name="f363"}

- [Modifying configurations for services like SSH to escalate
  privileges.]{#ba4b}

#### 30. Exploiting Writable Scripts {#617b .graf .graf--h4 .graf-after--li name="617b"}

- [Injecting commands into writable scripts executed by root.]{#0210}

#### 31. Exploiting SSH Keys {#af27 .graf .graf--h4 .graf-after--li name="af27"}

- [Using insecurely stored private keys or weak passwords to access root
  accounts.]{#5cd0}

#### 32. Exploiting NFS (Network File System) {#87d2 .graf .graf--h4 .graf-after--li name="87d2"}

- [Gaining root privileges by abusing insecure NFS exports.]{#4222}

#### 33. Exploiting X11 Permissions {#285e .graf .graf--h4 .graf-after--li name="285e"}

- [Using X11 session permissions to capture keystrokes or execute
  commands as root.]{#9c78}

#### 34. Abusing Capabilities {#f89c .graf .graf--h4 .graf-after--li name="f89c"}

- [Exploiting binaries with elevated capabilities, such as
  `CAP_NET_ADMIN`{.markup--code .markup--li-code}.]{#50b5}

#### 35. Writable /etc/passwd File {#0e0c .graf .graf--h4 .graf-after--li name="0e0c"}

- [Modifying `/etc/passwd`{.markup--code .markup--li-code} to add a new
  root user.]{#7c60}
:::
::::
::::::

:::::: {#5a7c .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Part 3: Platform-Agnostic Methods {#fbf5 .graf .graf--h3 .graf--leading name="fbf5"}

Certain privilege escalation techniques are applicable across multiple
platforms.

#### 36. Exploiting Misconfigured APIs {#f2f4 .graf .graf--h4 .graf-after--p name="f2f4"}

- [Using APIs that inadvertently expose privileged operations.]{#da70}

#### 37. Exploiting Vulnerable Applications {#b2e0 .graf .graf--h4 .graf-after--li name="b2e0"}

- [Targeting third-party applications with known vulnerabilities to
  escalate.]{#f7b4}

#### 38. Abusing Shared Folders {#9415 .graf .graf--h4 .graf-after--li name="9415"}

- [Modifying shared folders containing sensitive or executable
  files.]{#1f38}

#### 39. Social Engineering Privileged Users {#8911 .graf .graf--h4 .graf-after--li name="8911"}

- [Tricking privileged users into executing malicious files or
  commands.]{#cbb7}

#### 40. Leveraging Exploitation Frameworks {#61d5 .graf .graf--h4 .graf-after--li name="61d5"}

- [Using tools like Metasploit to automate privilege escalation
  attacks.]{#04e5}
:::
::::
::::::

:::::: {#f630 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### How Ethical Hackers Use These Methods {#8bd5 .graf .graf--h3 .graf--leading name="8bd5"}

As ethical hackers, it's important to approach privilege escalation
responsibly:

1.  [**Follow the Scope:** Only use these methods on systems authorized
    for testing.]{#66fe}
2.  [**Document Everything:** Maintain clear records of vulnerabilities
    exploited and their impact.]{#8e66}
3.  [**Report Vulnerabilities:** Share findings with stakeholders and
    provide mitigation strategies.]{#5777}
4.  [**Avoid Data Breach:** Never access sensitive information beyond
    what is required for testing.]{#2e67}
:::
::::
::::::

:::::: {#d7e6 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Mitigation Strategies for Organizations {#706c .graf .graf--h3 .graf--leading name="706c"}

To protect against privilege escalation, organizations should:

- [Implement **principle of least privilege (PoLP)** for user
  accounts.]{#b307}
- [Regularly audit file and folder permissions.]{#86b1}
- [Patch systems and update software to fix vulnerabilities.]{#19d4}
- [Enforce strong password policies.]{#1886}
- [Monitor systems for suspicious activities.]{#22e7}
:::
::::
::::::

:::::: {#f79b .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Conclusion {#032a .graf .graf--h3 .graf--leading name="032a"}

Privilege escalation is a double-edged sword: while it's a critical
skill for ethical hackers, it's also a significant risk for
organizations if not addressed. By understanding these 40 methods,
ethical hackers can uncover vulnerabilities and help organizations build
robust defenses.

When used responsibly, these techniques empower cybersecurity
professionals to stay one step ahead of malicious actors, ensuring the
safety of systems, data, and users.

### Promote and Collaborate on Cybersecurity Insights {#49d2 .graf .graf--h3 .graf-after--p name="49d2"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#919f .graf .graf--h3 .graf-after--p name="919f"}

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
:::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [November 16, 2024](https://medium.com/p/51699f2f22cc).

[Canonical
link](https://medium.com/@bevijaygupta/40-methods-for-privilege-escalation-51699f2f22cc){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
