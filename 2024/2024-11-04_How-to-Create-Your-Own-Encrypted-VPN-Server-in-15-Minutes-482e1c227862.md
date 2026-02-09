---
title: "How to Create Your Own Encrypted VPN Server in 15 Minutes 482e1c227862"
platform: Medium
original_file: 2024-11-04_How-to-Create-Your-Own-Encrypted-VPN-Server-in-15-Minutes-482e1c227862.md
---

# How to Create Your Own Encrypted VPN Server in 15 Minutes 482e1c227862

::: {}
# How to Create Your Own Encrypted VPN Server in 15 Minutes {#how-to-create-your-own-encrypted-vpn-server-in-15-minutes .p-name}
:::

::: {.section .p-summary field="subtitle"}
Setting up your own VPN server has become increasingly popular as
privacy concerns rise and online censorship becomes more prevalent. A...
:::

::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#4754 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### How to Create Your Own Encrypted VPN Server in 15 Minutes {#5b9d .graf .graf--h3 .graf--leading .graf--title name="5b9d"}

<figure id="e251" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*fDbiwvz5PRZ8NsEW.jpg"
class="graf-image" data-image-id="0*fDbiwvz5PRZ8NsEW.jpg"
data-width="2000" data-height="1333" data-is-featured="true" />
</figure>

Setting up your own VPN server has become increasingly popular as
privacy concerns rise and online censorship becomes more prevalent. A
personal, encrypted VPN server not only lets you browse the web securely
but also keeps your data private from third parties. Best of all, it's
something you can set up in as little as 15 minutes. This guide will
walk you through creating your own encrypted VPN server using
**OpenVPN** on a cloud service provider, like DigitalOcean, AWS, or even
on your own hardware.
:::
::::
::::::

