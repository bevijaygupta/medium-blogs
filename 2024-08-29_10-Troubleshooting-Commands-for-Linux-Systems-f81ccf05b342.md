::: {}
# 10 Troubleshooting Commands for Linux Systems {#troubleshooting-commands-for-linux-systems .p-name}
:::

::: {.section .p-summary field="subtitle"}
Linux systems are known for their stability and reliability, but like
any operating system, they can run into issues. Troubleshooting in...
:::

::::::: {.section .e-content field="body"}
:::::: {#6e67 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 10 Troubleshooting Commands for Linux Systems {#1d2a .graf .graf--h3 .graf--leading .graf--title name="1d2a"}

<figure id="5e2c" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*45PoKVVqJZ3VsyGBnBE6uQ.jpeg"
class="graf-image" data-image-id="1*45PoKVVqJZ3VsyGBnBE6uQ.jpeg"
data-width="6000" data-height="4000" />
</figure>

Linux systems are known for their stability and reliability, but like
any operating system, they can run into issues. Troubleshooting in Linux
often requires using the command line, which offers powerful tools for
diagnosing and fixing problems. This blog will walk you through ten
essential troubleshooting commands for Linux systems, along with
alternative methods to accomplish the same tasks.

### 1. Understanding the Linux Command Line {#abdd .graf .graf--h3 .graf-after--p name="abdd"}

The command line is the heart of Linux troubleshooting. Unlike graphical
interfaces, the command line allows you to execute commands directly,
providing greater control over the system. Familiarity with these
commands can make the difference between quickly resolving an issue and
spending hours troubleshooting.

### 2. Top 10 Troubleshooting Commands {#4f0d .graf .graf--h3 .graf-after--p name="4f0d"}

#### 1. `dmesg`{.markup--code .markup--h4-code} - Diagnosing Hardware and Kernel Issues {#cdad .graf .graf--h4 .graf-after--h3 name="cdad"}

The `dmesg`{.markup--code .markup--p-code} command is used to examine
messages from the kernel ring buffer. This buffer contains information
about hardware and kernel-related events, such as device recognition,
driver errors, and more.

**Usage:**

``` {#6b56 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
dmesg | less
```

This command displays the kernel messages with pagination, making it
easier to scroll through the output.

**Alternative:** You can also view the kernel messages in real-time
with:

``` {#fac0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
tail -f /var/log/kern.log
```

This command continuously monitors the kernel log file for new entries.

#### 2. `top`{.markup--code .markup--h4-code} - Monitoring System Performance {#7fd3 .graf .graf--h4 .graf-after--p name="7fd3"}

The `top`{.markup--code .markup--p-code} command provides a real-time
view of system processes, including CPU usage, memory consumption, and
more. It's an essential tool for identifying processes that are
consuming excessive resources.

**Usage:**

``` {#9125 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
top
```

Once `top`{.markup--code .markup--p-code} is running, you can sort the
output by CPU, memory usage, and more by pressing specific keys
(`P`{.markup--code .markup--p-code} for CPU, `M`{.markup--code
.markup--p-code} for memory).

**Alternative:** An alternative to `top`{.markup--code .markup--p-code}
is the `htop`{.markup--code .markup--p-code} command, which offers a
more user-friendly interface with color-coded output and interactive
process management.

**Install htop:**

``` {#fc1d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
sudo apt-get install htop
htop
```

#### 3. `ps`{.markup--code .markup--h4-code} - Process Management {#819e .graf .graf--h4 .graf-after--pre name="819e"}

The `ps`{.markup--code .markup--p-code} command is used to list running
processes. It provides detailed information about each process, such as
the process ID (PID), the user who owns the process, and the command
that started it.

**Usage:**

``` {#5194 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
ps aux | grep process_name
```

This command filters the process list to show only those processes that
match `process_name`{.markup--code .markup--p-code}.

**Alternative:** For a dynamic view similar to `top`{.markup--code
.markup--p-code}, you can use `pgrep`{.markup--code .markup--p-code} to
find PIDs by name and `pkill`{.markup--code .markup--p-code} to
terminate them:

``` {#873b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
pgrep process_name
pkill process_name
```

#### 4. `netstat`{.markup--code .markup--h4-code} - Network Diagnostics {#3f2c .graf .graf--h4 .graf-after--pre name="3f2c"}

The `netstat`{.markup--code .markup--p-code} command provides
information about network connections, routing tables, interface
statistics, and more. It's invaluable for diagnosing network-related
issues.

**Usage:**

``` {#5c0b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
netstat -tuln
```

This command lists all listening ports and their associated services.

**Alternative:** An alternative to `netstat`{.markup--code
.markup--p-code} is the `ss`{.markup--code .markup--p-code} command,
which offers more detailed and faster network information:

``` {#42fc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ss -tuln
```

#### 5. `ping`{.markup--code .markup--h4-code} - Network Connectivity Testing {#9264 .graf .graf--h4 .graf-after--pre name="9264"}

The `ping`{.markup--code .markup--p-code} command is used to test the
reachability of a host on a network. It sends ICMP echo request packets
and waits for a reply, making it useful for diagnosing network
connectivity issues.

**Usage:**

``` {#dbfa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="r"}
ping -c 4 google.com
```

This command sends four ping requests to `google.com`{.markup--code
.markup--p-code}.

**Alternative:** An alternative to `ping`{.markup--code .markup--p-code}
for testing connectivity and diagnosing DNS issues is the
`mtr`{.markup--code .markup--p-code} command, which combines the
functionality of `traceroute`{.markup--code .markup--p-code} and
`ping`{.markup--code .markup--p-code}.

**Install mtr:**

``` {#f640 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
sudo apt-get install mtr
mtr google.com
```

#### 6. `traceroute`{.markup--code .markup--h4-code} - Tracing Network Paths {#fbf6 .graf .graf--h4 .graf-after--pre name="fbf6"}

The `traceroute`{.markup--code .markup--p-code} command shows the path
packets take to reach a network host. This can help identify where
network delays or failures are occurring.

**Usage:**

``` {#7cff .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
traceroute google.com
```

This command displays each hop along the path to
`google.com`{.markup--code .markup--p-code}.

**Alternative:** The `mtr`{.markup--code .markup--p-code} command
mentioned earlier is a real-time alternative to
`traceroute`{.markup--code .markup--p-code} and can be used for
continuous monitoring:

``` {#d222 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
mtr google.com
```

#### 7. `df`{.markup--code .markup--h4-code} - Disk Space Usage {#87ce .graf .graf--h4 .graf-after--pre name="87ce"}

The `df`{.markup--code .markup--p-code} command displays the amount of
disk space used and available on filesystems. It's crucial for
diagnosing issues related to storage.

**Usage:**

``` {#4610 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
df -h
```

The `-h`{.markup--code .markup--p-code} option makes the output
human-readable by showing sizes in KB, MB, or GB.

**Alternative:** For a more detailed view, including file and directory
usage, use the `ncdu`{.markup--code .markup--p-code} (NCurses Disk
Usage) command:

``` {#efa9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
sudo apt-get install ncdu
ncdu /
```

#### 8. `du`{.markup--code .markup--h4-code} - Directory Disk Usage {#24a1 .graf .graf--h4 .graf-after--pre name="24a1"}

The `du`{.markup--code .markup--p-code} command estimates file space
usage. It's useful for identifying large files or directories that are
consuming excessive disk space.

**Usage:**

``` {#9b8b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
du -sh /path/to/directory
```

This command displays the size of the specified directory.

**Alternative:** The `ncdu`{.markup--code .markup--p-code} command, as
mentioned earlier, provides a more interactive way to analyze disk usage
across directories.

#### 9. `free`{.markup--code .markup--h4-code} - Memory Usage {#69d5 .graf .graf--h4 .graf-after--p name="69d5"}

The `free`{.markup--code .markup--p-code} command provides information
about the system's memory usage, including total, used, and available
memory. It's essential for diagnosing memory-related issues.

**Usage:**

``` {#1600 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
free -h
```

The `-h`{.markup--code .markup--p-code} option makes the output
human-readable.

**Alternative:** For real-time memory monitoring, use the
`vmstat`{.markup--code .markup--p-code} command:

``` {#4b33 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
vmstat 2
```

This command updates memory, CPU, and I/O statistics every 2 seconds.

#### 10. `journalctl`{.markup--code .markup--h4-code} - System Logs {#7b52 .graf .graf--h4 .graf-after--p name="7b52"}

The `journalctl`{.markup--code .markup--p-code} command is used to view
logs collected by the systemd journal. It's an all-encompassing tool for
viewing system logs, service logs, boot logs, and more.

**Usage:**

``` {#bb6c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
journalctl -xe
```

This command shows the most recent logs and highlights errors.

**Alternative:** You can also view specific service logs by specifying
the service name:

``` {#9144 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
journalctl -u ssh
```

This command shows logs related to the SSH service.

### 3. Alternatives to Command Line Troubleshooting {#2103 .graf .graf--h3 .graf-after--p name="2103"}

While the command line is powerful, some users may prefer graphical
tools or other alternatives:

- [**System Monitor (GUI):** Provides a graphical interface for
  monitoring system resources, similar to `top`{.markup--code
  .markup--li-code}.]{#8b83}
- [**GParted (GUI):** A disk partition manager that offers a graphical
  alternative to `df`{.markup--code .markup--li-code} and
  `du`{.markup--code .markup--li-code}.]{#c9ad}
- [**Wireshark (GUI):** A network protocol analyzer that provides a
  graphical alternative to `netstat`{.markup--code .markup--li-code} and
  `traceroute`{.markup--code .markup--li-code}.]{#a066}

### 4. Best Practices for Troubleshooting in Linux {#07f1 .graf .graf--h3 .graf-after--li name="07f1"}

1.  [**Keep Logs:** Always check system logs (`journalctl`{.markup--code
    .markup--li-code}, `/var/log/`{.markup--code .markup--li-code}) for
    error messages.]{#7538}
2.  [**Start Simple:** Begin with basic commands like
    `ping`{.markup--code .markup--li-code} or `df`{.markup--code
    .markup--li-code} before moving on to more complex tools.]{#750b}
3.  [**Use Man Pages:** Use `man command`{.markup--code
    .markup--li-code} to access the manual for any command to understand
    its options and usage.]{#d0d9}
4.  [**Document Solutions:** Maintain a log of issues and solutions for
    future reference.]{#e41b}

### 5. Conclusion {#6c29 .graf .graf--h3 .graf-after--li name="6c29"}

Troubleshooting in Linux is both an art and a science. The command line
offers a robust set of tools that, when used correctly, can quickly
diagnose and fix system issues. Whether you're monitoring system
performance, checking network connectivity, or managing disk space,
these commands form the backbone of Linux system administration. While
alternative methods and graphical tools are available, mastering these
commands will make you a more efficient and effective troubleshooter.

By understanding and practicing these 10 essential troubleshooting
commands, you'll be well-equipped to handle almost any issue that arises
on a Linux system. Remember, the key to successful troubleshooting is a
methodical approach, a solid understanding of the tools at your
disposal, and a commitment to learning and improvement.

### Promote and Collaborate on Cybersecurity Insights {#07fe .graf .graf--h3 .graf-after--p name="07fe"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#11ff .graf .graf--h3 .graf-after--p name="11ff"}

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
.h-card} on [August 29, 2024](https://medium.com/p/f81ccf05b342).

[Canonical
link](https://medium.com/@bevijaygupta/10-troubleshooting-commands-for-linux-systems-f81ccf05b342){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
