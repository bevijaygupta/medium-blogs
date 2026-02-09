---
title: "SoC Analyst  Active Directory   Splunk Home Lab 7e01e0db71e2"
platform: Medium
original_file: 2024-10-03_SoC-Analyst--Active-Directory---Splunk-Home-Lab-7e01e0db71e2.md
---

# SoC Analyst  Active Directory   Splunk Home Lab 7e01e0db71e2

::: {}
# SoC Analyst: Active Directory & Splunk Home Lab {#soc-analyst-active-directory-splunk-home-lab .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction
:::

::::::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#62af .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### SoC Analyst: Active Directory & Splunk Home Lab {#e93d .graf .graf--h3 .graf--leading .graf--title name="e93d"}

<figure id="cd38" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*b_8Uuv_3HFRIDNDD.jpg"
class="graf-image" data-image-id="0*b_8Uuv_3HFRIDNDD.jpg"
data-width="740" data-height="493" data-is-featured="true" />
</figure>

### Introduction {#22e9 .graf .graf--h3 .graf-after--figure name="22e9"}

In the cybersecurity landscape, **Security Operations Center (SoC)
Analysts** are at the forefront of defending organizations from cyber
threats. SoC analysts play a crucial role in monitoring, detecting, and
responding to security incidents. To become proficient, it is essential
to build hands-on experience using real-world tools like **Active
Directory** and **Splunk**, which are cornerstones in an enterprise's IT
infrastructure.

A home lab is the perfect environment to simulate an enterprise-like
security setup. With a home lab, aspiring SoC analysts can practice
monitoring, configuring, and troubleshooting security events in a
controlled setting. This blog will walk you through the process of
setting up a home lab featuring **Active Directory** and **Splunk** to
practice skills crucial for a SoC analyst.
:::
::::
::::::

