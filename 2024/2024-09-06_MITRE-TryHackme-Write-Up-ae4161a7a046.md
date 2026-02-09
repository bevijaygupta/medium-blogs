---
title: "MITRE TryHackme Write Up ae4161a7a046"
platform: Medium
original_file: 2024-09-06_MITRE-TryHackme-Write-Up-ae4161a7a046.md
---

# MITRE TryHackme Write Up ae4161a7a046

::: {}
# MITRE TryHackme Write-Up {#mitre-tryhackme-write-up .p-name}
:::

::: {.section .p-summary field="subtitle"}
TASK 1 & 2 are simple click and complete tasks
:::

::::::: {.section .e-content field="body"}
:::::: {#9b08 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### MITRE TryHackme Write-Up {#e9d3 .graf .graf--h3 .graf--leading .graf--title name="e9d3"}

<figure id="d405" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*82nKnWKXg-08kDgK.png"
class="graf-image" data-image-id="0*82nKnWKXg-08kDgK.png"
data-width="875" data-height="150" />
</figure>

**TASK 1 & 2** are simple click and complete tasks

**TASK 3**

**Question 1:** Only blue teamers will use the ATT&CK Matrix? (Yay/Nay)

``` {#fdf1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Nay
```

**Question 2:** What is the ID for this technique?

``` {#75fc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
T1566
```

**Question 3:** Based on this technique, what mitigation covers
identifying social engineering techniques?

``` {#f57b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
User Training
```

**Question 4:** There are other possible areas for detection for this
technique, which occurs after what other technique?

``` {#ed5e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
User Execution
```

**Question 5:** What group has used spear phishing in their campaigns?

``` {#5977 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Dragonfly
```

**Question 6:** Based on the information for this group, what are their
associated groups?

``` {#fee2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
TG-4192, Crouching Yeti, IRON LIBERTY, Energetic Bear
```

**Question 7:** What tool is attributed to this group to transfer tools
or files from one host to another within a compromised environment?

``` {#03cd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
PsExec
```

**Question 8:** Based on the information about this tool, what group
used a customized version of it?

``` {#ec58 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
FIN5
```

**Question 9:** This group has been active since what year?

``` {#7c82 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
2008
```

**Question 10:**Instead of Mimikatz, what OS Credential Dumping tool is
does this group use?

``` {#4739 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Windows Credential Editor
```

### Task 4 {#6e50 .graf .graf--h3 .graf-after--pre name="6e50"}

**Question 1:** For the above analytic, what is the pseudocode a
representation of?

``` {#24ad .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
Splunk search
```

**Question 2:** What tactic has an ID of TA0003?

``` {#8796 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Persistence
```

**Question 3:** What is the name of the library that is a collection of
Zeek (BRO) scripts?

``` {#1b17 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
BZAR
```

**Question 4:** What is the name of the technique for running
executables with the same hash and different names?

``` {#9c63 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Masquerading
```

**Question 5:** Examine CAR-2013--05--004, what additional information
is provided to analysts to ensure coverage for this technique?

``` {#530d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
Unit Tests
```

### Task 5 {#c24c .graf .graf--h3 .graf-after--pre name="c24c"}

**Question 1:**Which Shield tactic has the most techniques?

``` {#cdb9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Detect
```

**Question 2:** Is the technique 'Decoy Credentials' listed under the
tactic from question #1? (Yay/Nay)

``` {#bc98 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Yay
```

**Question 3:** Explore DTE0011, what is the ID for the use case where a
defender can plant artifacts on a system to make it look like a virtual
machine to the adversary?

``` {#e629 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
DUC0234
```

**Question 4:** Based on the above use case, what is its ATT&CK®
Technique mapping?

``` {#1762 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
T1497
```

**Question 5:**Continuing from the previous question, look at the
information for this ATT&CK® Technique, what 2 programs are listed that
adversary's will check for?

``` {#5cf5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Sysinternals and Wireshark
```

### Task 6 {#262a .graf .graf--h3 .graf-after--pre name="262a"}

**Question 1:** How many phases does APT3 Emulation Plan consists of?

``` {#7b1c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
3
```

**Question 2:** Under Persistence, what binary was replaced with
cmd.exe?

``` {#9ec7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
sethc.exe
```

**Question 3:** Examining APT29, what 2 tools were used to execute the
first scenario?

``` {#6248 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Pupy and Meterpreter
```

**Question 4:** What tool was used to execute the second scenario?

``` {#10a2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
PoshC2
```

**Question 5:** Where can you find step-by-step instructions to execute
both scenarios?

``` {#6d9d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ATT&CK Arsenal
```

### Task 7 {#c6cd .graf .graf--h3 .graf-after--pre name="c6cd"}

**Question 1:** What is a group that targets your sector who has been in
operation since at least 2013?

``` {#8662 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
APT33
```

**Question 2:** Does this group use Stuxnet? (Yay/Nay)

``` {#07d0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Nay
```

**Question 3:** As your organization is migrating to the cloud, is there
anything attributed to this APT group that you should focus on? If so,
what is it?

``` {#2a46 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Cloud Accounts
```

**Question 4:** What tool is associated with this technique?

``` {#4744 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Ruler
```

**Question 5:** Per the detection tip, what should you be detecting?

``` {#a273 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
Abnormal or malicious behavior
```

**Question 6:** What platforms does this affect?

``` {#fc58 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
AWS, Azure, Azure AD, GCP, Office 365, SaaS
```

### Promote and Collaborate on Cybersecurity Insights {#e38d .graf .graf--h3 .graf-after--pre name="e38d"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#ff57 .graf .graf--h3 .graf-after--p name="ff57"}

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
.h-card} on [September 6, 2024](https://medium.com/p/ae4161a7a046).

[Canonical
link](https://medium.com/@bevijaygupta/mitre-tryhackme-write-up-ae4161a7a046){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
