::: {}
# MAL: Strings TryHackme Writeup {#mal-strings-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/malstrings
:::

::::::: {.section .e-content field="body"}
:::::: {#9091 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### MAL: Strings TryHackme Writeup {#ea0f .graf .graf--h3 .graf--leading .graf--title name="ea0f"}

<figure id="d85d" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*1pE8UEin3E2TpEqR.png"
class="graf-image" data-image-id="0*1pE8UEin3E2TpEqR.png"
data-width="443" data-height="227" />
</figure>

**Room link:**
[https://tryhackme.com/room/malstrings](https://tryhackme.com/room/malstrings){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malstrings"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Investigating "strings" within an application and why these values are
important!

> *Motivation:*

What you will learn after completing this Room:

- [String analysis]{#2051}
- [OSINT]{#07f4}
- [Static Analysis(Part of Malware Analysis)]{#280e}

### What are "strings"? {#c080 .graf .graf--h3 .graf-after--li name="c080"}

From a programming perspective, "strings" is the term given for data
handled by an application. At a broader view, these pieces of data are
used to store information such as text to numerical values.

For example, let's say we have an application such as a calculator. A
user will have to input two numerical values (e.g. 1 and 5) combined
with an operator (e.g. + or plus) addition in this case. These values
will be stored as "strings".

However "strings" can be stored within the application itself --- where
no input is necessary from the user. For example, using the example of
usernames and passwords is a great representation of the many types of
information that may be stored as a "string".

### Why are "strings" important? {#af7d .graf .graf--h3 .graf-after--p name="af7d"}

We're all security-minded people here and know that writing down
passwords isn't a very smart thing to do. However, developers are not
quite so likeminded and often leave credentials in applications which
are often essential i.e. An application that server needs to know the IP
address of it. Arguably, an IP address is trivial in comparison to the
sensitivity of a password --- but both would be stored as strings.

There are a plethora of examples of companies storing sensitive
information such as passwords within their applications. For example,
[Intellian](https://www.intelliantech.com/){.markup--anchor
.markup--p-anchor data-href="https://www.intelliantech.com/"
rel="noopener ugc nofollow noopener" target="_blank"}, a
satellite-communications focused company had the disclosure of their
**"Aptus Web 1.24"** application retaining a default passcode of
"12345678".

Illustrated below is an example of an Android Application containing
sensitive credentials within strings:

<figure id="7df3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2XNxCyay32Md5yit.png"
class="graf-image" data-image-id="0*2XNxCyay32Md5yit.png"
data-width="640" data-height="184" />
</figure>

(Credit: [Ezequiel.,
Skullarmy](https://www.blogger.com/profile/01349805697841422503){.markup--anchor
.markup--p-anchor
data-href="https://www.blogger.com/profile/01349805697841422503"
rel="noopener ugc nofollow noopener" target="_blank"})

Time for a bit of
[research](https://tryhackme.com/room/introtoresearch){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/introtoresearch"
rel="noopener ugc nofollow noopener" target="_blank"} to solve the
questions below!

**Question 1**. What is the **name of the account** that had the
passcode of "12345678" in the intellian example discussed above?

> ***Answer: intellian***

**Question 2.** What is the CVE entry disclosed by the company
"Teradata" in their "Viewpoint" Application that has a password within a
string?

> ***Answer: CVE-2019--6499***

**Question 3.** According to **OWASP's** list of **"Top Ten IoT"**
vulnerabilities, name the ranking this vulnerability would fall within,
represented as text.

> ***Answer: one***

### Task 2. Practical: Extracting "strings" From an Application {#869d .graf .graf--h3 .graf-after--blockquote name="869d"}

It is a little console program I have written in c++ for this example
that replicates a login prompt. We will be using Kali Linux. You can use
the

<figure id="91fc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7Zizl9Y6suMXVKgO.png"
class="graf-image" data-image-id="0*7Zizl9Y6suMXVKgO.png"
data-width="482" data-height="266" />
</figure>

**Question 1**. What is the correct username required by the
"LoginForm"?

> ***Answer: cmnatic***

**Question 2.** What is the required password to authenticate with?

> ***Answer: TryHackMeMerchWhen***

**Question 3.** What is the "hidden" THM{} flag?

<figure id="e3d7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fvxHufYcISOzrBfW.png"
class="graf-image" data-image-id="0*fvxHufYcISOzrBfW.png"
data-width="330" data-height="266" />
</figure>

### Task 3. Strings in the Context of Malware {#9b19 .graf .graf--h3 .graf-after--figure name="9b19"}

**Question 1**. What is the key term to describe a server that Botnets
recieve instructions from?

> ***Answer: Command and Control***

**Question 2.** Name the discussed example malware that uses "strings"
to store the bitcoin wallet addresses for payment

> ***Answer: Wannacry***

### Task 4. Practical: Finding Bitcoin Addresses in Ransomware (Deploy!) {#9ce3 .graf .graf--h3 .graf-after--blockquote name="9ce3"}

**What is Bitcoin?**

At a brief overview, Bitcoin is an "anonymous" online payment currency
in the sense that there is no direct attribution between the sender and
recipient. Authors of ransomware use this currency because of this
trait --- however, just because there is no attribution such as real
names like traditional payment methods, it is traceable by Law
Enforcement (albeit difficult).

For example, Wannacry uses Bitcoin as the payment method for the
decryption of files. Bitcoin uses virtual wallets, similar to a MAC
address of a network interface card.
[MuirlandOracle](https://tryhackme.com/p/MuirlandOracle){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/p/MuirlandOracle"
rel="noopener ugc nofollow noopener" target="_blank"} explains the
concept of MAC addresses in his [Introductory: Networking
room](https://tryhackme.com/room/introtonetworking){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/introtonetworking"
rel="noopener ugc nofollow noopener" target="_blank"}, these wallets
have addresses who are unique.

I.e. The Bitcoin address used by the authors of Wannacry was
[13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94](https://live.blockcypher.com/btc/address/13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94/){.markup--anchor
.markup--p-anchor
data-href="https://live.blockcypher.com/btc/address/13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="5a6a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FEWy-mopCk8pJDoW.png"
class="graf-image" data-image-id="0*FEWy-mopCk8pJDoW.png"
data-width="875" data-height="368" />
</figure>

In this case, the previously mentioned Bitcoin address used for Wannacry
has to-date received over 20BTC (Bitcoins) from victims, which
translates into over just over £158k (as of 06/04/2020).

You can use a website such as
[BlockCypher](https://live.blockcypher.com/){.markup--anchor
.markup--p-anchor data-href="https://live.blockcypher.com/"
rel="noopener ugc nofollow noopener" target="_blank"} to explore the
Bitcoin network and transactions between wallets.

<figure id="0b8c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pFTXg3Fgfdq4hSZA.png"
class="graf-image" data-image-id="0*pFTXg3Fgfdq4hSZA.png"
data-width="875" data-height="573" />
</figure>

Practical

You need to perform a few prerequisites before you can complete this
task, the steps are detailed below:

1.  [**Question 1**. List the number of total transactions that the
    Bitcoin wallet used by the "Wannacry" author(s)]{#6ac0}

Visit
[https://live.blockcypher.com/btc/address/13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94/](https://live.blockcypher.com/btc/address/13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94/){.markup--anchor
.markup--p-anchor
data-href="https://live.blockcypher.com/btc/address/13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="8f70" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jkNirY9hz9o9PwEz.png"
class="graf-image" data-image-id="0*jkNirY9hz9o9PwEz.png"
data-width="875" data-height="463" />
</figure>

> ***Answer: 142***

**Question 2.** What is the Bitcoin Address stored within
"ComplexCalculator.exe"

1.  [Deploy the VM attached to this room and wait a couple of minutes
    for it to deploy. In the interim, ensure you are connected to
    TryHackMe via
    [OpenVPN](https://tryhackme.com/room/openvpn){.markup--anchor
    .markup--li-anchor data-href="https://tryhackme.com/room/openvpn"
    rel="noopener ugc nofollow noopener" target="_blank"} to RDP into
    the machine using the details below, or alternatively, control the
    instance in-browser at the top of the web page!]{#bf22}
2.  [Open the "Sysinternals" folder located on the Desktop to
    proceed]{#d52c}

To login to the instance via RDP:

`10.10.217.102`{.markup--code .markup--p-code}

**Username:** analysis

**Password:** tryhackme

Domain: analysis-pc

Before using the "strings" tool provided with Sysinternals, we need to
accept the license agreement first. You can do this by launching the
executable through the command prompt and press "Agree" on the popup
dialogue box.

<figure id="7ba3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZAa3lLETu2YdR_Zo.png"
class="graf-image" data-image-id="0*ZAa3lLETu2YdR_Zo.png"
data-width="875" data-height="336" />
</figure>

With this license accepted, we can now use this tool to extract the
"strings" contained within the ComplexCalculatorv2.exe with the
following syntax:

``` {#bb96 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
strings.exe ComplexCalculatorv2.exe > strings.txt
```

<figure id="a9d7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*rqTijdn-UDQBxuaT.png"
class="graf-image" data-image-id="0*rqTijdn-UDQBxuaT.png"
data-width="773" data-height="126" />
</figure>

now open strings.txt in notepad

<figure id="54a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AAMghof9psq08N5g.png"
class="graf-image" data-image-id="0*AAMghof9psq08N5g.png"
data-width="375" data-height="395" />
</figure>

> ***Answer: 1LVB65imeojrgC3JPZGBwWhK1BdVZ2vYNC***

### Task 5. Summary {#7d56 .graf .graf--h3 .graf-after--blockquote name="7d56"}

**Question 1**. What is the name of the toolset provided by Microsoft
that allows you to extract the "strings" of an application?

> ***Answer: Sysinternals***

**Question 2.** What operator would you use to "pipe" or store the
output of the strings command?

> ***Answer: \>***

**Question 3.** What is the name of the currency that ransomware often
uses for payment?

> ***Answer: bitcoin***

### Promote and Collaborate on Cybersecurity Insights {#6962 .graf .graf--h3 .graf-after--blockquote name="6962"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#ed36 .graf .graf--h3 .graf-after--p name="ed36"}

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
.h-card} on [August 31, 2024](https://medium.com/p/b48371bc9370).

[Canonical
link](https://medium.com/@bevijaygupta/mal-strings-tryhackme-writeup-b48371bc9370){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
