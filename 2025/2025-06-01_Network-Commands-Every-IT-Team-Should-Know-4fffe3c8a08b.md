---
title: "Network Commands Every IT Team Should Know 4fffe3c8a08b"
platform: Medium
original_file: 2025-06-01_Network-Commands-Every-IT-Team-Should-Know-4fffe3c8a08b.md
---

# Network Commands Every IT Team Should Know 4fffe3c8a08b

::: {}
# Network Commands Every IT Team Should Know {#network-commands-every-it-team-should-know .p-name}
:::

::: {.section .p-summary field="subtitle"}
In the ever-evolving world of IT and networking, one thing remains
constant --- the importance of mastering network commands. Whether
you're...
:::

::::::: {.section .e-content field="body"}
:::::: {#8613 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Network Commands Every IT Team Should Know {#d48f .graf .graf--h3 .graf--leading .graf--title name="d48f"}

<figure id="e6dc" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*TuxiAG0PaInpmQzg.jpg"
class="graf-image" data-image-id="0*TuxiAG0PaInpmQzg.jpg"
data-width="900" data-height="500" data-is-featured="true" />
</figure>

In the ever-evolving world of IT and networking, one thing remains
constant --- the **importance of mastering network commands**. Whether
you're troubleshooting slow connections, diagnosing DNS issues, or
ensuring uptime across multiple machines, command-line tools are often
your first and most reliable line of defense.

While modern GUI tools and network monitoring dashboards are incredibly
powerful, **the command line still holds unmatched speed, flexibility,
and depth** --- and it's accessible on every machine. In this post,
we'll walk through **network commands that every IT professional should
have at their fingertips**.

Think of this as your cheat sheet, mentor, and toolbox --- all rolled
into one.

### 1. `ping`{.markup--code .markup--h3-code} --- The First Responder of the Network World {#39a7 .graf .graf--h3 .graf-after--p name="39a7"}

If there's one tool every IT person knows, it's `ping`{.markup--code
.markup--p-code}. Think of it as your \"are you there?\" command for the
network.

### Usage: {#83ff .graf .graf--h3 .graf-after--p name="83ff"}

``` {#bef6 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ping google.com
```

### What It Does: {#f234 .graf .graf--h3 .graf-after--pre name="f234"}

- [Sends ICMP Echo Requests to a host to check availability.]{#58c1}
- [Measures response time and packet loss.]{#866c}

### When to Use: {#ed15 .graf .graf--h3 .graf-after--li name="ed15"}

- [Checking internet connectivity.]{#da72}
- [Verifying if a host is online.]{#cccc}
- [Testing latency.]{#c3b2}

### Example: {#1d21 .graf .graf--h3 .graf-after--li name="1d21"}

``` {#2fa7 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ping 192.168.1.1
```

If you see responses, your local router is online. If you don't --- time
to investigate further.

### 2. `tracert`{.markup--code .markup--h3-code} (Windows) / `traceroute`{.markup--code .markup--h3-code} (Linux/macOS) --- Mapping the Journey {#ddce .graf .graf--h3 .graf-after--p name="ddce"}

You know the server is slow --- but where's the slowdown happening?

### Usage: {#3e0f .graf .graf--h3 .graf-after--p name="3e0f"}

``` {#1efd .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
tracert google.com       # Windows  
traceroute google.com    # Linux/macOS
```

### What It Does: {#7458 .graf .graf--h3 .graf-after--pre name="7458"}

- [Shows the path packets take to a destination.]{#ec7e}
- [Identifies bottlenecks or outages in the route.]{#3ba2}

### Why It's Powerful: {#b65c .graf .graf--h3 .graf-after--li name="b65c"}

When a website is down or loading slowly, `traceroute`{.markup--code
.markup--p-code} reveals if the issue is in your local network, your
ISP, or somewhere along the internet backbone.

### 3. `ipconfig`{.markup--code .markup--h3-code} (Windows) / `ifconfig`{.markup--code .markup--h3-code} (Linux/macOS) --- Know Thy IP {#46de .graf .graf--h3 .graf-after--p name="46de"}

Your devices' IP addresses are the foundation of any network.

### Usage: {#6c39 .graf .graf--h3 .graf-after--p name="6c39"}

``` {#dff2 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
ipconfig                 # Windows  
ifconfig                 # Linux/macOS
```

### What It Shows: {#1665 .graf .graf--h3 .graf-after--pre name="1665"}

- [IP addresses]{#ac38}
- [Subnet masks]{#2b7e}
- [Default gateways]{#d0bb}
- [MAC addresses]{#60be}

### Real-World Scenario: {#093f .graf .graf--h3 .graf-after--li name="093f"}

Your user can't connect to the internet. You run
`ipconfig`{.markup--code .markup--p-code} and realize there's no IP
assigned --- their DHCP lease might have expired.

> *Note: On modern Linux systems,* *`ip a`{.markup--code
> .markup--blockquote-code}* *(from* *`iproute2`{.markup--code
> .markup--blockquote-code}) is often used instead of*
> *`ifconfig`{.markup--code .markup--blockquote-code}.*

### 4. `nslookup`{.markup--code .markup--h3-code} --- Investigate DNS Like a Detective {#e014 .graf .graf--h3 .graf-after--blockquote name="e014"}

Sometimes, the internet is "working" --- but not really. That's usually
a DNS issue.

### Usage: {#611c .graf .graf--h3 .graf-after--p name="611c"}

``` {#4658 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nslookup google.com
```

### What It Does: {#a73b .graf .graf--h3 .graf-after--pre name="a73b"}

- [Queries DNS to resolve domain names to IP addresses.]{#67ea}
- [Tests if your DNS server is working properly.]{#06e1}

### Advanced Tip: {#18b1 .graf .graf--h3 .graf-after--li name="18b1"}

You can specify a different DNS server:

``` {#213a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nslookup google.com 8.8.8.8
```

Useful for checking if DNS propagation is complete or whether your DNS
provider is misbehaving.

### 5. `netstat`{.markup--code .markup--h3-code} --- See Who's Talking to Whom {#e2a6 .graf .graf--h3 .graf-after--p name="e2a6"}

A classic tool for viewing active connections and open ports.

### Usage: {#29a9 .graf .graf--h3 .graf-after--p name="29a9"}

``` {#e149 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
netstat -an
```

### What It Does: {#aa98 .graf .graf--h3 .graf-after--pre name="aa98"}

- [Lists all TCP/UDP connections.]{#fd26}
- [Shows ports your system is listening on.]{#65aa}
- [Displays foreign IPs connected to your machine.]{#1012}

### Security Use Case: {#269d .graf .graf--h3 .graf-after--li name="269d"}

You suspect malware is running on a machine. Run `netstat`{.markup--code
.markup--p-code} to check for suspicious external IPs.

### 6. `arp`{.markup--code .markup--h3-code} --- Who's Who in the Local Network {#1cf3 .graf .graf--h3 .graf-after--p name="1cf3"}

The Address Resolution Protocol maps IP addresses to MAC addresses.

### Usage: {#4e65 .graf .graf--h3 .graf-after--p name="4e65"}

``` {#d822 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
arp -a
```

### What It Shows: {#f3f8 .graf .graf--h3 .graf-after--pre name="f3f8"}

- [A list of IP-to-MAC address mappings.]{#768e}
- [Useful for identifying devices on your local network.]{#aa8b}

### Pro Tip: {#2877 .graf .graf--h3 .graf-after--li name="2877"}

Helps detect **ARP spoofing** attempts. If two IPs have the same MAC
address, you've got trouble.

### 7. `ip`{.markup--code .markup--h3-code} --- The Modern Linux Networking Power Tool {#31de .graf .graf--h3 .graf-after--p name="31de"}

On modern Linux distros, `ip`{.markup--code .markup--p-code} has
replaced older commands like `ifconfig`{.markup--code .markup--p-code},
`route`{.markup--code .markup--p-code}, and `arp`{.markup--code
.markup--p-code}.

### Usage: {#f6e4 .graf .graf--h3 .graf-after--p name="f6e4"}

``` {#8d3d .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
ip a               # Show IP addresses  
ip r               # Show routing table  
ip link show       # Show interfaces
```

### Why It Matters: {#1f12 .graf .graf--h3 .graf-after--pre name="1f12"}

More powerful and scriptable than legacy tools. Every Linux-based server
admin should be fluent in it.

### 8. `dig`{.markup--code .markup--h3-code} --- DNS's Swiss Army Knife {#3c98 .graf .graf--h3 .graf-after--p name="3c98"}

More advanced than `nslookup`{.markup--code .markup--p-code},
`dig`{.markup--code .markup--p-code} is often used by IT pros and system
admins.

### Usage: {#ec26 .graf .graf--h3 .graf-after--p name="ec26"}

``` {#966a .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
dig google.com
```

### Features: {#60aa .graf .graf--h3 .graf-after--pre name="60aa"}

- [Query specific record types (A, MX, TXT, etc.)]{#58b9}
- [Test specific DNS servers]{#c8c0}
- [Measure response time]{#c5e9}

### Bonus: {#3bd2 .graf .graf--h3 .graf-after--li name="3bd2"}

To check DNS propagation:

``` {#30b5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
dig @8.8.8.8 yourdomain.com
```

### 9. `telnet`{.markup--code .markup--h3-code} / `nc`{.markup--code .markup--h3-code} (netcat) --- Test Port Connectivity {#a566 .graf .graf--h3 .graf-after--pre name="a566"}

Want to know if a specific port is open on a remote server?

### Usage: {#8c4c .graf .graf--h3 .graf-after--p name="8c4c"}

``` {#9284 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
telnet yourdomain.com 80         # Basic
nc -zv yourdomain.com 80         # More advanced, netcat
```

### Use Cases: {#810f .graf .graf--h3 .graf-after--pre name="810f"}

- [Test if mail ports (25, 587) are reachable.]{#4fe9}
- [Check if a firewall is blocking a port.]{#1fcf}

**Note:** `telnet`{.markup--code .markup--p-code} is deprecated on many
systems. Use `nc`{.markup--code .markup--p-code} instead.

### 10. `route`{.markup--code .markup--h3-code} --- See Where the Packets Go {#fea1 .graf .graf--h3 .graf-after--p name="fea1"}

Helps you understand and manipulate the routing table.

### Usage: {#7a84 .graf .graf--h3 .graf-after--p name="7a84"}

``` {#3c7c .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
route print        # Windows  
route -n           # Linux
```

### When to Use: {#188c .graf .graf--h3 .graf-after--pre name="188c"}

- [Diagnosing routing issues.]{#91ee}
- [Configuring a static route.]{#cb09}

### 11. `hostname`{.markup--code .markup--h3-code} --- Who Am I? {#c9c0 .graf .graf--h3 .graf-after--li name="c9c0"}

Simple but essential.

### Usage: {#0e33 .graf .graf--h3 .graf-after--p name="0e33"}

``` {#b2ee .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
hostname
```

### Use Case: {#96c9 .graf .graf--h3 .graf-after--pre name="96c9"}

Running multiple terminals or remote sessions? It's a quick sanity check
for which machine you're on.

### 12. `whois`{.markup--code .markup--h3-code} --- Domain Ownership Intel {#60c9 .graf .graf--h3 .graf-after--p name="60c9"}

Not just for network admins --- even marketing teams ask, "Who owns this
domain?"

### Usage: {#9718 .graf .graf--h3 .graf-after--p name="9718"}

``` {#6e6e .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
whois example.com
```

### What You Learn: {#7cbf .graf .graf--h3 .graf-after--pre name="7cbf"}

- [Domain registrant]{#9125}
- [Name servers]{#0108}
- [Registration/expiry dates]{#7e6b}

### 13. `nmap`{.markup--code .markup--h3-code} --- The Network Mapper {#3216 .graf .graf--h3 .graf-after--li name="3216"}

If you're in security, networking, or systems administration,
`nmap`{.markup--code .markup--p-code} is your X-ray vision.

### Usage: {#868c .graf .graf--h3 .graf-after--p name="868c"}

``` {#8a2d .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nmap 192.168.1.1
```

### Capabilities: {#9b34 .graf .graf--h3 .graf-after--pre name="9b34"}

- [Scan open ports]{#8f15}
- [Identify OS and services]{#7647}
- [Discover hosts on a subnet]{#bd1a}

### Caution: {#f4ed .graf .graf--h3 .graf-after--li name="f4ed"}

Can trigger intrusion detection systems. Use responsibly on authorized
networks.

### 14. `netsh`{.markup--code .markup--h3-code} (Windows Only) --- Deep Windows Networking Configuration {#8629 .graf .graf--h3 .graf-after--p name="8629"}

Think of `netsh`{.markup--code .markup--p-code} as the registry editor
for your network settings.

### Usage: {#09fe .graf .graf--h3 .graf-after--p name="09fe"}

``` {#d011 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
netsh wlan show profiles
netsh interface ip show config
```

### Why It's Useful: {#5b6c .graf .graf--h3 .graf-after--pre name="5b6c"}

- [Configure IPs]{#9cc3}
- [Reset TCP/IP stack]{#a686}
- [Manage firewall rules]{#042e}

### Example: {#c5d8 .graf .graf--h3 .graf-after--li name="c5d8"}

To reset your network stack:

``` {#f055 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
netsh int ip reset
```

### 15. `scp`{.markup--code .markup--h3-code} & `rsync`{.markup--code .markup--h3-code} --- Secure File Transfers over SSH {#8a5c .graf .graf--h3 .graf-after--pre name="8a5c"}

Not exactly diagnostic, but vital for IT teams.

### Usage: {#978e .graf .graf--h3 .graf-after--p name="978e"}

``` {#5f66 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
scp file.txt user@192.168.1.10:/home/user/
```

### `rsync`{.markup--code .markup--h3-code} for Speed: {#8404 .graf .graf--h3 .graf-after--pre name="8404"}

``` {#de26 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
rsync -avz file.txt user@host:/path/
```

`rsync`{.markup--code .markup--p-code} only sends differences --- faster
and more efficient.

### 16. `tcpdump`{.markup--code .markup--h3-code} & `Wireshark`{.markup--code .markup--h3-code} --- Dive Deep into the Packets {#afdd .graf .graf--h3 .graf-after--p name="afdd"}

For deep packet analysis.

### `tcpdump`{.markup--code .markup--h3-code} (CLI): {#1bc7 .graf .graf--h3 .graf-after--p name="1bc7"}

``` {#ce5c .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
tcpdump -i eth0 port 80
```

### Wireshark (GUI): {#eec8 .graf .graf--h3 .graf-after--pre name="eec8"}

Just open and click --- powerful for visual learners.

Great for:

- [Debugging application-level issues]{#92f7}
- [Capturing authentication attempts]{#16f3}
- [Security analysis]{#c7f3}

### 17. `systemctl status network`{.markup--code .markup--h3-code} (Linux) / `services.msc`{.markup--code .markup--h3-code} (Windows) {#3248 .graf .graf--h3 .graf-after--li name="3248"}

These help you check the **health of network services** on the OS level.

### Linux: {#89d0 .graf .graf--h3 .graf-after--p name="89d0"}

``` {#f3f0 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
systemctl status NetworkManager
```

### Windows: {#186a .graf .graf--h3 .graf-after--pre name="186a"}

Press `Win + R`{.markup--code .markup--p-code} \>
`services.msc`{.markup--code .markup--p-code} and look for DHCP, DNS
Client, WLAN AutoConfig.

### 18. `powercfg`{.markup--code .markup--h3-code} (Windows) --- Check Sleep & Network Power Settings {#5ff5 .graf .graf--h3 .graf-after--p name="5ff5"}

Ever had a network adapter turn off randomly?

### Usage: {#3a8a .graf .graf--h3 .graf-after--p name="3a8a"}

``` {#5e67 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
powercfg -devicequery wake_armed
```

You can adjust power settings to prevent disconnections during sleep.

### 19. `tasklist`{.markup--code .markup--h3-code} / `ps`{.markup--code .markup--h3-code} --- See Who's Eating Your Network {#feb1 .graf .graf--h3 .graf-after--p name="feb1"}

### Windows: {#e3ec .graf .graf--h3 .graf-after--h3 name="e3ec"}

``` {#4762 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
tasklist
```

### Linux/macOS: {#ce75 .graf .graf--h3 .graf-after--pre name="ce75"}

``` {#b9e7 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
ps aux | grep <process_name>
```

Useful to pair with `netstat`{.markup--code .markup--p-code} to trace
back active connections to their process origin.

### Final Thoughts: Why Knowing These Commands Pays Off {#58e7 .graf .graf--h3 .graf-after--p name="58e7"}

In the IT world, **problems don't wait for you to open a GUI tool**.
Whether you're remoted into a server, on a call with an angry
stakeholder, or racing to resolve a 2 AM incident --- these commands are
your first line of defense.

More than just troubleshooting, these tools give you:

- [**Visibility**: What's going on in your network.]{#395a}
- [**Control**: The ability to fix things on the fly.]{#0eba}
- [**Speed**: Solutions in seconds, not minutes.]{#6b12}

### Promote and Collaborate on Cybersecurity Insights {#a551 .graf .graf--h3 .graf-after--li name="a551"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#1575 .graf .graf--h3 .graf-after--p name="1575"}

[Vijay
Gupta](https://www.youtube.com%2F@www.youtube.com/@bevijaygupta){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com%2F@www.youtube.com/@bevijaygupta"
rel="noopener ugc nofollow noopener" target="_blank"} is a cybersecurity
enthusiast with several years of experience in cyber security, [cyber
crime forensics
investigation](https://play.google.com/store/books/series?id=_vUpHAAAABDW6M){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/series?id=_vUpHAAAABDW6M"
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
.h-card} on [June 1, 2025](https://medium.com/p/4fffe3c8a08b).

[Canonical
link](https://medium.com/@bevijaygupta/network-commands-every-it-team-should-know-4fffe3c8a08b){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
