---
title: "When You Can Just  Change Your Email  No OTP  No Questions Asked  Just Vibes  fc89db324366"
platform: Medium
original_file: 2025-07-06_When-You-Can-Just--Change-Your-Email--No-OTP--No-Questions-Asked--Just-Vibes--fc89db324366.md
---

# When You Can Just  Change Your Email  No OTP  No Questions Asked  Just Vibes  fc89db324366

::: {}
# When You Can Just... Change Your Email. No OTP. No Questions Asked. Just Vibes. {#when-you-can-just-change-your-email.-no-otp.-no-questions-asked.-just-vibes. .p-name}
:::

::: {.section .p-summary field="subtitle"}
"Security is like insurance --- useless until it's not."  This story
proves just that. Buckle up, because I'm about to take you on a
journey...
:::

::::::: {.section .e-content field="body"}
:::::: {#1716 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### When You Can Just... Change Your Email. No OTP. No Questions Asked. Just Vibes. {#3038 .graf .graf--h3 .graf--leading .graf--title name="3038"}

> "Security is like insurance --- useless until it's not."*\
>  This story proves just that. Buckle up, because I'm about to take you
> on a journey into the chaotic world of web app logic fails, where I
> stumbled upon an oversight so wild, it made me double-check if I was
> dreaming.*

### The Innocent Beginning {#7222 .graf .graf--h3 .graf-after--blockquote name="7222"}

So there I was, casually poking around in a web application. As someone
who breathes HTTP requests and thinks Burp Suite is a leisure tool, I
often find myself dissecting how websites behave under the hood. Call it
curiosity or just a habit of peeling off layers until I hit something
juicy.

This particular app was nothing out of the ordinary --- a standard
consumer-facing platform with basic login features, account settings,
and all the jazz you'd expect. I logged in, sniffed around, and then
decided to check how the profile update functionality worked.

What happened next left me stunned.

### Just... Change the Email? {#ced3 .graf .graf--h3 .graf-after--p name="ced3"}

Like any curious hacker (or ethical security researcher, if we're being
formal), I intercepted the API request sent when updating the profile.

The endpoint in question?

``` {#038e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
PUT /api/v1.0.0/Consumer/updConsumerProfile
```

Totally routine. I assumed it would be locked tight when it came to
sensitive data like email addresses.

But no.

All I had to do was change the value of a field called
`p_regemail`{.markup--code .markup--p-code}, hit send---and bam. I got a
`200 OK`{.markup--code .markup--p-code}. No OTP. No confirmation link.
No password re-authentication. Just vibes. The server responded like a
chill bartender: "Cool, thanks for the update."

### No OTP? No Warning? No Common Sense? {#1833 .graf .graf--h3 .graf-after--p name="1833"}

In case you're not a security nerd, let me break down what this means:

If someone has access to your **session** --- say through a stolen
cookie, XSS vulnerability, or you left your account open on a public
computer --- they could silently change your email address. Once that's
done, your account is as good as gone.

No alert.\
 No verification.\
 No rollback option.\
 Nothing.

In security speak, this is a **Business Logic Flaw**. It's not a bug in
the code itself, but in how the system is designed. A logic flaw allows
malicious actors to misuse legitimate features in unintended ways.

### The Technical Breakdown {#f8d4 .graf .graf--h3 .graf-after--p name="f8d4"}

Let's dive a bit deeper for the technically inclined folks.

### 🔍 Endpoint {#e7e5 .graf .graf--h3 .graf-after--p name="e7e5"}

`PUT /api/v1.0.0/Consumer/updConsumerProfile`{.markup--code
.markup--p-code}

### 🔧 Vulnerable Field {#648a .graf .graf--h3 .graf-after--p name="648a"}

`p_regemail`{.markup--code .markup--p-code}

### ⚠️ Bug Type {#8a9e .graf .graf--h3 .graf-after--p name="8a9e"}

**Business Logic Flaw** --- Unverified sensitive action

### 💥 Impact {#a619 .graf .graf--h3 .graf-after--p name="a619"}

**Silent Account Takeover**

If an attacker hijacks a session token (even temporarily), they can:

- [Change the victim's email address.]{#4298}
- [Lock the user out of recovery options.]{#3288}
- [Gain full control of the account with no trace.]{#63c3}

### 🧪 Reproduction Steps {#03dc .graf .graf--h3 .graf-after--li name="03dc"}

It took less than 2 minutes to confirm the flaw:

1.  [**Log into your account.**]{#1176}
2.  [**Intercept the update profile request** using a proxy tool like
    Burp Suite or Fiddler.]{#cc62}
3.  [**Modify the** **`p_regemail`{.markup--code .markup--li-code}**
    **field** in the request body to a new email address.]{#69d3}
4.  [**Forward the request.**]{#cd63}
5.  [**Boom: 200 OK. Email changed.**]{#ce13}

No email sent.\
 No confirmation needed.\
 Just vibes.

### Why This is Dangerous {#06fe .graf .graf--h3 .graf-after--p name="06fe"}

Let's say you use this app regularly. One day, someone steals your
session cookie (e.g., through a phishing attack or a vulnerability in
another site). They log in *as you* --- but silently.

They then change your email address using this API. Since there's no
verification involved, the system accepts it happily. Suddenly, you
can't recover your account because the "Forgot Password" link goes to a
new email. You don't even know your email has changed unless you check
it manually.

Your digital identity = hijacked.

This isn't just a theoretical attack --- it's a real-world scenario that
has led to credential theft, financial fraud, and user privacy breaches.

### No Bounty, But A Moral Victory {#f62d .graf .graf--h3 .graf-after--p name="f62d"}

Now, I believe in responsible disclosure.

So, like any decent human with a conscience and a caffeine addiction, I
documented the issue and emailed the company.

They responded fairly quickly, which was nice.

Their response went something like this:

> *"Thank you for your report. We've forwarded this to our development
> team. While we currently do not operate a public bug bounty program,
> we appreciate your help in making our platform more secure."*

No reward, no swag, not even a sticker. But that's okay.

Because here's the deal --- **security wins are still wins**, even
without a PayPal notification.

### What Should Have Happened Instead {#7c45 .graf .graf--h3 .graf-after--p name="7c45"}

Let's rewrite the logic the right way:

1.  [**User initiates email change.**]{#35f8}
2.  [**System sends confirmation to the OLD email.**]{#71c1}
3.  [**System sends verification to the NEW email.**]{#da81}
4.  [**Only upon verifying both sides, the email is updated.**]{#9695}
5.  [**Log the action. Notify the user via both email and in-app
    notification.**]{#5ede}

Even better?

- [Require **password re-authentication** before making sensitive
  changes.]{#f976}
- [Detect and alert on sudden changes in credentials.]{#e6c9}
- [Have some form of **audit logging** or **rate limiting** for profile
  updates.]{#4279}

Basically, **don't just let users change their identities like they're
changing Spotify playlists.**

### The Bigger Problem: Blind Trust in Users {#74ad .graf .graf--h3 .graf-after--p name="74ad"}

This bug is a textbook example of what happens when devs trust users a
little *too* much.

And let me be clear --- developers are not stupid. They're overworked,
underpaid, juggling deadlines, and battling technical debt. But
somewhere along the line, basic security hygiene is getting skipped.
Especially when it comes to **business logic**.

No matter how secure your backend is, if your **logic is flawed**, the
whole house falls apart.

### What Developers and Teams Can Learn {#15ff .graf .graf--h3 .graf-after--p name="15ff"}

Let's break this into clear takeaways:

### 🔒 1. Treat Profile Changes Like Password Resets {#879d .graf .graf--h3 .graf-after--p name="879d"}

Changing an email is as sensitive as changing a password. Maybe even
*more* dangerous. Treat it with the same level of scrutiny.

### 🛂 2. Verify and Authenticate {#36b2 .graf .graf--h3 .graf-after--p name="36b2"}

Re-authenticate users before performing critical actions like:

- [Email change]{#661c}
- [Password reset]{#239e}
- [Payment method updates]{#139a}
- [Role changes]{#403c}

### 📣 3. Notify the User {#923b .graf .graf--h3 .graf-after--li name="923b"}

Transparency builds trust. Notify users when their credentials change.
Let them know if an action is performed from a new IP, location, or
device.

### 🧱 4. Log Every Action {#310a .graf .graf--h3 .graf-after--p name="310a"}

Audit logs aren't just for compliance. They're for accountability. If
something shady happens, logs are your first line of defense in
reconstructing what went wrong.

### 🚫 5. Never Assume Good Intentions {#5037 .graf .graf--h3 .graf-after--p name="5037"}

Always apply the principle of **zero trust**. Assume users may abuse any
feature that isn't guarded, verified, or rate-limited.

### For My Fellow Bug Hunters {#b5e6 .graf .graf--h3 .graf-after--p name="b5e6"}

To the security community, here's a word of advice:

**Keep poking.**

We're the final defense against lazy logic and poorly implemented
features. Even if there's no bounty, your responsible reporting helps
make the internet a slightly safer place.

And for every ignored report, there's a team out there who'll *actually
fix* what you find.

### For Users: Be Paranoid (in a Healthy Way) {#1016 .graf .graf--h3 .graf-after--p name="1016"}

As an end-user, you should:

- [Regularly check your account details.]{#266a}
- [Log out from shared devices.]{#7b1e}
- [Use strong, unique passwords.]{#26eb}
- [Enable 2FA wherever possible.]{#14e6}
- [Keep an eye on login or activity history if the app supports
  it.]{#c3ef}

Because if a bug like this exists on a random site, who knows what other
doors are left unlocked?

### Conclusion: Vibes Don't Cut It in Security {#5b87 .graf .graf--h3 .graf-after--p name="5b87"}

This was one of those bugs that looks silly on the surface but has
serious consequences underneath. And the craziest part?

It's not uncommon.

I've seen dozens of similar issues across all kinds of apps --- finance,
healthcare, e-commerce. Logic bugs are the silent killers of web
security.

If you're a developer, double-check your flows.

If you're a bug hunter, stay curious.

And if you're a user, don't assume the apps you use are
bulletproof --- because sometimes, all it takes to hijack your identity
is a simple API call and... vibes.

**Thanks for reading. Stay secure. Stay skeptical. And always verify
your damn email changes.**

*-- A curious cybersecurity nerd who still hasn't received a bug bounty,
but sleeps better knowing he tried.* 💻🕵️‍♂️
:::
::::
::::::
:::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [July 6, 2025](https://medium.com/p/fc89db324366).

[Canonical
link](https://medium.com/@bevijaygupta/when-you-can-just-change-your-email-no-otp-no-questions-asked-just-vibes-fc89db324366){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