:::::: {#035c .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 1. Why a Home Lab is Essential for a SoC Analyst {#7abe .graf .graf--h3 .graf--leading name="7abe"}

As a SoC analyst, theoretical knowledge alone won't be enough to handle
complex real-world security challenges. Building a **home lab** provides
you with the following key advantages:

- [**Hands-on Experience**: The opportunity to practice skills in a safe
  environment.]{#bce1}
- [**Understanding of Real-World Tools**: Tools like Active Directory
  and Splunk are widely used in enterprises, so familiarity is
  essential.]{#d045}
- [**Simulating Attack Scenarios**: You can simulate different attack
  vectors and incident response strategies.]{#ac03}
- [**Skills Development**: Testing your knowledge, configuring
  environments, and working with logs help solidify concepts essential
  to security monitoring.]{#1c0e}

In a home lab, you can configure a setup that mimics an enterprise
network, offering a sandbox environment to experiment, learn, and refine
your capabilities as a SoC analyst.
:::
::::
::::::

:::::: {#54f6 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 2. Overview of Active Directory and Splunk {#70a5 .graf .graf--h3 .graf--leading name="70a5"}

Before diving into the home lab setup, let's briefly discuss two key
technologies: **Active Directory (AD)** and **Splunk**.

### 2.1 Active Directory {#a277 .graf .graf--h3 .graf-after--p name="a277"}

**Active Directory** (AD) is Microsoft's directory service used by
organizations to manage permissions and access to network resources. AD
organizes users, computers, and other objects in a hierarchical
structure. Its key functions include:

- [**Authentication**: AD manages login credentials for network
  users.]{#5b65}
- [**Authorization**: AD enforces policies that dictate access
  control.]{#4368}
- [**Centralized Management**: IT admins use AD to manage the entire
  network's users, computers, and resources.]{#aa25}

AD is a prime target for attackers, so having a deep understanding of
its structure and logs is critical for a SoC analyst.

### 2.2 Splunk {#1e1f .graf .graf--h3 .graf-after--p name="1e1f"}

**Splunk** is a powerful security information and event management
(SIEM) tool used to analyze large volumes of data. It collects,
monitors, and analyzes logs from various devices, including firewalls,
routers, and servers.

For a SoC analyst, Splunk provides:

- [**Real-time Monitoring**: Collects and monitors logs in real-time for
  security events.]{#269d}
- [**Log Analysis**: Helps identify suspicious patterns and activities
  through log correlation.]{#db1b}
- [**Alerting**: Triggers alerts based on pre-defined security
  conditions.]{#c940}
- [**Incident Response**: Enables analysts to quickly investigate and
  respond to security incidents.]{#f976}
:::
::::
::::::

:::::: {#542b .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 3. Planning the Home Lab: Requirements and Setup {#2385 .graf .graf--h3 .graf--leading name="2385"}

Before setting up your home lab, it's essential to plan the components
and infrastructure required. Here's a list of what you'll need to build
your SoC Analyst home lab:

### Hardware Requirements {#1ded .graf .graf--h3 .graf-after--p name="1ded"}

- [**Computer/Laptop**: A machine with at least 8 GB of RAM (preferably
  16 GB) and a multi-core processor.]{#48cc}
- [**Network Setup**: A basic network with at least one router or
  switch.]{#36c8}

### Software Requirements {#26f6 .graf .graf--h3 .graf-after--li name="26f6"}

- [**Virtualization Software**: You can use **VirtualBox** (free) or
  **VMware** to create virtual machines (VMs).]{#b214}
- [**Windows Server**: You'll need a copy of **Windows Server 2019** or
  **2022** for Active Directory. Microsoft offers trial
  versions.]{#a1e3}
- [**Splunk Free or Splunk Enterprise Trial**: A free version of Splunk
  can be used to process up to 500MB of data per day, which is ideal for
  a home lab.]{#1d53}
- [**Windows 10/11**: For a client machine to simulate real-world
  scenarios.]{#42fa}

### Lab Architecture {#238f .graf .graf--h3 .graf-after--li name="238f"}

Your lab will consist of multiple virtual machines running different
roles:

1.  [**Active Directory Server (Windows Server)**: This will manage
    users, groups, and domain policies.]{#2503}
2.  [**Splunk Server**: For collecting and analyzing logs.]{#9410}
3.  [**Client Machine (Windows 10)**: A user machine that will be part
    of your domain and generate activities to be monitored.]{#77fd}
:::
::::
::::::

:::::: {#5565 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. Step-by-Step Guide to Setting up Active Directory in a Home Lab {#3103 .graf .graf--h3 .graf--leading name="3103"}

### 4.1 Create a Virtual Machine for Windows Server {#6086 .graf .graf--h3 .graf-after--h3 name="6086"}

1.  [**Download and Install VirtualBox or VMware**.]{#b242}
2.  [**Create a new VM**:]{#fb98}

- [Allocate at least 4 GB of RAM and 40 GB of disk space.]{#8a9a}
- [Install **Windows Server** on the VM.]{#6812}

### 4.2 Install and Configure Active Directory Domain Services (AD DS) {#1369 .graf .graf--h3 .graf-after--li name="1369"}

**Promote the server to a Domain Controller**:

- [Go to **Server Manager** \> Add Roles and Features.]{#51f2}
- [Select **Active Directory Domain Services** (AD DS).]{#862f}
- [After installation, promote the server to a domain controller. You'll
  need to create a new forest and domain (e.g.,
  `lab.local`{.markup--code .markup--li-code}).]{#9850}

**Create Users and Groups**:

- [Using **Active Directory Users and Computers**, create users (e.g.,
  JohnDoe, JaneSmith) and groups (e.g., IT, HR) to simulate an
  organization.]{#2f0d}

**Configure Group Policies**:

- [Set up **Group Policy Objects (GPOs)** to simulate password policies,
  access restrictions, and more.]{#3644}
:::
::::
::::::

:::::: {#b6e4 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Installing and Configuring Splunk in a Home Lab {#5104 .graf .graf--h3 .graf--leading name="5104"}

### 5.1 Download and Install Splunk {#ad4a .graf .graf--h3 .graf-after--h3 name="ad4a"}

1.  [Visit **Splunk's official website** and download the free version
    of Splunk.]{#7c8a}
2.  [**Install Splunk** on a new virtual machine with at least 4 GB of
    RAM.]{#ce27}
3.  [During installation, set up an administrator account.]{#1afc}

### 5.2 Configure Splunk to Receive Logs {#8ab4 .graf .graf--h3 .graf-after--li name="8ab4"}

**Install the Universal Forwarder**:

- [On the client machines (e.g., your Windows 10 VM), install the
  **Splunk Universal Forwarder** to send logs to the Splunk
  server.]{#c12f}

**Set up Data Inputs**:

- [In the Splunk web interface, go to **Settings** \> **Data Inputs**
  and configure inputs for **Windows Event Logs** and **Active Directory
  Logs**.]{#98f9}

**Monitor Active Directory Events**:

- [Use **Windows Security Event Logs** to monitor login attempts, user
  creation, password changes, and Group Policy modifications.]{#19f0}
:::
::::
::::::

:::::: {#fd41 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 6. Simulating Security Events in Your Home Lab {#bf6d .graf .graf--h3 .graf--leading name="bf6d"}

To fully utilize your home lab, you'll need to generate activity and
security events that mirror real-world scenarios. Here are a few ways to
do that:

### 6.1 User Activity Simulation {#8b77 .graf .graf--h3 .graf-after--p name="8b77"}

- [**Logins**: Log in and out of the Windows 10 client machine several
  times.]{#43bf}
- [**Password Changes**: Force password changes for users in Active
  Directory.]{#7059}
- [**File Access**: Create, modify, and delete files to generate audit
  logs.]{#05e4}

### 6.2 Attack Simulation {#3cac .graf .graf--h3 .graf-after--li name="3cac"}

- [**Brute Force Attack**: Simulate multiple failed login
  attempts.]{#52bb}
- [**Privilege Escalation**: Use tools like **Mimikatz** (in a safe
  environment) to demonstrate privilege escalation.]{#9f6a}
- [**Suspicious PowerShell Activity**: Run custom scripts to simulate an
  attack using PowerShell.]{#5095}
:::
::::
::::::

:::::: {#4287 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 7. Monitoring and Investigating Logs in Splunk {#7dfc .graf .graf--h3 .graf--leading name="7dfc"}

Once you've generated events in your lab, you can start investigating
using Splunk.

### 7.1 Querying Logs {#7b72 .graf .graf--h3 .graf-after--p name="7b72"}

Splunk uses a powerful **Search Processing Language (SPL)** to query
logs. Here are a few useful commands:

- [**Failed Login Attempts**:]{#c007}
- [`index=windows sourcetype="WinEventLog:Security" EventCode=4625 | stats count by Account_Name, ComputerName`{.markup--code
  .markup--li-code}]{#b6bc}
- [**Password Changes**:]{#7db1}
- [`index=windows sourcetype="WinEventLog:Security" EventCode=4723 | stats count by Account_Name`{.markup--code
  .markup--li-code}]{#9db5}

### 7.2 Visualizing Security Incidents {#1496 .graf .graf--h3 .graf-after--li name="1496"}

You can create **dashboards** in Splunk to visualize key security
metrics, such as failed login attempts, user account lockouts, and
suspicious network traffic. These dashboards help SoC analysts quickly
identify patterns and potential threats.
:::
::::
::::::

:::::: {#8e6d .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 8. Sample Use Cases for Active Directory & Splunk in a SoC Environment {#f208 .graf .graf--h3 .graf--leading name="f208"}

### 8.1 Monitoring Privileged User Activities {#88c2 .graf .graf--h3 .graf-after--h3 name="88c2"}

Monitoring activities of privileged users like system administrators is
critical. Use Splunk to track when admin accounts are used, modified, or
deleted.

### 8.2 Detecting Lateral Movement {#abfa .graf .graf--h3 .graf-after--p name="abfa"}

Attackers often use **lateral movement** to pivot between machines in a
network. By analyzing AD logs in Splunk, you can detect patterns of
lateral movement, such as logins from unexpected locations or machines.

### 8.3 Tracking Brute Force Attacks {#4fe7 .graf .graf--h3 .graf-after--p name="4fe7"}

Brute force attacks are common in attempting to compromise user
accounts. By monitoring failed login attempts and lockouts, you can
proactively detect and prevent such attacks.
:::
::::
::::::

:::::: {#63b2 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 9. Advanced Configuration: Integrating Threat Intelligence with Splunk {#62dd .graf .graf--h3 .graf--leading name="62dd"}

For advanced users, you can integrate **threat intelligence feeds** into
Splunk to correlate internal logs with external threat data. This helps
in detecting known malicious IPs, URLs, or domains attempting to
interact with your environment.

You can use services like **VirusTotal** or **AlienVault OTX** to pull
in threat intelligence feeds, enhancing your lab's detection
capabilities.
:::
::::
::::::

:::::: {#e343 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 10. Conclusion {#753b .graf .graf--h3 .graf--leading name="753b"}

Setting up an Active Directory and Splunk home lab provides aspiring SoC
analysts with a comprehensive environment to build practical skills.
With a home lab, you can simulate real-world security scenarios,
practice detecting and responding to threats, and deepen your
understanding of enterprise security tools.

By mastering these tools and techniques, you'll be well on your way to a
successful career as a SoC analyst. Keep experimenting with your home
lab, stay updated on the latest security trends, and continue learning
to stay ahead in the cybersecurity field.

### Promote and Collaborate on Cybersecurity Insights {#4631 .graf .graf--h3 .graf-after--p name="4631"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#6c5c .graf .graf--h3 .graf-after--p name="6c5c"}

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
:::::::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [October 3, 2024](https://medium.com/p/7e01e0db71e2).

[Canonical
link](https://medium.com/@bevijaygupta/soc-analyst-active-directory-splunk-home-lab-7e01e0db71e2){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
