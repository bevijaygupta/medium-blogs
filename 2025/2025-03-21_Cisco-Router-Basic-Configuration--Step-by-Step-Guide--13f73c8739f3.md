---
title: "Cisco Router Basic Configuration  Step by Step Guide  13f73c8739f3"
platform: Medium
original_file: 2025-03-21_Cisco-Router-Basic-Configuration--Step-by-Step-Guide--13f73c8739f3.md
---

# Cisco Router Basic Configuration  Step by Step Guide  13f73c8739f3

::: {}
# Cisco Router Basic Configuration (Step by Step Guide) {#cisco-router-basic-configuration-step-by-step-guide .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction
:::

::::::: {.section .e-content field="body"}
:::::: {#7dd8 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Cisco Router Basic Configuration (Step by Step Guide) {#ecff .graf .graf--h3 .graf--leading .graf--title name="ecff"}

<figure id="ccdf" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*aJ53N01SmDjshMhz"
class="graf-image" data-image-id="0*aJ53N01SmDjshMhz" data-width="311"
data-height="162" />
</figure>

### Introduction {#7ba7 .graf .graf--h3 .graf-after--figure name="7ba7"}

Cisco routers are essential networking devices used for connecting
different networks and managing traffic efficiently. Configuring a Cisco
router correctly is crucial to ensure network stability, security, and
efficiency. This guide provides a detailed, step-by-step explanation of
basic Cisco router configuration, including essential commands,
interface setup, VLAN configuration, routing, ACLs, switch port
security, and troubleshooting techniques.

### 1. Basic Device Setup {#59cf .graf .graf--h3 .graf-after--p name="59cf"}

Before configuring a Cisco router, you need to log in and access the
command-line interface (CLI). Once inside, basic commands allow you to
manage the device settings and configurations efficiently.

### Logging In and Basic Commands {#f7bb .graf .graf--h3 .graf-after--p name="f7bb"}

When you first connect to a Cisco router, you will be in user EXEC mode,
which provides limited access to commands. To perform configuration
tasks, you need to enter privileged EXEC mode:

``` {#75f1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
enable
```

This command allows you to enter privileged EXEC mode, where you can
execute administrative commands.

Next, enter global configuration mode:

``` {#1d21 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
configure terminal
```

In this mode, you can make changes to the router configuration. To
assign a name to your router, use:

``` {#73ad .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
hostname MyRouter
```

This command sets the router's hostname to "MyRouter," making it easier
to identify in the network.

To exit from the current mode, use:

``` {#fd9d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
exit
```

This will return you to the previous mode.

### Saving and Viewing Configurations {#c82b .graf .graf--h3 .graf-after--p name="c82b"}

To save your current configuration so that it persists after a reboot,
use:

``` {#72ce .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
copy running-config startup-config
```

To display the active configuration currently running on the device,
use:

``` {#77ed .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
show running-config
```

To view the saved configuration stored in non-volatile memory, use:

``` {#dfd7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
show startup-config
```

### Erasing Configurations {#4d15 .graf .graf--h3 .graf-after--pre name="4d15"}

If you need to erase the startup configuration and reset the router to
factory settings, use:

``` {#30c0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
erase startup-config
reload
```

The `reload`{.markup--code .markup--p-code} command restarts the router,
applying any cleared configurations.

### 2. Interface Configuration {#8420 .graf .graf--h3 .graf-after--p name="8420"}

Interfaces connect the router to networks. Properly configuring them
ensures smooth communication.

### Basic Interface Setup {#f82c .graf .graf--h3 .graf-after--p name="f82c"}

To configure an interface, use:

``` {#bf99 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
interface GigabitEthernet0/1
 description Connection to LAN
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit
```

This assigns an IP address to the interface and brings it online.

### Common Interface Commands {#14c7 .graf .graf--h3 .graf-after--p name="14c7"}

- [**View interface status:** `show ip interface brief`{.markup--code
  .markup--li-code}]{#a2b3}
- [**Disable an interface:** `shutdown`{.markup--code
  .markup--li-code}]{#ccf2}
- [**Enable an interface:** `no shutdown`{.markup--code
  .markup--li-code}]{#b66f}

### 3. VLAN Configuration {#e2b0 .graf .graf--h3 .graf-after--li name="e2b0"}

Virtual LANs (VLANs) segment a network into separate broadcast domains.

### Configuring a VLAN {#26d5 .graf .graf--h3 .graf-after--p name="26d5"}

``` {#85d8 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
vlan 10
 name Sales
 exit
```

Assign an interface to the VLAN:

``` {#0dd8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
interface GigabitEthernet0/2
 switchport mode access
 switchport access vlan 10
 exit
```

To verify VLANs:

``` {#d5c2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
show vlan brief
```

### 4. Trunk Configuration {#9fa5 .graf .graf--h3 .graf-after--pre name="9fa5"}

Trunk ports carry multiple VLANs between switches.

``` {#b972 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
interface GigabitEthernet0/3
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 exit
```

To verify trunk settings:

``` {#b86f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
show interfaces trunk
```

### 5. Routing {#9b0d .graf .graf--h3 .graf-after--pre name="9b0d"}

### Configuring a Static Route {#e867 .graf .graf--h3 .graf-after--h3 name="e867"}

``` {#751b .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ip route 192.168.2.0 255.255.255.0 192.168.1.2
```

This routes packets for the 192.168.2.0 network through 192.168.1.2.

### Configuring OSPF Routing {#1b17 .graf .graf--h3 .graf-after--p name="1b17"}

``` {#6d82 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 exit
```

To verify routes:

``` {#dd91 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
show ip route
```

### 6. Access Control Lists (ACLs) {#6da3 .graf .graf--h3 .graf-after--pre name="6da3"}

ACLs control traffic flow by permitting or denying packets based on
source, destination, and protocol.

### Standard ACL Example {#23f9 .graf .graf--h3 .graf-after--p name="23f9"}

``` {#0812 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
access-list 10 permit 192.168.1.0 0.0.0.255
interface GigabitEthernet0/1
 ip access-group 10 in
 exit
```

### Extended ACL Example {#e7b0 .graf .graf--h3 .graf-after--pre name="e7b0"}

``` {#3c50 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
access-list 101 permit tcp 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255 eq 80
```

To verify ACLs:

``` {#f21d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
show access-lists
```

### 7. Switch Port Security {#aa2a .graf .graf--h3 .graf-after--pre name="aa2a"}

Switch port security restricts access based on MAC addresses.

``` {#90d8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
interface GigabitEthernet0/1
 switchport port-security
 switchport port-security maximum 2
 switchport port-security mac-address sticky
 switchport port-security violation restrict
 exit
```

To verify:

``` {#396d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
show port-security interface GigabitEthernet0/1
```

### 8. Troubleshooting {#8fca .graf .graf--h3 .graf-after--pre name="8fca"}

Network issues require effective troubleshooting tools.

### Basic Troubleshooting Commands {#2a5f .graf .graf--h3 .graf-after--p name="2a5f"}

- [**Check connectivity:** `ping 192.168.1.2`{.markup--code
  .markup--li-code}]{#9df2}
- [**Trace network path:** `traceroute 192.168.1.2`{.markup--code
  .markup--li-code}]{#5e24}
- [**View connected Cisco devices:** `show cdp neighbors`{.markup--code
  .markup--li-code}]{#f69a}
- [**View ARP table:** `show ip arp`{.markup--code
  .markup--li-code}]{#552f}
- [**Check router version:** `show version`{.markup--code
  .markup--li-code}]{#5262}
- [**Enable debugging:** `debug ip ospf events`{.markup--code
  .markup--li-code}]{#e224}

### Conclusion {#172b .graf .graf--h3 .graf-after--li name="172b"}

Configuring a Cisco router step by step ensures proper network operation
and security. This guide covered essential topics like basic setup,
interface configuration, VLANs, routing, ACLs, and troubleshooting.
Mastering these commands will help you build and manage efficient
network infrastructures. Keep practicing these configurations on lab
environments to gain confidence before implementing them in production
networks.

### Promote and Collaborate on Cybersecurity Insights {#ade0 .graf .graf--h3 .graf-after--p name="ade0"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#dd45 .graf .graf--h3 .graf-after--p name="dd45"}

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
.h-card} on [March 21, 2025](https://medium.com/p/13f73c8739f3).

[Canonical
link](https://medium.com/@bevijaygupta/cisco-router-basic-configuration-step-by-step-guide-13f73c8739f3){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
