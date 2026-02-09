---
title: "Termux Cheat Sheet  Linux Power on Mobile 8c6189ac7688"
platform: Medium
original_file: 2024-09-20_Termux-Cheat-Sheet--Linux-Power-on-Mobile-8c6189ac7688.md
---

# Termux Cheat Sheet  Linux Power on Mobile 8c6189ac7688

::: {}
# Termux Cheat Sheet: Linux Power on Mobile {#termux-cheat-sheet-linux-power-on-mobile .p-name}
:::

::: {.section .p-summary field="subtitle"}
Termux is a powerful terminal emulator and Linux environment app for
Android devices that bridges the gap between mobile and desktop...
:::

::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#5f1d .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Termux Cheat Sheet: Linux Power on Mobile {#7829 .graf .graf--h3 .graf--leading .graf--title name="7829"}

<figure id="1969" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*PdgZke5TVWMUx50P.jpg"
class="graf-image" data-image-id="0*PdgZke5TVWMUx50P.jpg"
data-width="640" data-height="360" data-is-featured="true" />
</figure>

Termux is a powerful terminal emulator and Linux environment app for
Android devices that bridges the gap between mobile and desktop
computing. With it, you can run a full-fledged Linux environment, access
a wide variety of tools for programming, ethical hacking, network
testing, and more --- all from your smartphone or tablet. This makes it
a favorite tool for developers, system administrators, and hackers who
want to leverage Linux's power without needing to carry a laptop around.

In this comprehensive guide, we will explore how to use Termux,
essential commands, and a cheat sheet to maximize your productivity on
mobile. We'll cover installation, configuration, package management,
useful tools, and how you can use Termux for programming, ethical
hacking, system administration, and other technical tasks.
:::
::::
::::::

