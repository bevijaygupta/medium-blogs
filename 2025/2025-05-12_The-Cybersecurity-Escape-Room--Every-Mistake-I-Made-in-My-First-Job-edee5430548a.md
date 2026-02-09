---
title: "The Cybersecurity Escape Room  Every Mistake I Made in My First Job edee5430548a"
platform: Medium
original_file: 2025-05-12_The-Cybersecurity-Escape-Room--Every-Mistake-I-Made-in-My-First-Job-edee5430548a.md
---

# The Cybersecurity Escape Room  Every Mistake I Made in My First Job edee5430548a

::: {}
# The Cybersecurity Escape Room: Every Mistake I Made in My First Job {#the-cybersecurity-escape-room-every-mistake-i-made-in-my-first-job .p-name}
:::

::: {.section .p-summary field="subtitle"}
Let me paint you a picture: a bright-eyed, bushy-tailed cybersecurity
enthusiast lands their dream job straight out of college. Full of...
:::

::::::: {.section .e-content field="body"}
:::::: {#84bc .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### **The Cybersecurity Escape Room: Every Mistake I Made in My First Job** {#b252 .graf .graf--h3 .graf--leading .graf--title name="b252"}

<figure id="aa82" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*gEiWAu_Kq2y0w8R_.png"
class="graf-image" data-image-id="0*gEiWAu_Kq2y0w8R_.png"
data-width="2000" data-height="1125" data-is-featured="true" />
</figure>

Let me paint you a picture: a bright-eyed, bushy-tailed cybersecurity
enthusiast lands their dream job straight out of college. Full of
excitement, a hint of arrogance, and precisely 0% idea of what they're
doing in the real world. That enthusiast? Me. Welcome to my TED Talk (or
rather, this blog): *The* [*Cybersecurity Escape
Room*](https://vijaykumargupta.in/category/cybersecurity/){.markup--anchor
.markup--p-anchor
data-href="https://vijaykumargupta.in/category/cybersecurity/"
rel="noopener" target="_blank"}*: Every Mistake I Made in My First Job.*

If you're entering cybersecurity and think you're going to be the hacker
version of James Bond from day one --- spoiler alert --- you're not.
You're more like Mr. Bean with a keyboard.

### Mistake #1: Believing Certifications Were Enough {#7497 .graf .graf--h3 .graf-after--p name="7497"}

I had four shiny certifications --- Security+, CEH, CISSP (don't ask how
I passed it), and a random Python course I barely finished. I walked in
thinking I was ready to decrypt the world. Day one, my manager asked me
to do a packet capture analysis. I stared at Wireshark like it had just
insulted my ancestors.

I thought I'd be performing penetration tests like in the
movies --- "I'm in" --- but instead, I was stuck trying to figure out
why the printer was sending traffic to Russia.

Lesson: **Certs are cool. Experience is cooler.**

### Mistake #2: The "Did You Try Turning It Off and On Again?" Era {#1c9d .graf .graf--h3 .graf-after--p name="1c9d"}

At some point, someone decided that I should help out the IT support
desk because "cybersecurity and IT are kind of the same, right?" Wrong.
That's like saying a dentist and a heart surgeon both work in
healthcare, so hey, hand them a scalpel.

So there I was, rebooting routers and telling people their passwords
couldn't be "123456." One user called me crying because I disabled her
account after three failed logins. Turns out, I had locked out the
*entire finance department* by mistake.

Lesson: **Don't mess with Active Directory unless you have a will
ready.**

### Mistake #3: Thinking Google Dorks Were Real People {#95da .graf .graf--h3 .graf-after--p name="95da"}

During one of our team discussions, someone said, "We need to use Google
Dorks to find exposed endpoints." I nodded confidently and immediately
Googled, "What is a Google Dork and how do I hire one?" I imagined some
guy in glasses and suspenders who just *knew* how to break into
databases.

A few hours later, I learned what Google Dorking was --- and let's just
say I accidentally found a public admin login page... for our own
company's test server.

Lesson: **You're the dork. Google just helps.**

### Mistake #4: Forgetting to Change Default Passwords {#952f .graf .graf--h3 .graf-after--p name="952f"}

It was a classic rookie mistake. We were setting up some IoT security
cameras around the office, and I didn't change the default login. One
week later, someone found the live feed through Shodan. Thankfully, it
was just the intern who found it. Unfortunately, she streamed the
footage onto the break room TV "for awareness."

Lesson: **Admin:admin is not a secure password.**

### Mistake #5: Falling for a Phishing Email (Yes, Me.) {#08bb .graf .graf--h3 .graf-after--p name="08bb"}

Irony, thy name is phishing. I had just given a workshop to junior staff
on identifying phishing attempts. Literally the next day, I clicked on a
fake FedEx email.

The worst part? It didn't even look convincing. It said, "Your Packaj is
in Transit" and had Comic Sans font. I clicked it because I was
expecting a delivery of a USB Rubber Ducky. Which, ironically, is now
what I call myself in moments of shame.

Lesson: **Always hover before you click. Especially when the email says
"CONGRATULATIONS!1!1!"**

### Mistake #6: Playing Hacker in Production {#b2a3 .graf .graf--h3 .graf-after--p name="b2a3"}

I had just learned how to use Metasploit. So naturally, I wanted to test
it. Did I use the lab environment? No. I tested it in production.

I ended up crashing our internal HR system. Everyone's leave balance
disappeared. The HR head walked over to my desk and said, "So... we all
got unlimited leave now?"

Lesson: **There's a reason the word "test" exists. Use it.**

### Mistake #7: Logging Everything... Including My Embarrassing Search History {#8b11 .graf .graf--h3 .graf-after--p name="8b11"}

I proudly set up logging for our network, ensuring we had full
visibility. What I forgot was to exclude personal machines (like mine).
One day, during an audit, my manager pulled up Kibana and said, "So, you
were searching 'How to explain cybersecurity to your mom' at 3:47 PM?"

To make things worse, the very next search was "What does SOC stand for
again?"

Lesson: **Audit logs are forever. So is shame.**

### Mistake #8: Overcomplicating Everything {#5d64 .graf .graf--h3 .graf-after--p name="5d64"}

I thought being a pro meant deploying complex tools and setting up
six-layer firewalls with honey pots, deception tech, and a touch of
voodoo. It took a grizzled old network admin to slap some wisdom into
me: "If you don't understand it, don't deploy it."

I had created such a complicated SIEM rule that even the rule didn't
know what it was detecting. It just triggered alerts like a confused
puppy every 2 minutes.

Lesson: **KISS --- Keep It Simple, Stupid.**

### Mistake #9: Trying to Impress with Jargon {#b037 .graf .graf--h3 .graf-after--p name="b037"}

During my first presentation to senior management, I said, "The endpoint
telemetry logs indicated anomalous lateral movement likely stemming from
a persistent threat actor."

My boss leaned forward and asked, "So... is that good or bad?"

I blinked. "Uh. Bad?"

He nodded and said, "Next time, just say the bad guys are inside."

Lesson: **Speak human. No one wants a jargon bot.**

### Mistake #10: Not Asking for Help {#fd2a .graf .graf--h3 .graf-after--p name="fd2a"}

This was the biggest one. I thought asking questions would make me look
dumb. So I ended up doing dumb things quietly, which is actually worse.

Eventually, a senior colleague noticed and pulled me aside. "No one
expects you to know everything," he said. "Just don't break the firewall
again."

Lesson: **Ask. Learn. Don't guess on a production firewall.**

### Bonus Mistake: Bragging Online {#c2d1 .graf .graf--h3 .graf-after--p name="c2d1"}

After three months, I posted on LinkedIn: "Loving the blue team life!
Just helped mitigate a critical vulnerability." What I didn't know was
that the vulnerability hadn't been disclosed publicly yet. Our CISO
commented, "Please remove this post."

Lesson: **Cybersecurity ≠ oversharing.**

### Conclusion: Escape Room Completed (Kind Of) {#e6d5 .graf .graf--h3 .graf-after--p name="e6d5"}

Looking back, it really did feel like a cybersecurity escape room. Every
mistake was a puzzle, every blunder a trapdoor. I made it
through --- barely --- and I learned a ton. Mostly what *not* to do.

If you're starting out, know this: making mistakes is okay. What's not
okay is pretending you didn't. Own them. Laugh at them. Share
them --- preferably *after* the damage has been fixed.

Now excuse me while I go rotate my passwords, patch my home router, and
double-check that I didn't accidentally forward our threat intel reports
to my mom.

Stay safe out there. And don't click the "Packaj" email.

### Promote and Collaborate on Cybersecurity Insights {#ec3f .graf .graf--h3 .graf-after--p name="ec3f"}

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
.h-card} on [May 12, 2025](https://medium.com/p/edee5430548a).

[Canonical
link](https://medium.com/@bevijaygupta/the-cybersecurity-escape-room-every-mistake-i-made-in-my-first-job-edee5430548a){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
