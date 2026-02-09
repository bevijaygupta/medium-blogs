---
title: "TryHackMe RustScan Challenge  A Complete Guide b80a167a1115"
platform: Medium
original_file: 2024-08-22_TryHackMe-RustScan-Challenge--A-Complete-Guide-b80a167a1115.md
---

# TryHackMe RustScan Challenge  A Complete Guide b80a167a1115

::: {}
# TryHackMe RustScan Challenge: A Complete Guide {#tryhackme-rustscan-challenge-a-complete-guide .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "RustScan"
:::

::::::: {.section .e-content field="body"}
:::::: {#175d .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### TryHackMe RustScan Challenge: A Complete Guide {#db21 .graf .graf--h3 .graf--leading .graf--title name="db21"}

**This is a Writeup of Tryhackme room "RustScan"**

<figure id="602b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LqhIPvcBe0Ay35_d.png"
class="graf-image" data-image-id="0*LqhIPvcBe0Ay35_d.png"
data-width="510" data-height="275" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/rustscan](https://tryhackme.com/room/rustscan){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/rustscan"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

RustScan is the modern day port scanner.

Capable of scanning targets in less than a second, extensible scripting
language allowing you to write scripts in Python, and more.

This room will teach you all there is need to know about RustScan.

You can find RustScan's GitHub repository here.

[https://github.com/RustScan/RustScan](https://github.com/RustScan/RustScan){.markup--anchor
.markup--p-anchor data-href="https://github.com/RustScan/RustScan"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 2: Installing RustScan {#92fd .graf .graf--h3 .graf-after--p name="92fd"}

The installation procedure of RustScan is very easy.

**Note:** If you use Mac OS, Arch, Docker, Nix OS or any other operating
system than Debian more install instructions can be found on the
repository.

[https://github.com/RustScan/RustScan/wiki/Installation-Guide](https://github.com/RustScan/RustScan/wiki/Installation-Guide){.markup--anchor
.markup--p-anchor
data-href="https://github.com/RustScan/RustScan/wiki/Installation-Guide"
rel="noopener ugc nofollow noopener" target="_blank"}

Go to [RustScan
Repo](https://github.com/RustScan/RustScan/releases){.markup--anchor
.markup--p-anchor
data-href="https://github.com/RustScan/RustScan/releases"
rel="noopener ugc nofollow noopener" target="_blank"}.

Download the **.deb file** for Kali
Linux.[(rustscan_1.8.0_amd64.deb**)**](https://github.com/RustScan/RustScan/releases/download/1.8.0/rustscan_1.8.0_amd64.deb){.markup--anchor
.markup--p-anchor
data-href="https://github.com/RustScan/RustScan/releases/download/1.8.0/rustscan_1.8.0_amd64.deb"
rel="noopener ugc nofollow noopener" target="_blank"}

In terminal type:- **dpkg -i \<file name\>**

Try running **rustscan** in terminal.

### Task 3: Accessible {#96f5 .graf .graf--h3 .graf-after--p name="96f5"}

RustScan is actively accessible. That means we:

- [Use continuous integration testing to ensure accessibility needs are
  met]{#08dd}
- [Manually test accessibility]{#e946}

This is important because accessibility is important in hacking.

Hacking isn't just inaccessible, it is the opposite --- it is actively
discluding members from the community because of some issues they were
born or developed that they cannot help.

It is a basic human right to extend everything we do to be accessible to
everyone. In the same way, it is right for you to get healthcare, to get
an education.

Around 15% of all people suffer from some sort of disability. See this
blog post for [more
info](https://bradfrost.com/blog/post/why-i-care-about-accessibility/){.markup--anchor
.markup--p-anchor
data-href="https://bradfrost.com/blog/post/why-i-care-about-accessibility/"
rel="noopener ugc nofollow noopener" target="_blank"} on why
accessibility is important or the [world report on disability for
statistics.](https://en.wikipedia.org/wiki/World_report_on_disability){.markup--anchor
.markup--p-anchor
data-href="https://en.wikipedia.org/wiki/World_report_on_disability"
rel="noopener ugc nofollow noopener" target="_blank"}

For more information about accessibility in infosec, [I wrote this blog
post](https://bees.substack.com/p/making-hacking-accessible){.markup--anchor
.markup--p-anchor
data-href="https://bees.substack.com/p/making-hacking-accessible"
rel="noopener ugc nofollow noopener" target="_blank"}.

Click "completed" if you agree A11Y in infosec is important

### Task 4: Fast {#4ec5 .graf .graf--h3 .graf-after--p name="4ec5"}

RustScan is fast. But, why? In short:

- [Low-level kernel networking]{#911e}
- [Written in a fast language (Rust)]{#70d2}
- [Asynchronous scanning. Multi-threading is slow due to the context
  switching cost. Async is fast. [See my Rust room for more information
  on this](https://tryhackme.com/room/rust){.markup--anchor
  .markup--li-anchor data-href="https://tryhackme.com/room/rust"
  rel="noopener ugc nofollow noopener" target="_blank"}.]{#a7d8}

At its fastest settings, the bottleneck is not the program. The
bottleneck is your computer, the network link between your computer and
the target, and finally the target itself.

If your OS/hardware isn't the best, that'll be the bottleneck.

This sounds bad, but some other port scanners have their bottlenecks in
the program itself. RustScan is as fast as your system, the network, and
the target is.

Being so fast is bad, but RustScan can be slowed down to however slow
you want. But just know, if speed is your thing --- RustScan is where
it's at.

**How do you ensure speed?**

As more features are added into RustScan, slowness tends to creep in
unless noticed.

As we add more features, the program generally tends to slow down. This
is a rule for all programs. More complexity will often mean it is slower
(but not always).

RustScan deals with this by:

- [Manual testing on targets]{#fe33}
- [Continuous integration that fails if the program is too slow]{#7121}
- [Benchmarking the program and graphing the results]{#0048}
- [Keeping all features outside of the scanning itself. Unless it is
  absolutely needed, RustScan will not run code before or during the
  scan --- only after.]{#48c3}

### Task 5: Extensible {#db23 .graf .graf--h3 .graf-after--li name="db23"}

Now for the largest feature of RustScan. Thanks to Bergabman for working
on this one.

RustScan is extensible by the RustScan Scripting Engine. This allows you
to write a script which runs after the scan has completed, taking inputs
of open ports and their respective IPs.

RSE supports these languages:

- [Python]{#7a2b}
- [Shell]{#a85f}
- [Perl]{#ba2d}
- [Any program which is a binary and in \$PATH]{#ace5}

**Scripting Engine Arguments**

RustScan's scripting engine can be altered using the " --- scripts"
argument.

There are 3 possible arguments:

- [None (don't run any scripts)]{#1d8e}
- [Custom (run all scripts in the scripts folder)]{#b800}
- [Default (runs Nmap script, or whatever script is in the config file.
  Default does not need to be enabled, it is on by default.)]{#8a70}

**Python Custom Scripts**

To execute a custom script, we need a
`rustscan_scripts.toml`{.markup--code .markup--p-code} file located at
`$HOME/.rustscan_scripts.toml`{.markup--code .markup--p-code}.

The script file should look like:

``` {#e660 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
# Test/Example ScriptConfig file# Tags to filter on scripts. Only scripts containing all these tags will run.
tags = ["core_approved", "example"]# If it's present then only those scripts will run which has a tag ports = "80". Not yet implemented.
#
# ex.:
# ports = ["80"]
# ports = ["80","81","8080"]
ports = ["80"]# Only this developer(s) scripts to run. Not yet implemented.
developer = ["example"]
```

Let's walk through this.

Firstly, for reference, this is a basic Python script.

``` {#b0d8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="shell"}
#!/usr/bin/python3
#tags = ["core_approved", "example",]
#developer = [ "example", "https://example.org" ]
#trigger_port = "80"
#call_format = "python3 {{script}} {{ip}} {{port}}"# Scriptfile parser stops at the first blank line with parsing.
# This script will run itself as an argument with the system installed python interpreter, only scanning port 80.
# Unused filed: ports_separator = ","import sysprint('Python script ran with arguments', str(sys.argv))
```

Note: the metadata of scripts is stored as comments. The first line is
always a
[shebang](https://en.wikipedia.org/wiki/Shebang_%28Unix%29){.markup--anchor
.markup--p-anchor
data-href="https://en.wikipedia.org/wiki/Shebang_(Unix)"
rel="noopener ugc nofollow noopener" target="_blank"}.

### Tags {#3730 .graf .graf--h3 .graf-after--p name="3730"}

Tags are categories of scripts. For example, we may have these
categories:

- [HTTP]{#c4f6}
- [SSH]{#6ab2}
- [Tomcat]{#1dce}

And only wish to run scripts that match these categories. Our config
file will only execute the scripts with matching categories.

### Developer {#12e6 .graf .graf--h3 .graf-after--p name="12e6"}

This tag issues who the developer of the script is.

### Trigger Point {#e505 .graf .graf--h3 .graf-after--p name="e505"}

This tag states at what port should the script trigger? For HTTP it
would be "80". For HTTP and HTTPS it would be "80, 443"

### Call Format {#07c4 .graf .graf--h3 .graf-after--p name="07c4"}

RustScan uses a templating library called
[text_placeholder](https://crates.io/crates/text_placeholder){.markup--anchor
.markup--p-anchor data-href="https://crates.io/crates/text_placeholder"
rel="noopener ugc nofollow noopener" target="_blank"}.

This allows us to enclose variables in `{{variable}}`{.markup--code
.markup--p-code} doubly curly braces. RustScan supports 3 variables:

- [The script name]{#b747}
- [The IP address]{#28ef}
- [The port(s)]{#23b9}

``` {#8e36 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="shell"}
#call_format = "python3 {{script}} {{ip}} {{port}}"
```

### The Code itself {#e788 .graf .graf--h3 .graf-after--pre name="e788"}

Now everything after this metadata is the code itself.

The script will receive arguments via `sys.argv`{.markup--code
.markup--p-code} in the format specified in the
`call_format`{.markup--code .markup--p-code} variable.

Now with this data, we run the script, doing whatever we please!

### Contributing / Making Scripts {#6f66 .graf .graf--h3 .graf-after--p name="6f66"}

We have a folder of example scripts
[here](https://github.com/RustScan/RustScan/tree/master/fixtures/.rustscan_scripts){.markup--anchor
.markup--p-anchor
data-href="https://github.com/RustScan/RustScan/tree/master/fixtures/.rustscan_scripts"
rel="noopener ugc nofollow noopener" target="_blank"}.

If you make a script, please consider contributing to RustScan. Right
now you can submit a pull request to [this
folder](https://github.com/RustScan/RustScan/tree/master/fixtures/.rustscan_scripts){.markup--anchor
.markup--p-anchor
data-href="https://github.com/RustScan/RustScan/tree/master/fixtures/.rustscan_scripts"
rel="noopener ugc nofollow noopener" target="_blank"} and we'll include
your script.

### Running Other Tools with RustScan {#cfd5 .graf .graf--h3 .graf-after--p name="cfd5"}

Any tool installed in the system (like Nmap, GoBuster, etc) can be run
with RustScan.

We do this by default with Nmap.

To execute another program, create a shell script which calls that
program. So to call Nmap, create a shell script with our RustScan
Scripting Engine and then for the function:

``` {#95cd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
nmap -vvv -p {{port}} {{ip}}
```

You can replace this with GoBuster or any program at all. So long as the
program is installed and reachable in the environment \$PATH.

**Q.1:** What is the scripting file config called?

> ***Answer: rustscan_scripts.toml***

**Q.2:** Can you run other binaries with RustScan? (T)rue / (F)alse.

> ***Answer: T***

**Q.3:** Does RutScan support scripts in Javascript? (T)rue / (F)alse.

> ***Answer: F***

### Task 6: Adaptive {#7f0b .graf .graf--h3 .graf-after--blockquote name="7f0b"}

RustScan is **adaptive**. That means it changes how it works to better
suit its environment. We call this the "adaptive learning" feature set.

Some of these features included (or are being worked on) are:

- [Adaptive Outbound SYN timing to optimize the speed of
  scanning]{#7fa0}

While RustScan scans the target, it learns how it reacts, How fast is it
to scan? Does it respond quickly? How far away?

By using this data RustScan moulds itself so it is the fastest scanner
for any target.

- [Custom Top Ports]{#dcb3}

You may be familiar with the top ports feature of other scanners. It'll
let you scan the top 1000 ports on the internet.

But, the top 1000 ports on the internet are not often the top 1000 ports
you might come across. Corporate networks may have unusual ports open,
capture the flag events may have unusual ports. As an example, port
31137 is used a lot in CTFs because "l33t".

This port is not in any top 1000 ports list.

RustScan learns what the most commonly open ports are **for you** and
adapts itself.

- [Operating System Adaption]{#476d}

Your computer is not the same as my computer. So why run the same scan
settings? Mac OS devices have an open file limit of around 250. That
means they can only make 250 connections at any given time.

Kali Linux has around 90,000 open files.

If we built this for Kali Linux, it would break on a Mac which does not
support that many open files.

RustScan learns about your operating system and adapts itself to better
suit you and your computer, as well as the networks it is scanning.

- [Configuration File]{#550d}

All of this information is stored in a configuration file. Onboarding a
new pentesting intern? Send them your config file and their RustScan
will be optimal from day 1.

### Task 7: Scanning Time! {#66c1 .graf .graf--h3 .graf-after--p name="66c1"}

The tool is really amazing in terms of scanning. It can scan all the
ports really fast and then pipe the output to the Nmap. Now in this
room, we'll scan our vulnerable machine.\
Basic format for RustScan is **rustscan -r ports -a
\<Target-ip\> --- \<nmap cmds\>**

Here's a full list of things you can do.

### Multiple IP Scanning {#1af8 .graf .graf--h3 .graf-after--p name="1af8"}

You can scan multiple IPs using a comma-separated list like so:

``` {#6c20 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
rustscan -a 127.0.0.1,0.0.0.0
```

### Host Scanning {#7159 .graf .graf--h3 .graf-after--pre name="7159"}

RustScan can also scan hosts, like so:

``` {#ef04 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
➜ rustscan -a www.google.com, 127.0.0.1
Open 216.58.210.36:1
Open 216.58.210.36:80
Open 216.58.210.36:443
Open 127.0.0.1:53
Open 127.0.0.1:631
```

### CIDR support {#a3d9 .graf .graf--h3 .graf-after--pre name="a3d9"}

RustScan supports CIDR:

``` {#9dc2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
➜ rustscan -a 192.168.0.0/30
```

### Hosts file as input {#f731 .graf .graf--h3 .graf-after--pre name="f731"}

The file is a new line separated list of IPs / Hosts to scan:

hosts.txt

``` {#20af .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
192.168.0.1
192.168.0.2
google.com
192.168.0.0/30
127.0.0.1
```

The argument is:

``` {#5244 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
rustscan -a 'hosts.txt'
```

### Individual Port Scanning {#0194 .graf .graf--h3 .graf-after--pre name="0194"}

RustScan can scan individual ports, like so:

``` {#0740 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
➜ rustscan -a 127.0.0.1 -p 53
53
```

### Multiple selected port scanning {#8d98 .graf .graf--h3 .graf-after--pre name="8d98"}

You can input a comma-separated list of ports to scan:

``` {#5821 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
➜ rustscan -a 127.0.0.1 -p 53,80,121,65535
53
```

### Ranges of ports {#b4f8 .graf .graf--h3 .graf-after--pre name="b4f8"}

To scan a range of ports:

To run:

``` {#b4d4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
➜ rustscan -a 127.0.0.1 --range 1-1000    
53,631
```

### Adjusting the Nmap arguments {#0b6b .graf .graf--h3 .graf-after--pre name="0b6b"}

RustScan, at the moment, runs Nmap by default.

You can adjust the arguments like so:

``` {#c0d5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
rustscan -a 127.0.0.1 -- -A -sC
```

To run:

``` {#9176 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
nmap -Pn -vvv -p $PORTS -A -sC 127.0.0.1
```

### Random Port Ordering {#1017 .graf .graf--h3 .graf-after--pre name="1017"}

If you want to scan ports in a random order (which will help with not
setting off firewalls) run RustScan like this:

``` {#552b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
➜ rustscan -a 127.0.0.1 --range 1-1000 --scan-order "Random"
53,631
```

**Q.1:** After scanning this, how many ports do we find open under 1000?

<figure id="4608" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bJxGb9GcMp9v-bMu.png"
class="graf-image" data-image-id="0*bJxGb9GcMp9v-bMu.png"
data-width="677" data-height="452" />
</figure>

> ***Answer: 2***

**Q.2:** Perform a service version detection scan, what is the version
of the software running on port 22?

<figure id="6a03" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CYRXJobI2IaJNbvn.png"
class="graf-image" data-image-id="0*CYRXJobI2IaJNbvn.png"
data-width="604" data-height="138" />
</figure>

<figure id="3e64" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*NvA4Nsjx0BTqSbEQ.png"
class="graf-image" data-image-id="0*NvA4Nsjx0BTqSbEQ.png"
data-width="723" data-height="91" />
</figure>

Answer: 6.6.1p1

**Q.3:** Perform an aggressive scan, what flag isn't set under the
results for port 80?

<figure id="3a5e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*k_N2kv00KCg6NuRm.png"
class="graf-image" data-image-id="0*k_N2kv00KCg6NuRm.png"
data-width="591" data-height="150" />
</figure>

<figure id="859f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*lLnxREciMVx4Euh3.png"
class="graf-image" data-image-id="0*lLnxREciMVx4Euh3.png"
data-width="657" data-height="220" />
</figure>

> ***Answer: httponly***

### Task 8: RustScan Quiz {#b5e1 .graf .graf--h3 .graf-after--blockquote name="b5e1"}

A short quiz on the more useful switches that we can use with RustScan.
All you'll need for this is the help menu for RustScan. Include all
parts of the switch unless otherwise specified, this includes
`-`{.markup--code .markup--p-code}. For example, we would specify the
`-z`{.markup--code .markup--p-code} switch via
`rustscan -z`{.markup--code .markup--p-code}

**Q.1:** First, how do you access the help menu?

> ***Answer: -h***

**Q.2:** Often referred to as "quiet" mode, What switch can do this?

> ***Answer: -q***

**Q.3:** Which switch can help us to scan for a particular Range?

> ***Answer: -r***

**Q.4:** What switch would you use to find out RustScan's version?

> ***Answer: -v***

**Q.5:** Which switch will help us to select batch size?

> ***Answer: -b***

**Q.6:** Which switch can set timeout?

> ***Answer: -t***

### Promote and Collaborate on Cybersecurity Insights {#4505 .graf .graf--h3 .graf-after--blockquote name="4505"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#0943 .graf .graf--h3 .graf-after--p name="0943"}

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
.h-card} on [August 22, 2024](https://medium.com/p/b80a167a1115).

[Canonical
link](https://medium.com/@bevijaygupta/tryhackme-rustscan-challenge-a-complete-guide-b80a167a1115){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