:::::: {#b220 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### What is Termux? {#a09e .graf .graf--h3 .graf--leading name="a09e"}

Termux is a terminal emulator that enables you to run Linux commands on
Android devices. It provides access to a wide range of command-line
utilities and applications, making it feel like you're working on a
Linux desktop. Termux allows users to install and manage packages using
the built-in package manager (`pkg`{.markup--code .markup--p-code}) and
apt, similar to Debian-based Linux systems.

### Why Use Termux? {#9dfa .graf .graf--h3 .graf-after--p name="9dfa"}

Termux offers several benefits:

- [**Portability**: You carry a Linux terminal in your pocket, allowing
  you to manage systems, write code, or run scripts wherever you
  are.]{#ad56}
- [**Customizability**: It gives access to thousands of Linux packages
  for development, ethical hacking, server management, and more.]{#ff92}
- [**No Root Required**: Unlike many other Android terminal apps, Termux
  does not require root access.]{#272d}
- [**Multifunctionality**: It can be used for web development,
  programming in various languages, ethical hacking, and network
  administration.]{#b84b}
:::
::::
::::::

:::::: {#e266 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Getting Started with Termux {#8b69 .graf .graf--h3 .graf--leading name="8b69"}

To get started with Termux, follow these simple steps:

### 1. Installing Termux {#8f27 .graf .graf--h3 .graf-after--p name="8f27"}

Termux can be installed directly from the Google Play Store or from
F-Droid, a trusted repository for free and open-source Android apps.

- [**Google Play Store**: Install from here]{#2524}
- [**F-Droid**: Install from here]{#789c}

Once installed, open Termux and you'll be greeted with a basic terminal
interface.

### 2. Updating and Upgrading Termux {#783d .graf .graf--h3 .graf-after--p name="783d"}

The first thing you should do is update the Termux environment by
running the following commands:

``` {#dc62 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
pkg update
pkg upgrade
```

This updates the list of available packages and upgrades all installed
packages to their latest versions.

### 3. Installing Essential Packages {#29ba .graf .graf--h3 .graf-after--p name="29ba"}

Termux comes with minimal packages pre-installed. To start working
effectively, you'll want to install some basic packages:

- [**Git** (for version control):]{#d184}
- [`pkg install git`{.markup--code .markup--li-code}]{#becd}
- [**Python** (for scripting and programming):]{#9080}
- [`pkg install python`{.markup--code .markup--li-code}]{#aeb0}
- [**Node.js** (for JavaScript development):]{#d5eb}
- [`pkg install nodejs`{.markup--code .markup--li-code}]{#41c2}
- [**Curl** (for transferring data with URLs):]{#3e07}
- [`pkg install curl`{.markup--code .markup--li-code}]{#3a79}
- [**Wget** (for downloading files from the web):]{#ea74}
- [`pkg install wget`{.markup--code .markup--li-code}]{#1b39}
:::
::::
::::::

:::::: {#8e92 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Termux Cheat Sheet: Essential Commands and Shortcuts {#c97a .graf .graf--h3 .graf--leading name="c97a"}

### System Management {#4595 .graf .graf--h3 .graf-after--h3 name="4595"}

Here are some fundamental Termux commands to manage your system:

- [**Update Termux Package Repository**:]{#44c1}
- [`pkg update`{.markup--code .markup--li-code}]{#0de4}
- [**Upgrade Installed Packages**:]{#25b8}
- [`pkg upgrade`{.markup--code .markup--li-code}]{#8821}
- [**Install a Package**:]{#b1fe}
- [`pkg install <package-name>`{.markup--code .markup--li-code}]{#8e29}
- [**Remove a Package**:]{#4dcb}
- [`pkg uninstall <package-name>`{.markup--code
  .markup--li-code}]{#f4ab}
- [**Search for a Package**:]{#3f01}
- [`pkg search <package-name>`{.markup--code .markup--li-code}]{#8e27}
- [**Display Package Information**:]{#2734}
- [`pkg show <package-name>`{.markup--code .markup--li-code}]{#8317}
- [**Check Disk Usage**:]{#9ee2}
- [`df -h`{.markup--code .markup--li-code}]{#028f}
- [**Check System Uptime**:]{#026c}
- [`uptime`{.markup--code .markup--li-code}]{#2564}
- [**List Running Processes**:]{#5475}
- [`ps aux`{.markup--code .markup--li-code}]{#2c09}

### Navigation and File Management {#6712 .graf .graf--h3 .graf-after--li name="6712"}

Navigating and managing files within Termux is similar to using the
Linux command line:

- [**List Files in Current Directory**:]{#b2f6}
- [`ls`{.markup--code .markup--li-code}]{#9b0b}
- [**Change Directory**:]{#d40f}
- [`cd /path/to/directory`{.markup--code .markup--li-code}]{#2d5e}
- [**Create a New Directory**:]{#824d}
- [`mkdir <directory-name>`{.markup--code .markup--li-code}]{#f350}
- [**Delete a File**:]{#1c5b}
- [`rm <file-name>`{.markup--code .markup--li-code}]{#760a}
- [**Move or Rename a File**:]{#4a1b}
- [`mv <source> <destination>`{.markup--code .markup--li-code}]{#1e94}
- [**Copy a File**:]{#d476}
- [`cp <source> <destination>`{.markup--code .markup--li-code}]{#4032}
- [**View the Contents of a File**:]{#13a9}
- [`cat <file-name>`{.markup--code .markup--li-code}]{#76d3}
- [**Search for Files**:]{#ed72}
- [`find / -name <file-name>`{.markup--code .markup--li-code}]{#505a}

### Permissions and Access {#3848 .graf .graf--h3 .graf-after--li name="3848"}

- [**Change File Permissions**:]{#68c0}
- [`chmod <permissions> <file-name>`{.markup--code
  .markup--li-code}]{#68e2}
- [**Check File Permissions**:]{#d380}
- [`ls -l`{.markup--code .markup--li-code}]{#f6d3}
- [**Change File Ownership**:]{#85b9}
- [`chown <user>:<group> <file-name>`{.markup--code
  .markup--li-code}]{#2669}

### Networking Commands {#3f48 .graf .graf--h3 .graf-after--li name="3f48"}

Termux can be used for basic network diagnostics and even advanced
network scanning. Here are some networking commands:

- [**Check Connectivity (Ping a Host)**:]{#23cd}
- [`ping <host>`{.markup--code .markup--li-code}]{#5943}
- [**Display IP Address Configuration**:]{#e73e}
- [`ifconfig`{.markup--code .markup--li-code}]{#2b41}
- [**Download a File with Wget**:]{#0f12}
- [`wget <url>`{.markup--code .markup--li-code}]{#98f7}
- [**Download a File with Curl**:]{#cf06}
- [`curl -O <url>`{.markup--code .markup--li-code}]{#eb1e}
- [**Check Open Ports (Using Nmap)**:]{#c66d}
- [`pkg install nmap nmap <host>`{.markup--code
  .markup--li-code}]{#a3fc}
- [**Check Current Network Connections**:]{#4335}
- [`netstat -tuln`{.markup--code .markup--li-code}]{#1d46}

### Programming and Scripting {#d5ad .graf .graf--h3 .graf-after--li name="d5ad"}

Termux supports a variety of programming languages, making it an ideal
environment for coding on the go.

- [**Running Python Scripts**:]{#ed7b}
- [`python <script.py>`{.markup--code .markup--li-code}]{#f041}
- [**Running Bash Scripts**:]{#340c}
- [`bash <script.sh>`{.markup--code .markup--li-code}]{#288f}
- [**Running Node.js Scripts**:]{#9aba}
- [`node <script.js>`{.markup--code .markup--li-code}]{#d67a}
- [**Installing Python Libraries**:]{#62a3}
- [`pip install <library-name>`{.markup--code .markup--li-code}]{#c7ce}

### Git Version Control {#eee8 .graf .graf--h3 .graf-after--li name="eee8"}

Git is essential for managing code repositories. In Termux, Git
functions just like it does on desktop Linux systems.

- [**Clone a Repository**:]{#533c}
- [`git clone <repository-url>`{.markup--code .markup--li-code}]{#5762}
- [**Check Repository Status**:]{#d218}
- [`git status`{.markup--code .markup--li-code}]{#1907}
- [**Stage Files for Commit**:]{#8ada}
- [`git add <file-name>`{.markup--code .markup--li-code}]{#2e5c}
- [**Commit Changes**:]{#b1c6}
- [`git commit -m "Your commit message"`{.markup--code
  .markup--li-code}]{#3191}
- [**Push Changes to Remote Repository**:]{#1a8d}
- [`git push origin <branch-name>`{.markup--code
  .markup--li-code}]{#8af2}
- [**Pull Latest Changes**:]{#fe9b}
- [`git pull origin <branch-name>`{.markup--code
  .markup--li-code}]{#7ebd}

### Advanced Commands {#6a37 .graf .graf--h3 .graf-after--li name="6a37"}

Here are some advanced Termux commands that can enhance your
productivity.

- [**SSH into a Remote Server**:]{#18c9}
- [`ssh user@host`{.markup--code .markup--li-code}]{#3cbc}
- [**Set Up an SSH Server on Termux**: Install OpenSSH:]{#48c3}
- [`pkg install openssh`{.markup--code .markup--li-code}]{#7714}
- [Start SSH server:]{#659c}
- [`sshd`{.markup--code .markup--li-code}]{#4137}
- [Check your IP address:]{#276e}
- [`ifconfig`{.markup--code .markup--li-code}]{#078b}
- [You can now SSH into your Termux instance from any other
  machine:]{#4460}
- [`ssh user@<Termux-IP>`{.markup--code .markup--li-code}]{#64bf}
- [**Run Python's HTTP Server**: Serve the current directory over
  HTTP:]{#aee9}
- [`python -m http.server`{.markup--code .markup--li-code}]{#466a}
- [**Compile C Code**: Install `gcc`{.markup--code
  .markup--li-code}:]{#441b}
- [`pkg install clang`{.markup--code .markup--li-code}]{#7866}
- [Compile and run:]{#8068}
- [`clang <file.c> -o <output> ./<output>`{.markup--code
  .markup--li-code}]{#62a8}

### Running Linux Services on Termux {#b2be .graf .graf--h3 .graf-after--li name="b2be"}

Termux can run services like SSH, Apache, and even MySQL. You can host
websites or manage databases directly from your mobile device.

- [**Install Apache HTTP Server**:]{#9e1a}
- [`pkg install apache2`{.markup--code .markup--li-code}]{#1e4c}
- [Start Apache server:]{#b5b8}
- [`apachectl start`{.markup--code .markup--li-code}]{#485a}
- [**Install MySQL Server**:]{#056c}
- [`pkg install mariadb`{.markup--code .markup--li-code}]{#9169}
- [Start MySQL server:]{#7b3a}
- [`mysqld_safe --skip-grant-tables &`{.markup--code
  .markup--li-code}]{#925a}
- [**Install PHP**]{#4110}
- [`pkg install php`{.markup--code .markup--li-code}]{#cde1}
- [Run PHP code:]{#6e7a}
- [`php <script.php>`{.markup--code .markup--li-code}]{#39eb}
:::
::::
::::::

:::::: {#7811 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Using Termux for Ethical Hacking {#6306 .graf .graf--h3 .graf--leading name="6306"}

Termux has become a go-to tool for many ethical hackers because it
provides access to many security tools. With Termux, you can run
penetration testing tools, scan networks, and exploit
vulnerabilities --- all from your Android device.

### 1. Nmap {#8663 .graf .graf--h3 .graf-after--p name="8663"}

Nmap is a popular network scanning tool used to discover devices on a
network and identify open ports.

Install Nmap:

``` {#ed39 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
pkg install nmap
```

Scan a network:

``` {#0ef9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="go"}
nmap -sP <network-range>
```

Scan for open ports:

``` {#199e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
nmap -p <port-range> <target-ip>
```

### 2. Metasploit {#2852 .graf .graf--h3 .graf-after--pre name="2852"}

Metasploit is a powerful framework used for developing and executing
exploit code against a remote target machine.

Install Metasploit:

``` {#a377 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
pkg install unstable-repo
pkg install metasploit
```

Start Metasploit:

``` {#b792 .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
msfconsole
```
:::
::::
::::::

:::::: {#dfe5 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Conclusion {#f73f .graf .graf--h3 .graf--leading name="f73f"}

Termux is a versatile tool that brings the power of Linux to your mobile
device. Whether you're a developer, system administrator, or ethical
hacker, Termux provides a robust platform for mobile productivity. From
basic system management to running advanced Linux services, Termux opens
up endless possibilities on Android. This cheat sheet is a starting
point to unlock the potential of Termux and use it effectively for
various tasks.

With the right knowledge and tools, Termux turns your mobile device into
a portable Linux workstation, offering flexibility and power wherever
you go.

### Promote and Collaborate on Cybersecurity Insights {#6e17 .graf .graf--h3 .graf-after--p name="6e17"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#96bc .graf .graf--h3 .graf-after--p name="96bc"}

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
:::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 20, 2024](https://medium.com/p/8c6189ac7688).

[Canonical
link](https://medium.com/@bevijaygupta/termux-cheat-sheet-linux-power-on-mobile-8c6189ac7688){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
