::: {}
# Essential Linux Commands for DevOps Engineers: A Comprehensive Guide {#essential-linux-commands-for-devops-engineers-a-comprehensive-guide .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction
:::

::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#ca53 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Essential Linux Commands for DevOps Engineers: A Comprehensive Guide {#159f .graf .graf--h3 .graf--leading .graf--title name="159f"}

<figure id="834e" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*G7f1EOicmpAY4MEoAtY7Gw.png"
class="graf-image" data-image-id="1*G7f1EOicmpAY4MEoAtY7Gw.png"
data-width="2240" data-height="1260" data-is-featured="true" />
</figure>

**Introduction**

In the realm of DevOps, Linux commands are fundamental tools that
engineers use daily to manage and operate systems, automate tasks, and
deploy applications. Linux's powerful command-line interface (CLI)
allows DevOps professionals to efficiently handle a variety of tasks,
from monitoring system performance to managing files and directories.
Mastery of these commands not only improves efficiency but also enhances
troubleshooting skills and overall system management.

This blog will provide an in-depth exploration of essential Linux
commands that every DevOps engineer should be familiar with. We'll cover
commands related to file and directory management, system monitoring,
user management, and networking, offering practical examples and
explanations to help you leverage these commands in your daily
activities.
:::
::::
::::::

