---
title: "Password Reset Glitch Leads to Instant Account Takeover a4e67b667eaf"
platform: Medium
original_file: 2024-08-26_Password-Reset-Glitch-Leads-to-Instant-Account-Takeover-a4e67b667eaf.md
---

# Password Reset Glitch Leads to Instant Account Takeover a4e67b667eaf

::: {}
# Password Reset Glitch Leads to Instant Account Takeover {#password-reset-glitch-leads-to-instant-account-takeover .p-name}
:::

::: {.section .p-summary field="subtitle"}
I reported this bug in March 2023, but due to the team's delay, I
completely forgot about it. To my surprise, I discovered a week ago
that...
:::

::::::: {.section .e-content field="body"}
:::::: {#eddd .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Password Reset Glitch Leads to Instant Account Takeover {#c917 .graf .graf--h3 .graf--leading .graf--title name="c917"}

I reported this bug in March 2023, but due to the team's delay, I
completely forgot about it. To my surprise, I discovered a week ago that
they had actually responded about three months ago, in December 2023!

Anyway, let's discuss how I found this bug

let's assume our target gonna call it "target.com", after the subdomain
enum I decided to focus on the main app.

I opened my burp and started to interact with the app by doing the
normal actions like creating something or deleting something to save the
API requests to check it after that for any idor or any access control
bugs.\
started to check for any idor but unfortunately, it was secure.\
I took a break and after I came back, I tried to check some data I got
from my scripts like subdomains and screenshots but nothing interesting

I tried to read javascript files to check for any secrets or read the
API requests but found nothing :(

my bad luck

The last thing I was checking was the reset password page so let's dig
into it i went to the reset password page and tried to enter my email
address and reset it until here there is no problem

<figure id="3096" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yQuuNdHltQDFr2_f.png"
class="graf-image" data-image-id="0*yQuuNdHltQDFr2_f.png"
data-width="875" data-height="438" />
</figure>

The email address reset password

usually, I open the console and the local storage and cookie to check
the data saved into it so I opened it and found some field called
user_email

<figure id="5335" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*p0u3HZLqkSGRl6zT.png"
class="graf-image" data-image-id="0*p0u3HZLqkSGRl6zT.png"
data-width="875" data-height="491" />
</figure>

and the value of it was my email I reset the password for it so I tried
to change it to check if the value of the email in the page was taken
from this local storage field and when I changed it changed in the page.

<figure id="a542" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oa_irQGRV2hl09Lb.png"
class="graf-image" data-image-id="0*oa_irQGRV2hl09Lb.png"
data-width="875" data-height="439" />
</figure>

after I changed the local storage to the attacker's mail

so I thought it might be trying to inject anything but after one minute
I told myself even if I injected anything it's self so I clicked on the
button to resend the email with dead hope but guess what? I got the
reset link for the victim mail to the new mail I put in the local
storage!!!!!!!!!!!!!!!

So let's reproduce the bug:

1.  [go to the reset password link and put the victim's mail]{#38d8}
2.  [after the first link goes to the victim's mail open the console and
    change the user_email to the attacker's mail]{#8875}
3.  [reload and resend the mail]{#2a8b}
4.  [open the attacker's mail and use the link to reset the victim's
    password]{#c33e}

<figure id="ffe5" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*O5Zg9oXd_IBFtrSh.png"
class="graf-image" data-image-id="0*O5Zg9oXd_IBFtrSh.png"
data-width="875" data-height="128" />
</figure>

So let's talk about this weird behavior :

the app when you make the reset password action returns the user data in
some field called token in the local storage so when the user hits the
resend email it should send the email to the email stored in that token
but what the app does is get the email value from the user_email and
send it to the user id stored in the token.

### Promote and Collaborate on Cybersecurity Insights {#7e3d .graf .graf--h3 .graf-after--p name="7e3d"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#9f8b .graf .graf--h3 .graf-after--p name="9f8b"}

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
.h-card} on [August 26, 2024](https://medium.com/p/a4e67b667eaf).

[Canonical
link](https://medium.com/@bevijaygupta/password-reset-glitch-leads-to-instant-account-takeover-a4e67b667eaf){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