:::::: {#7d53 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Why Set Up Your Own VPN Server? {#4c6f .graf .graf--h3 .graf--leading name="4c6f"}

While there are many VPN providers available, a personal VPN offers
several unique advantages:

1.  [**Enhanced Privacy**: Unlike commercial VPNs, where your data
    passes through their servers, a private VPN ensures you control who
    has access to your data.]{#7f36}
2.  [**Reduced Risk of Data Logging**: No third party can log your data
    or internet activity if you're running the VPN.]{#c65f}
3.  [**Control Over the Server Location**: Choose the server's location
    to improve your browsing experience or access geo-restricted
    content.]{#03ec}
4.  [**Customizable Security**: A personal VPN allows you to select
    encryption and security settings tailored to your needs.]{#6d5d}
:::
::::
::::::

:::::: {#e0c2 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Prerequisites {#7823 .graf .graf--h3 .graf--leading name="7823"}

Before we begin, here's what you'll need:

1.  [**A Cloud Server**: You'll need a server to host your VPN.
    Providers like DigitalOcean, AWS, Linode, and Vultr offer
    budget-friendly options. You can choose an instance with at least
    1GB RAM.]{#6895}
2.  [**Basic Terminal Knowledge**: We'll use terminal commands for this
    setup.]{#ffaf}
3.  [**Domain Name (Optional)**: A domain makes accessing the VPN easier
    but isn't strictly necessary.]{#0975}
:::
::::
::::::

:::::: {#ba8c .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 1: Setting Up Your Server {#0b94 .graf .graf--h3 .graf--leading name="0b94"}

**Sign Up for a Cloud Provider**:

- [Choose a provider, like **DigitalOcean**, **AWS**, or **Linode**, and
  set up an account.]{#5b6a}
- [If you're a beginner, **DigitalOcean** is user-friendly and offers a
  \$5/month plan that is perfect for hosting a VPN server.]{#449d}

**Create a New Droplet (Server)**:

- [Choose **Ubuntu** as the operating system (OS). Ubuntu 20.04 is
  stable and widely used for OpenVPN setups.]{#27ad}
- [Select a data center region close to your location for better
  performance.]{#6d17}

**Launch the Server**:

- [Once your droplet is created, note down the IP address. You'll use
  this to SSH into the server.]{#9ee5}
:::
::::
::::::

:::::: {#a5bf .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 2: Connecting to Your Server via SSH {#25d8 .graf .graf--h3 .graf--leading name="25d8"}

**Open Terminal**:

- [If you're on Linux or macOS, use the built-in Terminal. Windows users
  can use PowerShell or an SSH client like PuTTY.]{#6c47}

**Connect to Your Server**:

- [Enter the following command, replacing `your_server_ip`{.markup--code
  .markup--li-code} with your server's IP address:]{#ed73}
- [`ssh root@your_server_ip`{.markup--code .markup--li-code}]{#f799}
- [If prompted, type "yes" to confirm the connection and enter your
  password when prompted.]{#8491}
:::
::::
::::::

:::::: {#5a70 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 3: Install OpenVPN and Easy-RSA {#a12e .graf .graf--h3 .graf--leading name="a12e"}

OpenVPN is a powerful, open-source VPN solution. We'll also use
**Easy-RSA**, a command-line tool for creating and managing SSL keys, to
generate encryption keys.

**Update the System**:

- [`sudo apt update && sudo apt upgrade -y`{.markup--code
  .markup--li-code}]{#9fcc}

**Install OpenVPN and Easy-RSA**:

- [`sudo apt install openvpn easy-rsa -y`{.markup--code
  .markup--li-code}]{#69c8}
:::
::::
::::::

:::::: {#410e .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 4: Configuring Easy-RSA to Generate Encryption Keys {#370f .graf .graf--h3 .graf--leading name="370f"}

Encryption keys are crucial to securing the VPN connection. Easy-RSA
makes this process easy.

1.  [**Create a Directory for Easy-RSA**:]{#6afb}

- [`make-cadir ~/openvpn-ca cd ~/openvpn-ca`{.markup--code
  .markup--li-code}]{#7e30}

**Configure Easy-RSA Variables**:

- [Open the **vars** file in a text editor:]{#ca36}
- [`nano vars`{.markup--code .markup--li-code}]{#b946}
- [Customize fields like `KEY_COUNTRY`{.markup--code .markup--li-code},
  `KEY_PROVINCE`{.markup--code .markup--li-code},
  `KEY_CITY`{.markup--code .markup--li-code}, `KEY_ORG`{.markup--code
  .markup--li-code}, and `KEY_EMAIL`{.markup--code .markup--li-code}
  according to your preference. Save and close the file (Ctrl + X, then
  Y to confirm).]{#6049}

**Generate the Certificate Authority (CA)**:

- [Initialize the Easy-RSA environment:]{#a5b3}
- [`source vars ./clean-all ./build-ca`{.markup--code
  .markup--li-code}]{#2bf1}

**Create a Server Certificate and Key**:

- [`./build-key-server server`{.markup--code .markup--li-code}]{#8f74}
- [Follow the prompts and leave the `challenge password`{.markup--code
  .markup--li-code} blank.]{#6120}
- [When asked to sign the certificate, type **yes**.]{#1feb}

**Generate Diffie-Hellman Parameters**:

- [`./build-dh`{.markup--code .markup--li-code}]{#de10}

**Generate an HMAC Signature to Enhance Security**:

- [`openvpn --genkey --secret keys/ta.key`{.markup--code
  .markup--li-code}]{#c60f}
:::
::::
::::::

:::::: {#48b5 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 5: Configuring the OpenVPN Server {#2187 .graf .graf--h3 .graf--leading name="2187"}

With the keys generated, the next step is to configure OpenVPN.

1.  [**Copy the Server Keys**:]{#a4b6}

- [`sudo cp ~/openvpn-ca/keys/{server.crt,server.key,ca.crt,dh2048.pem,ta.key} /etc/openvpn`{.markup--code
  .markup--li-code}]{#a906}

**Create the OpenVPN Server Configuration File**:

- [Open the OpenVPN configuration file:]{#7299}
- [`sudo nano /etc/openvpn/server.conf`{.markup--code
  .markup--li-code}]{#38c6}
- [Paste the following configuration:]{#34e7}
- [`port 1194 proto udp dev tun ca ca.crt cert server.crt key server.key dh dh2048.pem auth SHA256 tls-auth ta.key 0 persist-key persist-tun user nobody group nogroup server 10.8.0.0 255.255.255.0 ifconfig-pool-persist ipp.txt push "redirect-gateway def1 bypass-dhcp" push "dhcp-option DNS 8.8.8.8" push "dhcp-option DNS 8.8.4.4" keepalive 10 120 cipher AES-256-CBC comp-lzo max-clients 10 status openvpn-status.log log-append /var/log/openvpn.log verb 3`{.markup--code
  .markup--li-code}]{#3b11}
- [Save and close the file (Ctrl + X, then Y to confirm).]{#e9f4}
:::
::::
::::::

:::::: {#9a6d .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 6: Starting and Enabling OpenVPN {#05c1 .graf .graf--h3 .graf--leading name="05c1"}

1.  [**Enable and Start the OpenVPN Service**:]{#bfd3}

- [`sudo systemctl start openvpn@server sudo systemctl enable openvpn@server`{.markup--code
  .markup--li-code}]{#b9b4}

**Verify the VPN Service**:

- [Check if the VPN is active by running:]{#03a1}
- [`sudo systemctl status openvpn@server`{.markup--code
  .markup--li-code}]{#0281}
:::
::::
::::::

:::::: {#776c .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 7: Configuring Firewall and Network Settings {#a645 .graf .graf--h3 .graf--leading name="a645"}

**Enable IP Forwarding**:

- [Open the **sysctl.conf** file:]{#a2b2}
- [`sudo nano /etc/sysctl.conf`{.markup--code .markup--li-code}]{#3c2a}
- [Uncomment or add the following line:]{#9d77}
- [`net.ipv4.ip_forward=1`{.markup--code .markup--li-code}]{#b0bd}
- [Apply the change:]{#57c8}
- [`sudo sysctl -p`{.markup--code .markup--li-code}]{#196e}

**Set Up Firewall Rules**:

- [Allow VPN traffic and enable NAT to route traffic through the
  VPN:]{#70b5}
- [`sudo ufw allow 1194/udp sudo ufw enable`{.markup--code
  .markup--li-code}]{#0be1}
:::
::::
::::::

:::::: {#a33f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 8: Creating Client Configurations {#425c .graf .graf--h3 .graf--leading name="425c"}

Finally, let's set up a client configuration file so you can connect to
your VPN from your devices.

**Generate Client Certificates**:

- [`cd ~/openvpn-ca source vars ./build-key client1`{.markup--code
  .markup--li-code}]{#76ee}

**Create a Client Configuration File**:

- [Save the following configuration to a file named
  `client.ovpn`{.markup--code .markup--li-code}:]{#907c}
- [`client dev tun proto udp remote your_server_ip 1194 resolv-retry infinite nobind persist-key persist-tun remote-cert-tls server auth SHA256 cipher AES-256-CBC comp-lzo verb 3`{.markup--code
  .markup--li-code}]{#3f3e}
- [Insert your certificates and keys inline.]{#a98d}
:::
::::
::::::

:::::: {#822f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Step 9: Connecting to Your VPN {#9b7d .graf .graf--h3 .graf--leading name="9b7d"}

To connect, use the OpenVPN client software (available on Windows,
macOS, Android, and iOS) and import the `client.ovpn`{.markup--code
.markup--p-code} configuration file.
:::
::::
::::::

:::::: {#c92c .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Final Thoughts {#fb19 .graf .graf--h3 .graf--leading name="fb19"}

Setting up your own encrypted VPN server in just 15 minutes provides a
fast, reliable, and private way to secure your internet connection. With
your VPN server, you can have more control over your internet privacy
and bypass geo-restrictions safely. As online privacy becomes
increasingly important, a personal VPN is an invaluable tool for keeping
your information secure.

### Promote and Collaborate on Cybersecurity Insights {#0c91 .graf .graf--h3 .graf-after--p name="0c91"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#4def .graf .graf--h3 .graf-after--p name="4def"}

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
.h-card} on [November 4, 2024](https://medium.com/p/482e1c227862).

[Canonical
link](https://medium.com/@bevijaygupta/how-to-create-your-own-encrypted-vpn-server-in-15-minutes-482e1c227862){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
