---
title: "Hardening Basics Part 1 TryHackme 14ff5672d3d6"
platform: Medium
original_file: 2024-09-06_Hardening-Basics-Part-1-TryHackme-14ff5672d3d6.md
---

# Hardening Basics Part 1 TryHackme 14ff5672d3d6

::: {}
# Hardening Basics Part 1 TryHackme {#hardening-basics-part-1-tryhackme .p-name}
:::

::: {.section .p-summary field="subtitle"}
Machine Credential spooky:tryhackme
:::

::::::: {.section .e-content field="body"}
:::::: {#0fdf .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Hardening Basics Part 1 TryHackme {#102f .graf .graf--h3 .graf--leading .graf--title name="102f"}

<figure id="73f5" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*6ltDU9ZU_1TGw_21.png"
class="graf-image" data-image-id="0*6ltDU9ZU_1TGw_21.png"
data-width="771" data-height="231" data-is-featured="true" />
</figure>

Machine Credential **spooky:tryhackme**

<figure id="f98c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zx0Jrv5vk7L1Lbby.png"
class="graf-image" data-image-id="0*zx0Jrv5vk7L1Lbby.png"
data-width="834" data-height="191" />
</figure>

### Task 11. Chapter 1 Quiz {#9117 .graf .graf--h3 .graf-after--figure name="9117"}

Question 1. What group are users automatically added to in Ubuntu?

> ***Answer: sudo***

Question 2. What would be the command to add an existing user, nick, to
the sudo group? You're running as root

> ***Answer: usermode -aG sudo nick***

Question 3.What command as a user can we enter to see what we are
allowed to execute with sudo?

> ***Answer: sudo -l***

Question 4. Where is the sudo policy file stored?

> ***Answer: /etc/sudoers***

Question 5. When in visudo and you see %\_\_\_\_, what does the % sign
indicate that you are dealing with?

> ***Answer: group***

Question 6. This Alias lets the user assign a name, like "ADMINS" to a
group of people

> ***Answer: user***

Question 7. Which Alias allows you to create a set of commands that you
can then assign to a User Alias?

> ***Answer: command***

Question 8. Yey/Ney --- emacs has a shell escape

> ***Answer: Yey***

Question 9. What is the minimum recommended password length set by NIST?

> ***Answer: 8***

Question 10. When using the pwhistory module, which file will contain
the previous passwords for the user?

> ***Answer: opasswd***

Question 11. What principle states that every user only has enough
access to do their daily duties and tasks

> ***Answer: principle of least privilege***

### Task 15. Basic Uncomplicated Firewall for Ubuntu & Chapter 2 Quiz {#9ba5 .graf .graf--h3 .graf-after--blockquote name="9ba5"}

Question 1. This type of Firewall typically has two NIC cards

> ***Answer: Network-Based***

Question 2. This type of Firewall is typically installed on a host
computer and rules apply to that specific host only

> ***Answer: Host-Based***

Question 3. Web Application Firewalls help add an extra layer of
security to your web servers. Where should these be installed?

> ***Answer: demilitarized zone***

Question 4. iptables is *not* the name of the Linux Firewall. What is
the framework that iptables allows us to interact with?

> ***Answer: netfilter***

Question 5. This 3 letter acronym is a set of rules that defines what
the Firewall should allow and what it should deny

> ***Answer: ACL***

Question 6. Which iptables option allows us to keep track of the
connection state?

> ***Answer: --- ctstate***

Question 7. Which iptable Chain is responsible for packets on the local
network that are being carried onwards?

> ***Answer: Forward***

Question 8. Which table mashes up the packets as they go through the
Firewall?

> ***Answer: mangle***

Question 9. What is the last rule that should be added to an access
control list?

> ***Answer: implicity deny***

### Promote and Collaborate on Cybersecurity Insights {#c77e .graf .graf--h3 .graf-after--blockquote name="c77e"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#9020 .graf .graf--h3 .graf-after--p name="9020"}

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
.h-card} on [September 6, 2024](https://medium.com/p/14ff5672d3d6).

[Canonical
link](https://medium.com/@bevijaygupta/hardening-basics-part-1-tryhackme-14ff5672d3d6){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
