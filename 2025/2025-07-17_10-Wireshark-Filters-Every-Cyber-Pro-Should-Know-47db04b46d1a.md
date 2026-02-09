---
title: "10 Wireshark Filters Every Cyber Pro Should Know 47db04b46d1a"
platform: Medium
original_file: 2025-07-17_10-Wireshark-Filters-Every-Cyber-Pro-Should-Know-47db04b46d1a.md
---

# 10 Wireshark Filters Every Cyber Pro Should Know 47db04b46d1a

::: {}
# 10 Wireshark Filters Every Cyber Pro Should Know {#wireshark-filters-every-cyber-pro-should-know .p-name}
:::

::: {.section .p-summary field="subtitle"}
In the world of cybersecurity, network traffic is like a noisy
crowd --- full of random chatter, but hidden somewhere is the one
voice...
:::

::::::: {.section .e-content field="body"}
:::::: {#4c29 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 10 Wireshark Filters Every Cyber Pro Should Know {#6832 .graf .graf--h3 .graf--leading .graf--title name="6832"}

<figure id="b807" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*lSj3sdOmL2yG49mL.jpg"
class="graf-image" data-image-id="0*lSj3sdOmL2yG49mL.jpg"
data-width="705" data-height="397" data-is-featured="true" />
</figure>

In the world of cybersecurity, network traffic is like a noisy
crowd --- full of random chatter, but hidden somewhere is the one voice
you're trying to hear. Whether you're a beginner just starting out or a
seasoned analyst, **Wireshark** is one of the most powerful tools in
your toolkit. But knowing how to open Wireshark isn't enough --- knowing
how to filter the noise and zoom into what matters is what separates
amateurs from professionals.

Today, we'll dive into **10+ powerful Wireshark display filters** that
every cyber pro should know --- explained simply, with real-world
context, use cases, and tips.

### Why Filters Matter in Wireshark {#5b7a .graf .graf--h3 .graf-after--p name="5b7a"}

Wireshark can capture **hundreds of thousands of packets** in a single
session. Without filters, it's like finding a needle in a haystack.
Filters help you:

- [Isolate suspicious behavior.]{#2b60}
- [Investigate incidents faster.]{#3693}
- [Understand protocols better.]{#727f}
- [Catch vulnerabilities in real time.]{#033a}

Let's break down these must-know filters into real use cases you'll
actually encounter.

### 1. `tcp.port == 443`{.markup--code .markup--h3-code} → Filter HTTPS Traffic {#cda7 .graf .graf--h3 .graf-after--p name="cda7"}

Most secure web traffic today runs over **port 443**, the standard port
for **HTTPS**.

**Use Case:**\
 You're analyzing web traffic to ensure a user is visiting only
encrypted websites. This filter will help you zero in on traffic that's
being sent securely.

**Bonus Tip:** If you're capturing decrypted SSL/TLS traffic (e.g., with
SSLKEYLOG), this helps you narrow down full sessions.

### 2. `http.request`{.markup--code .markup--h3-code} → Catch All HTTP Requests {#9ef5 .graf .graf--h3 .graf-after--p name="9ef5"}

Want to catch all **unsecured web browsing**? This filter shows every
**HTTP request**, including GET, POST, and even HEAD requests.

**Use Case:**\
 Monitoring user behavior on a network, seeing which websites are
accessed, and identifying potential privacy leaks or data exfiltration
attempts.

**Why It Matters:** HTTP data often travels **unencrypted**, making it a
goldmine for packet sniffers and a red flag for security.

### 3. `tcp.flags.syn == 1 && tcp.flags.ack == 0`{.markup--code .markup--h3-code} → Show Only SYN Packets {#d8ff .graf .graf--h3 .graf-after--p name="d8ff"}

This is a classic for identifying **connection attempts**.

**Use Case:**\
 If you're looking for **network scanning activity**, attackers often
send SYN packets to probe open ports (think Nmap).

**Why It Matters:** If you see a **lot of SYNs with no ACKs**, you may
be witnessing a **reconnaissance scan** or a **half-open (SYN) attack**.

### 4. `dns`{.markup--code .markup--h3-code} → All DNS Traffic {#7866 .graf .graf--h3 .graf-after--p name="7866"}

DNS is like the phonebook of the internet. Attackers abuse it all the
time.

**Use Case:**\
 Detecting **suspicious domain lookups**, typo-squatting, or **command &
control (C2)** infrastructure.

**Why It Matters:** DNS traffic can often reveal **malware trying to
phone home** or **users accessing sketchy domains**.

**Bonus:** Use `dns.qry.name contains ".xyz"`{.markup--code
.markup--p-code} to filter specific TLDs often abused in phishing.

### 5. `ftp`{.markup--code .markup--h3-code} → Filter FTP Traffic {#0423 .graf .graf--h3 .graf-after--p name="0423"}

FTP is **ancient** and **insecure**, but it still exists in many legacy
systems.

**Use Case:**\
 Looking for sensitive data being transferred in clear text, like
**usernames and passwords**.

**Why It Matters:** FTP transmits everything unencrypted. You can
literally read credentials in the packet details. Huge red flag!

### 6. `icmp`{.markup--code .markup--h3-code} → Echo Requests & Replies (aka ping) {#b18e .graf .graf--h3 .graf-after--p name="b18e"}

This filter isolates **ICMP traffic**, which includes **ping
requests/replies**.

**Use Case:**\
 Troubleshooting connectivity or spotting **ICMP flooding** (a basic
DDoS attack).

**Why It Matters:** While mostly harmless, excessive ICMP traffic can
indicate malicious reconnaissance or denial-of-service activity.

### 7. `tcp contains "password"`{.markup--code .markup--h3-code} → Search for Password Leaks 😬 {#2778 .graf .graf--h3 .graf-after--p name="2778"}

This is an **old-school hacker trick**, and sadly, it still works on
poorly secured systems.

**Use Case:**\
 Scan for packets that might be leaking passwords in clear text,
especially on HTTP, FTP, or SMTP sessions.

**Why It Matters:** In pen testing, this is a fast way to uncover
**credential leaks** from outdated applications.

### 8. `tcp.analysis.retransmission`{.markup--code .markup--h3-code} → Spot Retransmissions {#7471 .graf .graf--h3 .graf-after--p name="7471"}

Wireshark marks these when packets are **resent**.

**Use Case:**\
 Diagnosing network performance issues, identifying **congested links**
or **flaky connections**.

**Why It Matters:** Constant retransmissions waste bandwidth and hurt
user experience. In a security context, they can also point to
**interception** or **traffic shaping**.

### 9. `tcp.flags.reset == 1`{.markup--code .markup--h3-code} → Spot TCP Resets {#28c9 .graf .graf--h3 .graf-after--p name="28c9"}

A TCP reset (RST flag) closes a connection **abruptly**.

**Use Case:**\
 You may see this during **scanning attempts**, where a service rejects
unexpected probes. Or during **DoS mitigation**.

**Why It Matters:** Too many RSTs could mean someone's trying to disrupt
connections or perform **TCP RST injection attacks**.

### 10. `udp.port == 53`{.markup--code .markup--h3-code} → All DNS Queries via UDP {#3117 .graf .graf--h3 .graf-after--p name="3117"}

Unlike filter #4, this one specifically targets **UDP-based DNS**, the
most common method.

**Use Case:**\
 Catch **bulk DNS lookups**, sometimes automated by malware or
aggressive tracking scripts.

**Why It Matters:** DNS over UDP is fast but **easily spoofed or
intercepted**, which is why monitoring it is crucial.

### Bonus Filters (Advanced Use) {#eaa5 .graf .graf--h3 .graf-after--p name="eaa5"}

Once you've mastered the above 10, here are **pro-level filters** to
level up your Wireshark skills:

### `frame contains "admin"`{.markup--code .markup--h3-code} → Search Payloads for "admin" {#7ea5 .graf .graf--h3 .graf-after--p name="7ea5"}

**Use Case:**\
 Looking for hardcoded credentials, login attempts, or admin panels in
traffic.

**Warning:** Requires packets to have **unencrypted payloads**.

### `ssl.handshake.version`{.markup--code .markup--h3-code} → Filter SSL/TLS Handshakes {#684c .graf .graf--h3 .graf-after--p name="684c"}

**Use Case:**\
 Check the TLS versions used in handshakes. Are they using **TLS 1.0**
or **1.1** (deprecated)? Time to flag it!

**Tip:** Combine with `tls.handshake.version == 0x0301`{.markup--code
.markup--p-code} to find TLS 1.0.

### `tcp.stream eq 1`{.markup--code .markup--h3-code} → Follow a Specific TCP Conversation {#4cb1 .graf .graf--h3 .graf-after--p name="4cb1"}

Every TCP stream in Wireshark gets a unique number.

**Use Case:**\
 Troubleshooting a slow-loading website? Use this filter to follow the
back-and-forth of just one user session.

**Tip:** Right-click any packet and choose "Follow TCP Stream" to
auto-filter it.

### `ip.proto == 1`{.markup--code .markup--h3-code} → All ICMP Traffic {#3128 .graf .graf--h3 .graf-after--p name="3128"}

An alternate way to view ICMP (echo, time exceeded, unreachable, etc.)

**Use Case:**\
 Filter **ICMP scanning**, traceroutes, or detect ICMP tunneling (used
in covert data exfiltration).

### `eth.addr == aa:bb:cc:dd:ee:ff`{.markup--code .markup--h3-code} → Filter by MAC Address {#d3bc .graf .graf--h3 .graf-after--p name="d3bc"}

**Use Case:**\
 Troubleshoot one specific device in a crowded office or Wi-Fi network.

**Why It Matters:** IPs change. MACs don't.

### `tcp.analysis.flags`{.markup--code .markup--h3-code} → Show TCP Anomalies {#1f8c .graf .graf--h3 .graf-after--p name="1f8c"}

This is the **Swiss Army knife** of TCP analysis.

**Use Case:**\
 Catch **duplicate ACKs**, **retransmissions**, **zero-window events**,
and **bad TCP behavior**.

**Why It Matters:** It helps both **network admins** and **cybersecurity
analysts** detect deeper problems or odd behaviors that can be
security-related.

### `tcp.len == 0`{.markup--code .markup--h3-code} → Empty TCP Payloads {#5dc4 .graf .graf--h3 .graf-after--p name="5dc4"}

These often appear during **keep-alive messages** or **SYN/ACK
handshakes**.

**Use Case:**\
 Spot when sessions are being kept open unnecessarily or where nothing
meaningful is transmitted.

### Final Thoughts: Sniff Smarter, Not Harder {#d57f .graf .graf--h3 .graf-after--p name="d57f"}

Mastering these filters gives you a **superpower** in traffic analysis.
With the right display filters, you can cut through noise like a
surgeon --- isolating threats, investigating incidents, and learning how
your network truly behaves.

Here's how to go further:

### Tips for Practicing Wireshark Filters: {#d7f9 .graf .graf--h3 .graf-after--p name="d7f9"}

- [**Use sample PCAPs** from malware-traffic-analysis.net.]{#66f9}
- [**Capture your own traffic** (on a test machine!) and try filters
  live.]{#9809}
- [**Try filtering encrypted vs unencrypted sessions.**]{#7107}
- [**Challenge yourself:** Try building a timeline using only
  filters.]{#4729}
:::
::::
::::::
:::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [July 17, 2025](https://medium.com/p/47db04b46d1a).

[Canonical
link](https://medium.com/@bevijaygupta/10-wireshark-filters-every-cyber-pro-should-know-47db04b46d1a){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
