---
title: "Zero Logon TryHackme Writeup 015cfe5f54b0"
platform: Medium
original_file: 2024-09-02_Zero-Logon-TryHackme-Writeup-015cfe5f54b0.md
---

# Zero Logon TryHackme Writeup 015cfe5f54b0

::: {}
# Zero Logon TryHackme Writeup {#zero-logon-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/zer0logon Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#acca .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Zero Logon TryHackme Writeup {#18df .graf .graf--h3 .graf--leading .graf--title name="18df"}

<figure id="e996" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*uM09cEl4S-qqzpIC.png"
class="graf-image" data-image-id="0*uM09cEl4S-qqzpIC.png"
data-width="507" data-height="235" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/zer0logon](https://tryhackme.com/room/zer0logon){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/zer0logon"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### Zero Logon --- The Zero Day Angle {#514e .graf .graf--h3 .graf-after--p name="514e"}

**About The vulnerability -**

On September 14, Secura released a whitepaper for CVE-2020--1472, that
allowed an attacker to go from Zero to Domain Admin in approximately one
minute. They dubbed this vulnerability Zero Logon.

Zero Logon is a purely statistics based attack that abuses a feature
within MS-NRPC (Microsoft NetLogon Remote Protocol), MS-NRPC is a
critical authentication component of Active Directory that handles
authentication for User and Machine accounts. In short --- the attack
mainly focuses on a poor implementation of Cryptography. To be more
specific, Microsoft chose to use AES-CFB8 for a function called
ComputeNetlogonCredential, which is normally fine, except they had hard
coded the Initialization Vector to use all zeros instead of a random
string. When an attacker sends a message only containing zeros with the
IV of zero, there is a 1-in-256 chance that the Ciphertext will be Zero.

But how is that useful to us? We'll touch on that note in the following
sections.

**About Machine Accounts -**

Normally, if we tried a statistics based attack on any user account, we
would get locked out. This is not the case if we apply this principal to
machine accounts. Machines accounts behave in a much different way than
standard user accounts. They have no predefined account lockout attempts
because a 64+ character alpha numeric password is normally used to
secure them, making them very difficult to break into. They're not meant
to be accessed by an end user by any means. In certain circumstances, we
can dump the machine account password using a tool like Mimikatz, but if
we're at that point, we've already compromised the machine --- and we're
looking for persistence within the domain, not lateral movement.

**Abusing the Vulnerability -**

Machine accounts often hold system level privileges which we can use for
a variety of things. If you're not familiar with Active Directory, we
can take the Domain Controller's Machine Account and attempt to use the
granted authentication in conjunction with Secretsdump.py (SecretsDump
is a password dumping utility like Mimikatz, except it lives on the
Network instead of the host) to dump all of the passwords within the
domain. At this point we have a rough kill chain starting to form:

Use Zero Logon to bypass authentication on the Domain Controller's
Machine Account -\> Run Secretsdump.py to dump credentials -\>
Crack/Pass Domain Admin Hashes -\> ??? -\> Profit

**Analyzing the MS-NRPC Logon Process -**

At this point, we know a vulnerability exists, but we're not quite sure
how to exploit it yet. We'll be covering that soon, but what we do know
there's a vulnerability within the way Microsoft handles Authentication
within ComputeNetLogonCredetial function of MS-NRPC. To better
understand the vulnerability, we need to do a bit of a deeper dive on
how Microsoft handles authentication to NRPC.

To analyze where the vulnerability occurs, we'll be using the Diagram
provided by Secura as well as Microsoft Documentation to decipher the
magic behind Zero Logon. The sources can be found at the bottom of this
task.

<figure id="c8ed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*X45BkcVAzwTghIIv.png"
class="graf-image" data-image-id="0*X45BkcVAzwTghIIv.png"
data-width="875" data-height="598" />
</figure>

[https://tryhackme.com/room/zer0logon](https://tryhackme.com/room/zer0logon){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/zer0logon"
rel="noopener ugc nofollow noopener" target="_blank"}

*Source: Secura*

**Step 1**. The client creates a NetrServerReqChallenge and sends it off
*\[Figure 1. Step 1\]*. This contains the following values:

1\. The DC

2\. The Target Device (Also the DC, in our case)

3\. A Nonce (In our case is 16 Bytes of Zero).

**Step 2**. The server receives the NetrServerReqChallenge, the server
will then generate it's own Nonce (This is called the Server Challenge),
the server will send the Server Challenge back. *\[Figure 1. Step 2\]*

**Step 3**. The client (us) will compute it's NetLogon Credentials with
the Server Challenge provided *\[Figure 1. Step 3\]*. It uses the
NetrServerAuthenticate3 method which requires the following parameters:

1\. A Custom Binding Handle (Impacket handles this for us, it's
negotiated prior)

2\. An Account Name (The Domain Controller's machine account name. ex:
DC01\$)

3\. A Secure Channel Type (Impacket sort of handles this for us, but we
still need to specify it:
\[nrpc.NETLOGON_SECURE_CHANNEL_TYPE.ServerSecureChannel\])

4\. The Computer Name (The Domain Controller ex: DC01)

5\. The Client Credential String (this will be 8 hextets of \\x00 \[16
Bytes of Zero\])

6\. Negotiation Flags (The following value observed from a Win10 client
with Sign/Seal flags disabled: 0x212fffff Provided by Secura)

**Step 4**. The server will receive the NetrServerAuthenticate request
and will compute the same request itself using it's known, good values.
If the results are good, the server will send the required info back to
the client. *\[Figure 1. Step 4.\]*

At this point the attempt to exploit the Zero Logon vulnerability is
under way. The above steps above will be looped through a certain number
of times to attempt to exploit the Zero Logon vulnerability. The actual
exploit occurs at Step 3 and 4, this where we're hoping for the Server
to a have the same computations as the client. This is where are
1-in-256 chance comes in.

**Step 5**. If the server calculates the same value, the client will
re-verify and once mutual agreement is confirmed, they will agree on a
session key. The session key will be used to encrypt communications
between the client and the server, which means authentication is
successful. *\[Figure 1. Step 5\]*

From there, normal RPC communications can occur.

**Sources -**

1\. Tom Tervoort of
Secura --- [https://www.secura.com/pathtoimg.php?id=2055](https://www.secura.com/pathtoimg.php?id=2055){.markup--anchor
.markup--p-anchor
data-href="https://www.secura.com/pathtoimg.php?id=2055"
rel="noopener ugc nofollow noopener" target="_blank"}

1\.
Microsoft --- [https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/7b9e31d1-670e-4fc5-ad54-9ffff50755f9](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/7b9e31d1-670e-4fc5-ad54-9ffff50755f9){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/7b9e31d1-670e-4fc5-ad54-9ffff50755f9"
rel="noopener ugc nofollow noopener" target="_blank"}

2\.
Microsoft --- [https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/3a9ed16f-8014-45ae-80af-c0ecb06e2db9](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/3a9ed16f-8014-45ae-80af-c0ecb06e2db9){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/3a9ed16f-8014-45ae-80af-c0ecb06e2db9"
rel="noopener ugc nofollow noopener" target="_blank"}

**Impacket Installation**

``` {#1e59 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
python3 -m pip install virtualenvpython3 -m virtualenv impacketEnvsource impacketEnv/bin/activatepip install git+https://github.com/SecureAuthCorp/impacket
```

[NetrServerAuthenticate3](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/3a9ed16f-8014-45ae-80af-c0ecb06e2db9){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/3a9ed16f-8014-45ae-80af-c0ecb06e2db9"
rel="noopener ugc nofollow noopener" target="_blank"} and
[NetrServerPasswordSet2](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81"
rel="noopener ugc nofollow noopener" target="_blank"}

[https://raw.githubusercontent.com/Sq00ky/Zero-Logon-Exploit/master/zeroLogon-NullPass.py](https://raw.githubusercontent.com/Sq00ky/Zero-Logon-Exploit/master/zeroLogon-NullPass.py){.markup--anchor
.markup--p-anchor
data-href="https://raw.githubusercontent.com/Sq00ky/Zero-Logon-Exploit/master/zeroLogon-NullPass.py"
rel="noopener ugc nofollow noopener" target="_blank"}

**Question 1**. What method will allow us to change Passwords over NRPC?

<figure id="2b13" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZjO6uVVWe7idAlnI.png"
class="graf-image" data-image-id="0*ZjO6uVVWe7idAlnI.png"
data-width="743" data-height="507" />
</figure>

[https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: NetrServerPasswordSet2***

**Question 2**. What are the required fields for the method per the
Microsoft Documentation?

> ***Answer:
> PrimaryName,AccountName,SecureChannelType,ComputerName,Authenticator,ReturnAuthenticator,ClearNewPassword***

### Task 4. Lab It Up {#05ee .graf .graf--h3 .graf-after--blockquote name="05ee"}

``` {#f9bc .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nmap -sV -sC 10.10.44.120
```

<figure id="4f3e" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Wls4QYAcaLIyHKTt.png"
class="graf-image" data-image-id="0*Wls4QYAcaLIyHKTt.png"
data-width="702" data-height="462" />
</figure>

**Question 1**. What is the NetBIOS name of the Domain Controller?

> ***Answer: DC01***

**Question 2**. What is the NetBIOS domain name of the network?

> ***Answer: hololive***

**Question 3**. What domain are you attacking?

> ***Answer: hololive.local***

**Question 4**. What is the Local Administrator's NTLM hash?

<figure id="66e5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7w5cE6eVqYS3u_kX.png"
class="graf-image" data-image-id="0*7w5cE6eVqYS3u_kX.png"
data-width="875" data-height="260" />
</figure>

<figure id="38d7" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*WktDhH8XP1H6xwV3.png"
class="graf-image" data-image-id="0*WktDhH8XP1H6xwV3.png"
data-width="799" data-height="284" />
</figure>

<figure id="e429" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*mqhG34d2UBlcSqFM.png"
class="graf-image" data-image-id="0*mqhG34d2UBlcSqFM.png"
data-width="875" data-height="394" />
</figure>

**Question 5.** How many Domain Admin accounts are there?

> ***Answer: 2***

**Question 6**. What is the root flag?

<figure id="0f23" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qh0Y-CAEL4HYvUYC.png"
class="graf-image" data-image-id="0*qh0Y-CAEL4HYvUYC.png"
data-width="875" data-height="143" />
</figure>

<figure id="300a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*uvK36kVEd2UqCJdC.png"
class="graf-image" data-image-id="0*uvK36kVEd2UqCJdC.png"
data-width="609" data-height="320" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#5292 .graf .graf--h3 .graf-after--figure name="5292"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#4f5a .graf .graf--h3 .graf-after--p name="4f5a"}

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
.h-card} on [September 2, 2024](https://medium.com/p/015cfe5f54b0).

[Canonical
link](https://medium.com/@bevijaygupta/zero-logon-tryhackme-writeup-015cfe5f54b0){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