:::::: {#c295 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**1. File and Directory Management Commands**

**1.1.** **`ls`{.markup--code .markup--p-code}**

**Overview:** The `ls`{.markup--code .markup--p-code} command lists the
contents of a directory. It's one of the most commonly used commands for
navigating and inspecting file systems.

**Common Options:**

- [`-l`{.markup--code .markup--li-code}: Long format, which provides
  detailed information about each file (permissions, owner, size, and
  modification date).]{#655f}
- [`-a`{.markup--code .markup--li-code}: Includes hidden files (those
  starting with a dot).]{#37cb}
- [`-h`{.markup--code .markup--li-code}: Human-readable file sizes
  (e.g., KB, MB).]{#7fb1}

**Example Usage:**

``` {#c5a6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
ls -lah
```

This command lists all files and directories in the current directory in
a long format with human-readable sizes.

**1.2.** **`cd`{.markup--code .markup--p-code}**

**Overview:** The `cd`{.markup--code .markup--p-code} (change directory)
command allows you to navigate between directories.

**Example Usage:**

``` {#f583 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cd /var/log
```

This command changes the current directory to `/var/log`{.markup--code
.markup--p-code}.

**1.3.** **`pwd`{.markup--code .markup--p-code}**

**Overview:** The `pwd`{.markup--code .markup--p-code} (print working
directory) command displays the path of the current directory.

**Example Usage:**

``` {#d872 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
pwd
```

This command shows the absolute path of your current working directory.

**1.4.** **`cp`{.markup--code .markup--p-code}**

**Overview:** The `cp`{.markup--code .markup--p-code} command copies
files and directories from one location to another.

**Common Options:**

- [`-r`{.markup--code .markup--li-code}: Recursively copies
  directories.]{#6ae3}
- [`-i`{.markup--code .markup--li-code}: Prompts before overwriting
  files.]{#4920}

**Example Usage:**

``` {#7b17 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cp -r /source_directory /destination_directory
```

This command copies the entire contents of
`/source_directory`{.markup--code .markup--p-code} to
`/destination_directory`{.markup--code .markup--p-code}.

**1.5.** **`mv`{.markup--code .markup--p-code}**

**Overview:** The `mv`{.markup--code .markup--p-code} command moves or
renames files and directories.

**Example Usage:**

``` {#aaa4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mv oldname.txt newname.txt
```

This command renames `oldname.txt`{.markup--code .markup--p-code} to
`newname.txt`{.markup--code .markup--p-code}. To move a file:

``` {#6596 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
mv file.txt /new_directory/
```

This moves `file.txt`{.markup--code .markup--p-code} to
`/new_directory/`{.markup--code .markup--p-code}.

**1.6.** **`rm`{.markup--code .markup--p-code}**

**Overview:** The `rm`{.markup--code .markup--p-code} command removes
files and directories.

**Common Options:**

- [`-r`{.markup--code .markup--li-code}: Recursively removes directories
  and their contents.]{#e6a6}
- [`-f`{.markup--code .markup--li-code}: Forces removal without
  prompting.]{#0d0d}

**Example Usage:**

``` {#72b1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
rm -rf /directory_to_remove
```

This command forcefully removes `/directory_to_remove`{.markup--code
.markup--p-code} and its contents.
:::
::::
::::::

:::::: {#fd59 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**2. System Monitoring Commands**

**2.1.** **`top`{.markup--code .markup--p-code}**

**Overview:** The `top`{.markup--code .markup--p-code} command provides
a real-time view of system processes, including CPU and memory usage.

**Example Usage:**

``` {#e2f5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
top
```

This command opens an interactive display of current system processes
and resource usage.

**2.2.** **`htop`{.markup--code .markup--p-code}**

**Overview:** The `htop`{.markup--code .markup--p-code} command is an
enhanced version of `top`{.markup--code .markup--p-code}, offering a
more user-friendly interface with color-coded information and process
management features.

**Example Usage:**

``` {#d65c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
htop
```

This command opens the `htop`{.markup--code .markup--p-code} interface,
where you can scroll and filter processes interactively.

**2.3.** **`df`{.markup--code .markup--p-code}**

**Overview:** The `df`{.markup--code .markup--p-code} command shows disk
space usage for file systems.

**Common Options:**

- [`-h`{.markup--code .markup--li-code}: Human-readable format.]{#c17c}

**Example Usage:**

``` {#b26f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
df -h
```

This command displays disk space usage with human-readable sizes (e.g.,
GB, MB).

**2.4.** **`du`{.markup--code .markup--p-code}**

**Overview:** The `du`{.markup--code .markup--p-code} command estimates
disk space usage of files and directories.

**Common Options:**

- [`-h`{.markup--code .markup--li-code}: Human-readable format.]{#78c6}
- [`-s`{.markup--code .markup--li-code}: Summarizes total size.]{#dc0c}

**Example Usage:**

``` {#1d6c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
du -sh /directory
```

This command shows the total size of `/directory`{.markup--code
.markup--p-code} in a human-readable format.

**2.5.** **`free`{.markup--code .markup--p-code}**

**Overview:** The `free`{.markup--code .markup--p-code} command provides
information about system memory usage.

**Common Options:**

- [`-h`{.markup--code .markup--li-code}: Human-readable format.]{#5120}

**Example Usage:**

``` {#2bf6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
free -h
```

This command displays memory usage with human-readable sizes.

**2.6.** **`vmstat`{.markup--code .markup--p-code}**

**Overview:** The `vmstat`{.markup--code .markup--p-code} command
provides information about system processes, memory, paging, and block
I/O.

**Example Usage:**

``` {#b9e3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
vmstat 5
```

This command provides a snapshot of system performance every 5 seconds.
:::
::::
::::::

:::::: {#23e7 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**3. User Management Commands**

**3.1.** **`useradd`{.markup--code .markup--p-code}**

**Overview:** The `useradd`{.markup--code .markup--p-code} command
creates a new user account.

**Example Usage:**

``` {#31df .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
useradd newuser
```

This command creates a new user named `newuser`{.markup--code
.markup--p-code}.

**3.2.** **`passwd`{.markup--code .markup--p-code}**

**Overview:** The `passwd`{.markup--code .markup--p-code} command
changes a user's password.

**Example Usage:**

``` {#07fb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
passwd newuser
```

This command prompts you to set a new password for the user
`newuser`{.markup--code .markup--p-code}.

**3.3.** **`usermod`{.markup--code .markup--p-code}**

**Overview:** The `usermod`{.markup--code .markup--p-code} command
modifies user account properties.

**Common Options:**

- [`-aG`{.markup--code .markup--li-code}: Adds the user to a
  group.]{#bd9c}

**Example Usage:**

``` {#48e0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
usermod -aG sudo newuser
```

This command adds `newuser`{.markup--code .markup--p-code} to the
`sudo`{.markup--code .markup--p-code} group, granting administrative
privileges.

**3.4.** **`deluser`{.markup--code .markup--p-code}**

**Overview:** The `deluser`{.markup--code .markup--p-code} command
removes a user account.

**Example Usage:**

``` {#33ca .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
deluser newuser
```

This command deletes the user `newuser`{.markup--code .markup--p-code}.

**3.5.** **`groups`{.markup--code .markup--p-code}**

**Overview:** The `groups`{.markup--code .markup--p-code} command lists
the groups a user belongs to.

**Example Usage:**

``` {#c196 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
groups newuser
```

This command shows the groups that `newuser`{.markup--code
.markup--p-code} is a member of.
:::
::::
::::::

:::::: {#b18c .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**4. Networking Commands**

**4.1.** **`ping`{.markup--code .markup--p-code}**

**Overview:** The `ping`{.markup--code .markup--p-code} command tests
connectivity between the local machine and a remote host.

**Example Usage:**

``` {#b203 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ping google.com
```

This command sends ICMP packets to `google.com`{.markup--code
.markup--p-code} to check network connectivity.

**4.2.** **`ifconfig`{.markup--code .markup--p-code}**

**Overview:** The `ifconfig`{.markup--code .markup--p-code} command
displays or configures network interfaces. Note that
`ifconfig`{.markup--code .markup--p-code} is being replaced by
`ip`{.markup--code .markup--p-code} in many distributions.

**Example Usage:**

``` {#b12c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ifconfig
```

This command shows information about all network interfaces.

**4.3.** **`ip`{.markup--code .markup--p-code}**

**Overview:** The `ip`{.markup--code .markup--p-code} command is a more
modern replacement for `ifconfig`{.markup--code .markup--p-code}, used
to display and manage network interfaces, routes, and addresses.

**Example Usage:**

``` {#62fc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
ip addr show
```

This command displays IP addresses and network interface information.

**4.4.** **`netstat`{.markup--code .markup--p-code}**

**Overview:** The `netstat`{.markup--code .markup--p-code} command
displays network connections, routing tables, and interface statistics.

**Example Usage:**

``` {#6cbe .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
netstat -tuln
```

This command shows active network connections and listening ports.

**4.5.** **`ss`{.markup--code .markup--p-code}**

**Overview:** The `ss`{.markup--code .markup--p-code} command provides
detailed information about network sockets, and is often used as a
replacement for `netstat`{.markup--code .markup--p-code}.

**Example Usage:**

``` {#9cb2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ss -tuln
```

This command displays listening TCP and UDP sockets.

**4.6.** **`traceroute`{.markup--code .markup--p-code}**

**Overview:** The `traceroute`{.markup--code .markup--p-code} command
traces the route packets take to reach a destination.

**Example Usage:**

``` {#dbee .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
traceroute google.com
```

This command shows the path taken by packets to reach
`google.com`{.markup--code .markup--p-code}.

**4.7.** **`curl`{.markup--code .markup--p-code}**

**Overview:** The `curl`{.markup--code .markup--p-code} command
transfers data from or to a server using various protocols, including
HTTP, HTTPS, and FTP.

**Example Usage:**

``` {#e4d4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
curl -I https://www.example.com
```

This command retrieves the HTTP headers from
[`www.example.com`{.markup--code
.markup--p-code}](http://www.example.com.){.markup--anchor
.markup--p-anchor data-href="http://www.example.com." rel="noopener"
target="_blank"}[.](http://www.example.com.){.markup--anchor
.markup--p-anchor data-href="http://www.example.com." rel="noopener"
target="_blank"}
:::
::::
::::::

:::::: {#8bab .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**5. Process Management Commands**

**5.1.** **`ps`{.markup--code .markup--p-code}**

**Overview:** The `ps`{.markup--code .markup--p-code} command displays
information about active processes.

**Common Options:**

- [`-e`{.markup--code .markup--li-code}: Shows all processes.]{#f3df}
- [`-f`{.markup--code .markup--li-code}: Full format listing.]{#18df}

**Example Usage:**

``` {#bbed .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ps -ef
```

This command shows a detailed list of all running processes.

**5.2.** **`top`{.markup--code .markup--p-code}**

**Overview:** The `top`{.markup--code .markup--p-code} command provides
a real-time, interactive view of system processes.

**Example Usage:**

``` {#2fd3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
top
```

This command displays a dynamic view of system resource usage and
processes.

**5.3.** **`kill`{.markup--code .markup--p-code}**

**Overview:** The `kill`{.markup--code .markup--p-code} command sends a
signal to a process, typically used to terminate it.

**Example Usage:**

``` {#f14e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
kill -9 1234
```

This command forcefully terminates the process with PID 1234.

**5.4.** **`pkill`{.markup--code .markup--p-code}**

**Overview:** The `pkill`{.markup--code .markup--p-code} command sends a
signal to processes based on their name.

**Example Usage:**

``` {#e115 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
pkill firefox
```

This command sends a termination signal to all processes named
`firefox`{.markup--code .markup--p-code}.

**5.5.** **`killall`{.markup--code .markup--p-code}**

**Overview:** The `killall`{.markup--code .markup--p-code} command
terminates processes by name, similar to `pkill`{.markup--code
.markup--p-code}.

**Example Usage:**

``` {#a9c4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
killall firefox
```

This command terminates all instances of `firefox`{.markup--code
.markup--p-code}.
:::
::::
::::::

:::::: {#3bee .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**6. File Permissions and Ownership Commands**

**6.1.** **`chmod`{.markup--code .markup--p-code}**

**Overview:** The `chmod`{.markup--code .markup--p-code} command changes
file permissions.

**Common Options:**

- [`+x`{.markup--code .markup--li-code}: Adds execute
  permission.]{#d4db}
- [`-r`{.markup--code .markup--li-code}: Applies changes
  recursively.]{#5bc8}

**Example Usage:**

``` {#1dee .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
chmod 755 script.sh
```

This command sets the permissions of `script.sh`{.markup--code
.markup--p-code} to read, write, and execute for the owner, and read and
execute for others.

**6.2.** **`chown`{.markup--code .markup--p-code}**

**Overview:** The `chown`{.markup--code .markup--p-code} command changes
the owner and group of a file or directory.

**Example Usage:**

``` {#434c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
chown user:group file.txt
```

This command changes the owner of `file.txt`{.markup--code
.markup--p-code} to `user`{.markup--code .markup--p-code} and the group
to `group`{.markup--code .markup--p-code}.

**6.3.** **`chgrp`{.markup--code .markup--p-code}**

**Overview:** The `chgrp`{.markup--code .markup--p-code} command changes
the group ownership of a file or directory.

**Example Usage**

``` {#c067 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
chgrp group file.txt
```

This command changes the group ownership of `file.txt`{.markup--code
.markup--p-code} to `group`{.markup--code .markup--p-code}.
:::
::::
::::::

:::::: {#5dcb .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**Conclusion**

Mastering these basic Linux commands is crucial for DevOps engineers.
They form the backbone of daily operations, enabling efficient
management of files, processes, and systems. By becoming proficient with
these commands, you'll enhance your ability to troubleshoot issues,
automate tasks, and ensure the smooth operation of your environments.

In the fast-paced world of DevOps, being comfortable with these commands
will not only make your work more efficient but also help you adapt to
new challenges and technologies. Keep practicing and exploring these
commands to build a solid foundation for your DevOps career.

### Promote and Collaborate on Cybersecurity Insights {#3a8c .graf .graf--h3 .graf-after--p name="3a8c"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#2b4e .graf .graf--h3 .graf-after--p name="2b4e"}

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
:::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [August 22, 2024](https://medium.com/p/a20caa1cfe8b).

[Canonical
link](https://medium.com/@bevijaygupta/essential-linux-commands-for-devops-engineers-a-comprehensive-guide-a20caa1cfe8b){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
