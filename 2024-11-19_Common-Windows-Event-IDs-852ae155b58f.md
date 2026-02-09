::: {}
# Common Windows Event IDs {#common-windows-event-ids .p-name}
:::

::: {.section .p-summary field="subtitle"}
Windows Event Logs are one of the most crucial sources of information
for Security Operations Center (SOC) analysts, administrators, and...
:::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#4766 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Common Windows Event IDs {#d515 .graf .graf--h3 .graf--leading .graf--title name="d515"}

<figure id="77ae" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*4yq8wagdm2QStDIJ"
class="graf-image" data-image-id="0*4yq8wagdm2QStDIJ" data-width="1280"
data-height="720" />
</figure>

Windows Event Logs are one of the most crucial sources of information
for Security Operations Center (SOC) analysts, administrators, and
forensic investigators. These logs contain a wealth of data, but the
sheer volume can be overwhelming without a solid understanding of
**Event IDs** --- unique identifiers assigned to specific types of
events. In this guide, we'll dive deep into the most common Event IDs,
their meanings, and how they help security professionals monitor,
analyze, and respond to system activities.
:::
::::
::::::

:::::: {#689a .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Why Event IDs Matter {#303d .graf .graf--h3 .graf--leading name="303d"}

Event IDs are like breadcrumbs left by the operating system, guiding us
toward a clear understanding of what's happening under the hood. For a
SOC analyst, they:

1.  [**Provide Context**: Event IDs explain the nature of an event,
    whether it's a login attempt, system error, or software
    installation.]{#6674}
2.  [**Streamline Monitoring**: Analysts can filter logs by specific
    Event IDs to focus on critical activities.]{#5064}
3.  [**Enhance Threat Detection**: Recognizing malicious patterns tied
    to certain Event IDs helps analysts detect and respond to security
    threats.]{#3fe0}
4.  [**Support Incident Investigations**: Forensic analysts rely on
    Event IDs to reconstruct events leading to a security
    incident.]{#65d9}
:::
::::
::::::

:::::: {#1c21 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Key Event Logs and Their Categories {#88fb .graf .graf--h3 .graf--leading name="88fb"}

Windows logs are categorized into different types, each serving a
specific purpose. Here's a quick overview:

### 1. System Logs {#d0a5 .graf .graf--h3 .graf-after--p name="d0a5"}

These logs track events related to system operations, such as driver
issues, service failures, or hardware errors.

### 2. Security Logs {#dabc .graf .graf--h3 .graf-after--p name="dabc"}

Security logs record activities like logins, logouts, account
management, and policy changes. They are the most critical logs for SOC
analysts.

### 3. Application Logs {#71b3 .graf .graf--h3 .graf-after--p name="71b3"}

These logs capture application-specific events, such as errors in
installed software.

### 4. Setup Logs {#ac21 .graf .graf--h3 .graf-after--p name="ac21"}

Events related to the installation or setup of the operating system.

### 5. Forwarded Events {#c0d3 .graf .graf--h3 .graf-after--p name="c0d3"}

These logs collect events from other systems for centralized monitoring.
:::
::::
::::::

:::::: {#e4b4 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Critical Event IDs Every SOC Analyst Should Know {#94e1 .graf .graf--h3 .graf--leading name="94e1"}

Let's break down the most common Event IDs, their meanings, and how
they're used in security operations.
:::
::::
::::::

:::::: {#f0a4 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Account Logon Events {#6ce6 .graf .graf--h3 .graf--leading name="6ce6"}

#### 1. Event ID 4624 --- Successful Logon {#ec07 .graf .graf--h4 .graf-after--h3 name="ec07"}

**Description**: This Event ID indicates that a user successfully logged
into the system.\
**Why It Matters**: It helps track legitimate user access and detect
suspicious login patterns.

**Key Fields to Review**:

- [**Logon Type**: Identifies the nature of the logon. For
  example:]{#ff6f}
- [Type 2: Interactive logon (user at the console).]{#6718}
- [Type 3: Network logon (e.g., accessing shared folders).]{#ea96}
- [Type 10: Remote Desktop Protocol (RDP) session.]{#8c0b}
- [**Account Name**: The username of the account that logged in.]{#439b}
:::
::::
::::::

:::::: {#2bce .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 2. Event ID 4625 --- Failed Logon {#2540 .graf .graf--h4 .graf--leading name="2540"}

**Description**: This Event ID is generated when a user login attempt
fails.\
**Why It Matters**: Failed logons could indicate brute force attacks or
unauthorized access attempts.

**Key Fields to Review**:

- [**Failure Reason**: Provides insights into why the login failed
  (e.g., bad password, disabled account).]{#d3ae}
- [**Source Network Address**: The IP address of the machine attempting
  the login.]{#3e74}
:::
::::
::::::

:::::: {#0532 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 3. Event ID 4768 --- Kerberos Authentication Ticket (TGT) Issued {#6e5a .graf .graf--h4 .graf--leading name="6e5a"}

**Description**: Indicates that a Kerberos Ticket Granting Ticket was
issued.\
**Why It Matters**: Useful for monitoring authentication activity and
detecting unusual patterns in ticket issuance.
:::
::::
::::::

:::::: {#0dd3 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 4. Event ID 4771 --- Kerberos Pre-Authentication Failure {#3a55 .graf .graf--h4 .graf--leading name="3a55"}

**Description**: This Event ID is logged when Kerberos
pre-authentication fails.\
**Why It Matters**: Frequent failures may indicate password spray
attacks or misconfigurations.
:::
::::
::::::

:::::: {#0800 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Privilege Use Events {#afb6 .graf .graf--h3 .graf--leading name="afb6"}

#### 5. Event ID 4672 --- Special Privileges Assigned to New Logon {#3559 .graf .graf--h4 .graf-after--h3 name="3559"}

**Description**: Logged when a user logs on with administrative
privileges.\
**Why It Matters**: Helps detect privileged account activity, which is
critical for spotting insider threats or compromised admin accounts.
:::
::::
::::::

:::::: {#f108 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 6. Event ID 4688 --- Process Creation {#fae4 .graf .graf--h4 .graf--leading name="fae4"}

**Description**: Logs the creation of a new process.\
**Why It Matters**: Useful for tracking potentially malicious processes,
such as malware execution.

**Key Fields to Review**:

- [**Parent Process ID**: Identifies the parent process that spawned the
  new one.]{#1fce}
- [**New Process Name**: The executable associated with the
  process.]{#945e}
:::
::::
::::::

:::::: {#20bd .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Object Access Events {#7b54 .graf .graf--h3 .graf--leading name="7b54"}

#### 7. Event ID 4656 --- Handle to an Object Requested {#065d .graf .graf--h4 .graf-after--h3 name="065d"}

**Description**: Logged when a user requests access to an object, such
as a file or registry key.\
**Why It Matters**: Useful for detecting unauthorized access to
sensitive files or system resources.
:::
::::
::::::

:::::: {#ddbb .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 8. Event ID 4663 --- Object Accessed {#e93f .graf .graf--h4 .graf--leading name="e93f"}

**Description**: Indicates that a user accessed an object, such as a
file, folder, or registry key.\
**Why It Matters**: Critical for monitoring data exfiltration or insider
threats.
:::
::::
::::::

:::::: {#80c2 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Policy Changes and Account Management {#523d .graf .graf--h3 .graf--leading name="523d"}

#### 9. Event ID 4738 --- User Account Changed {#d7b6 .graf .graf--h4 .graf-after--h3 name="d7b6"}

**Description**: Logged when changes are made to a user account, such as
password resets or permission modifications.\
**Why It Matters**: Helps track unauthorized or suspicious account
changes.
:::
::::
::::::

:::::: {#d597 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 10. Event ID 4719 --- System Audit Policy Changed {#bf2b .graf .graf--h4 .graf--leading name="bf2b"}

**Description**: Indicates modifications to the system's audit
policies.\
**Why It Matters**: Unusual changes to audit policies may be an attempt
to cover malicious activity.
:::
::::
::::::

:::::: {#ef27 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Network and Remote Access Events {#0fb0 .graf .graf--h3 .graf--leading name="0fb0"}

#### 11. Event ID 4627 --- Group Membership Enumeration {#7c69 .graf .graf--h4 .graf-after--h3 name="7c69"}

**Description**: Logged when a user queries group memberships.\
**Why It Matters**: Attackers often query group memberships to identify
privileged accounts.
:::
::::
::::::

:::::: {#64f8 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 12. Event ID 5140 --- File Share Accessed {#2a45 .graf .graf--h4 .graf--leading name="2a45"}

**Description**: Indicates that a network share was accessed.\
**Why It Matters**: Useful for detecting lateral movement or data theft
attempts.
:::
::::
::::::

:::::: {#32fb .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 13. Event ID 4648 --- Logon Using Explicit Credentials {#e18e .graf .graf--h4 .graf--leading name="e18e"}

**Description**: Logged when a user attempts to log on using alternate
credentials.\
**Why It Matters**: Could indicate pass-the-hash or other credential
misuse attacks.
:::
::::
::::::

:::::: {#fab3 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Malicious Activity Detection {#a417 .graf .graf--h3 .graf--leading name="a417"}

#### 14. Event ID 1102 --- Audit Log Cleared {#721e .graf .graf--h4 .graf-after--h3 name="721e"}

**Description**: Logged when the event logs are cleared.\
**Why It Matters**: Often a sign of malicious activity, as attackers may
clear logs to cover their tracks.
:::
::::
::::::

:::::: {#33e0 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
#### 15. Event ID 7035/7036 --- Service Control Manager Events {#dad7 .graf .graf--h4 .graf--leading name="dad7"}

**Description**: Logs service state changes, such as starting or
stopping a service.\
**Why It Matters**: Sudden or unexpected service state changes can be an
indicator of malware or attacker activity.
:::
::::
::::::

:::::: {#26f2 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Using Event Logs Effectively in SOC Operations {#e430 .graf .graf--h3 .graf--leading name="e430"}

### Filtering for Relevance {#8eec .graf .graf--h3 .graf-after--h3 name="8eec"}

With thousands of events generated daily, it's vital to filter out
noise. Use log management tools like Splunk, Elastic Stack, or SIEM
solutions to focus on high-priority Event IDs.

### Correlating Events {#b923 .graf .graf--h3 .graf-after--p name="b923"}

Rarely does a single Event ID tell the full story. Correlate events
across multiple IDs to build a timeline of activities, such as:

1.  [A failed logon (Event ID 4625).]{#e701}
2.  [Followed by a successful logon (Event ID 4624).]{#7746}
3.  [Culminating in a suspicious process creation (Event ID
    4688).]{#56b8}

### Automating Threat Detection {#3639 .graf .graf--h3 .graf-after--li name="3639"}

SOC analysts can use SIEM solutions to create detection rules for
critical Event IDs. For example:

- [Alert if Event ID 1102 (Audit Log Cleared) is logged.]{#ce89}
- [Trigger a high-severity alarm if multiple failed logons (Event
  ID 4625) are followed by a successful logon.]{#c23f}

### Leveraging Threat Intelligence {#dd24 .graf .graf--h3 .graf-after--li name="dd24"}

Combine Event Log analysis with threat intelligence feeds to enrich the
context around suspicious activities.
:::
::::
::::::

:::::: {#e4c2 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Conclusion {#cd07 .graf .graf--h3 .graf--leading name="cd07"}

Understanding Windows Event IDs is an indispensable skill for SOC
analysts, administrators, and forensic investigators. These identifiers
provide a roadmap for monitoring, detecting, and responding to system,
security, and application events.

By familiarizing yourself with critical Event IDs, adopting advanced log
analysis tools, and correlating events effectively, you can transform
raw log data into actionable intelligence --- ensuring robust security
for your organization.
:::
::::
::::::

:::::: {#6e5d .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**What's your experience with Windows Event Logs? Share your insights or
questions in the comments below!**

### Promote and Collaborate on Cybersecurity Insights {#ce46 .graf .graf--h3 .graf-after--p name="ce46"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#5d17 .graf .graf--h3 .graf-after--p name="5d17"}

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
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [November 19, 2024](https://medium.com/p/852ae155b58f).

[Canonical
link](https://medium.com/@bevijaygupta/common-windows-event-ids-852ae155b58f){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
