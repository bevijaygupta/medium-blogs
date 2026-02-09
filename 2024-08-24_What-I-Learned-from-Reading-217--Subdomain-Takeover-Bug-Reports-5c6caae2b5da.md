::: {}
# What I Learned from Reading 217\* Subdomain Takeover Bug Reports {#what-i-learned-from-reading-217-subdomain-takeover-bug-reports .p-name}
:::

::: {.section .p-summary field="subtitle"}
In the world of cybersecurity, few vulnerabilities capture the attention
of both seasoned professionals and curious newcomers like the...
:::

::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#0f79 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### *What I Learned from Reading 217\** Subdomain Takeover Bug Reports {#98a9 .graf .graf--h3 .graf--leading .graf--title name="98a9"}

<figure id="ec13" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*IztvRBW-6isV8j9rXktZMg.png"
class="graf-image" data-image-id="1*IztvRBW-6isV8j9rXktZMg.png"
data-width="1600" data-height="1000" data-is-featured="true" />
</figure>

In the world of cybersecurity, few vulnerabilities capture the attention
of both seasoned professionals and curious newcomers like the subdomain
takeover. A potent mix of misconfiguration, negligence, and oversight
often leads to this critical vulnerability, allowing attackers to hijack
subdomains and potentially exploit them for malicious purposes. To truly
understand the mechanics, risks, and prevention strategies of subdomain
takeovers, I immersed myself in 217\* bug reports detailing real-world
cases of this vulnerability.

In this blog, I'll share what I learned from these reports, offering
insights into the patterns, common mistakes, and best practices that can
help secure your digital assets against subdomain takeovers.
:::
::::
::::::

:::::: {#e174 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 1. Understanding Subdomain Takeovers {#0d76 .graf .graf--h3 .graf--leading name="0d76"}

Before delving into the specifics of the bug reports, it's crucial to
grasp what subdomain takeovers are and why they pose such a significant
threat.

#### What is a Subdomain Takeover? {#9f06 .graf .graf--h4 .graf-after--p name="9f06"}

A subdomain takeover occurs when an attacker gains control over a
subdomain that still exists in the DNS (Domain Name System) but is no
longer properly associated with a service. This typically happens when a
company decommissions a resource but forgets to remove the corresponding
DNS entry. The orphaned DNS entry still points to the decommissioned
service, but since the service is no longer active, an attacker can
claim it by creating an account with the service provider or by pointing
it to their own infrastructure.

#### Why Are Subdomain Takeovers Dangerous? {#dd86 .graf .graf--h4 .graf-after--p name="dd86"}

The potential impact of a subdomain takeover can be severe:

- [**Phishing:** Attackers can use the compromised subdomain to host
  phishing pages, exploiting the trust associated with the legitimate
  domain.]{#ba7f}
- [**Malware Distribution:** The subdomain can be used to distribute
  malware, affecting users who visit it thinking it's part of the
  legitimate site.]{#f128}
- [**Brand Damage:** A subdomain under an attacker's control can be used
  to tarnish a brand's reputation, either by hosting inappropriate
  content or by being involved in cyberattacks.]{#22d0}
:::
::::
::::::

:::::: {#48fd .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 2. Common Patterns in Subdomain Takeover Reports {#f522 .graf .graf--h3 .graf--leading name="f522"}

As I combed through the 217\* bug reports, certain patterns and
commonalities emerged, shedding light on the typical scenarios that lead
to subdomain takeovers.

#### 2.1. Orphaned DNS Records {#d72c .graf .graf--h4 .graf-after--p name="d72c"}

The most frequent cause of subdomain takeovers in the reports was
orphaned DNS records. These are DNS entries that point to services that
have been decommissioned or moved, but the DNS entry itself was never
removed or updated. Examples include:

- [**Cloud Services:** Subdomains that were once tied to cloud services
  like AWS S3, Azure, or Heroku, but the associated buckets or apps were
  deleted.]{#45cd}
- [**Third-Party Integrations:** Integrations with services like GitHub
  Pages, Shopify, or WordPress that were terminated, but their DNS
  records remained active.]{#d468}

#### 2.2. Misconfigured CNAME Records {#4a1d .graf .graf--h4 .graf-after--li name="4a1d"}

CNAME (Canonical Name) records, which are used to alias one domain to
another, were often misconfigured. For example:

- [**Pointing to Nonexistent Resources:** A CNAME pointing to a
  non-existent GitHub Pages site or an AWS CloudFront distribution that
  was deleted.]{#7c7e}
- [**Incorrect Service Configurations:** Incorrectly setting up or
  failing to properly verify the ownership of a service before
  configuring a CNAME record.]{#24bd}

#### 2.3. Lack of Monitoring and Auditing {#3065 .graf .graf--h4 .graf-after--li name="3065"}

Many organizations failed to monitor and audit their DNS records
regularly. This oversight allowed attackers to exploit stale records
that pointed to decommissioned services. Key issues included:

- [**No Regular Audits:** DNS records were rarely, if ever, audited for
  accuracy.]{#7b33}
- [**Lack of Ownership Tracking:** It was unclear who owned certain
  subdomains, leading to their neglect when the associated service was
  decommissioned.]{#5a31}

#### 2.4. Improper Service Decommissioning {#3035 .graf .graf--h4 .graf-after--li name="3035"}

Improperly decommissioning services was another major theme.
Organizations would shut down services but forget to clean up the
associated DNS records. Examples included:

- [**Cloud Resources:** Forgetting to remove DNS entries after
  decommissioning cloud infrastructure.]{#af27}
- [**Old Projects:** Abandoning old projects or microsites without fully
  decommissioning the related subdomains.]{#cb4b}
:::
::::
::::::

:::::: {#2258 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 3. Insights into the Impact of Subdomain Takeovers {#fd43 .graf .graf--h3 .graf--leading name="fd43"}

Subdomain takeovers can have far-reaching consequences, as demonstrated
by the reports I analyzed. Understanding these impacts can help
underscore the importance of vigilance and proactive defense.

#### 3.1. Real-World Examples of Damage {#21c8 .graf .graf--h4 .graf-after--p name="21c8"}

Several reports highlighted the actual damage caused by subdomain
takeovers:

- [**Phishing Attacks:** In one case, an attacker used a hijacked
  subdomain to host a phishing page that mimicked the legitimate login
  page of a major service provider. The result was the compromise of
  hundreds of user accounts.]{#ce07}
- [**Brand Impersonation:** Another report detailed how an attacker used
  a compromised subdomain to impersonate a brand, sending fraudulent
  emails that damaged the company's reputation.]{#6258}
- [**SEO Poisoning:** In some instances, attackers used hijacked
  subdomains to host content that manipulated search engine rankings,
  directing traffic away from legitimate websites.]{#de0c}

#### 3.2. Financial and Reputational Costs {#27f7 .graf .graf--h4 .graf-after--li name="27f7"}

The financial and reputational costs associated with subdomain takeovers
were frequently mentioned in the reports:

- [**Cleanup Costs:** Organizations often had to spend significant
  resources on cleaning up after a subdomain takeover, including
  updating DNS records, notifying affected users, and reinforcing
  security measures.]{#aa2c}
- [**Legal Implications:** In some cases, legal action was taken against
  the companies for failing to protect user data or allowing phishing
  attacks to occur from their domains.]{#8791}
- [**Loss of Trust:** Perhaps the most significant impact was the loss
  of customer trust. Once a subdomain is compromised, users may be wary
  of interacting with the brand, fearing further security
  lapses.]{#d5d8}
:::
::::
::::::

:::::: {#3a77 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. Prevention Strategies: Lessons Learned {#ef2c .graf .graf--h3 .graf--leading name="ef2c"}

The 217\* reports I reviewed also offered a wealth of information on how
to prevent subdomain takeovers. Here are some of the most effective
strategies employed by organizations to safeguard their digital assets.

#### 4.1. Regular DNS Audits {#6a63 .graf .graf--h4 .graf-after--p name="6a63"}

Regular DNS audits are essential for maintaining control over your
subdomains. This involves:

- [**Automated Tools:** Utilize tools that can scan your DNS records for
  stale or misconfigured entries. These tools can be scheduled to run at
  regular intervals, providing continuous monitoring.]{#6bc5}
- [**Manual Reviews:** While automation is crucial, manual reviews by
  knowledgeable personnel can catch issues that automated tools might
  miss.]{#634b}

#### 4.2. Proper Decommissioning Procedures {#073d .graf .graf--h4 .graf-after--li name="073d"}

When decommissioning services, it's vital to follow a thorough process
to ensure that no orphaned DNS records are left behind:

- [**Check All Dependencies:** Before shutting down a service, ensure
  that all related DNS records are identified and properly
  handled.]{#bef6}
- [**Use a Checklist:** Create a checklist for service decommissioning
  that includes steps for DNS cleanup. This ensures that nothing is
  overlooked during the process.]{#bfb9}

#### 4.3. Implementing DNS Monitoring Solutions {#70f6 .graf .graf--h4 .graf-after--li name="70f6"}

Continuous monitoring of DNS records can help detect and prevent
subdomain takeovers:

- [**Real-Time Alerts:** Set up alerts for any changes to your DNS
  records. This can help catch unauthorized changes quickly.]{#8b8d}
- [**Historical Analysis:** Maintain logs of DNS changes to analyze
  trends and identify potential issues before they become
  critical.]{#6841}

#### 4.4. Strong Ownership and Accountability {#33c4 .graf .graf--h4 .graf-after--li name="33c4"}

Assigning clear ownership and accountability for DNS records can prevent
neglect:

- [**Designated Owners:** Each DNS record should have a designated owner
  responsible for its maintenance and accuracy.]{#3ab0}
- [**Regular Training:** Provide regular training for those responsible
  for DNS management to keep them up to date on best practices and
  common pitfalls.]{#10b9}

#### 4.5. Least Privilege Principle {#999a .graf .graf--h4 .graf-after--li name="999a"}

Applying the principle of least privilege can minimize the risk of
subdomain takeovers:

- [**Restrict Access:** Limit access to DNS management tools to only
  those who need it. This reduces the chance of accidental or malicious
  changes.]{#d807}
- [**Review Access Controls:** Regularly review who has access to DNS
  records and adjust permissions as needed.]{#0f78}
:::
::::
::::::

:::::: {#5c61 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Advanced Techniques for Detecting and Mitigating Subdomain Takeovers {#8997 .graf .graf--h3 .graf--leading name="8997"}

Beyond basic prevention strategies, some advanced techniques can further
enhance your defenses against subdomain takeovers.

#### 5.1. Automated Subdomain Takeover Scanning {#6bca .graf .graf--h4 .graf-after--p name="6bca"}

Use automated tools to regularly scan for potential subdomain takeovers:

- [**Open Source Tools:** There are several open-source tools available,
  such as Sublist3r and SubOver, which can scan for subdomains
  vulnerable to takeover.]{#7045}
- [**Custom Scripts:** For large organizations, custom scripts tailored
  to your specific infrastructure can provide more targeted and
  effective scanning.]{#f99c}

#### 5.2. DNS Security Extensions (DNSSEC) {#55cd .graf .graf--h4 .graf-after--li name="55cd"}

Implementing DNSSEC can help protect against various types of DNS
attacks, including subdomain takeovers:

- [**DNSSEC Basics:** DNSSEC adds a layer of security to DNS by ensuring
  that the responses to DNS queries are authentic and have not been
  tampered with.]{#c789}
- [**Deployment Considerations:** While DNSSEC can be complex to
  implement, it's a powerful tool in preventing DNS spoofing and similar
  attacks.]{#b183}

#### 5.3. Using Content Security Policy (CSP) and Subresource Integrity (SRI) {#9fe7 .graf .graf--h4 .graf-after--li name="9fe7"}

Content Security Policy (CSP) and Subresource Integrity (SRI) can
mitigate the impact of a subdomain takeover:

- [**CSP Headers:** CSP can prevent attackers from loading malicious
  content by restricting the domains from which content can be loaded.
  This limits the damage that can be done if a subdomain is
  compromised.]{#0297}
- [**SRI:** SRI ensures that only specific versions of resources (like
  scripts or stylesheets) are loaded by checking their integrity hashes.
  This prevents attackers from injecting malicious content even if they
  control a subdomain.]{#0135}
:::
::::
::::::

:::::: {#120f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 6. Case Studies: Learning from Real-World Subdomain Takeovers {#0025 .graf .graf--h3 .graf--leading name="0025"}

Several of the reports included detailed case studies that offered
valuable lessons in how subdomain takeovers occur and how they can be
prevented.

#### 6.1. Case Study 1: The Overlooked CNAME {#9fba .graf .graf--h4 .graf-after--p name="9fba"}

In one of the more illustrative cases, a large e-commerce company faced
a subdomain takeover due to an overlooked CNAME record pointing to a
third-party service that had been decommissioned. The service in
question was used for marketing campaigns but was phased out as the
company transitioned to a new platform.

**The Issue:**

- [The company's DNS records still included a CNAME entry for
  `campaigns.example.com`{.markup--code .markup--li-code}, which pointed
  to the third-party service that was no longer active.]{#cbd4}
- [An attacker noticed the orphaned CNAME and quickly registered the
  same service with the third-party provider, gaining control over
  `campaigns.example.com`{.markup--code .markup--li-code}.]{#c2bf}

**The Impact:**

- [The attacker used the compromised subdomain to host phishing pages,
  tricking customers into entering their credentials.]{#c2cf}
- [The phishing attack led to a significant breach, with thousands of
  customer accounts compromised, resulting in a loss of customer trust
  and significant financial damage.]{#f2e5}

**Lessons Learned:**

- [**Regular DNS Audits:** The importance of regularly auditing DNS
  records was underscored by this incident. If the company had routinely
  checked its DNS entries, the orphaned CNAME could have been identified
  and removed before it became a liability.]{#68f7}
- [**Service Decommissioning Procedures:** Proper decommissioning
  procedures, including the removal of associated DNS entries, could
  have prevented this issue.]{#1776}

#### 6.2. Case Study 2: Forgotten Cloud Resources {#f33f .graf .graf--h4 .graf-after--li name="f33f"}

A medium-sized tech company experienced a subdomain takeover after
forgetting to delete DNS records pointing to a decommissioned AWS S3
bucket. The bucket had been used for hosting static assets during a
product launch, but after the launch, the bucket was deleted without
updating the DNS records.

**The Issue:**

- [The DNS entry for `assets.example.com`{.markup--code
  .markup--li-code} was still pointing to the S3 bucket, which no longer
  existed.]{#442f}
- [An attacker, using automated tools to scan for such vulnerabilities,
  identified the open DNS entry and created a new S3 bucket with the
  same name, taking control of `assets.example.com`{.markup--code
  .markup--li-code}.]{#207e}

**The Impact:**

- [The compromised subdomain was used to serve malicious scripts, which
  were subsequently injected into the company's main website through
  compromised ads. This led to the distribution of malware to thousands
  of unsuspecting visitors.]{#c0d8}

**Lessons Learned:**

- [**Automated Scanning:** Implementing automated tools to detect
  potential subdomain takeover vulnerabilities could have prevented this
  issue. Such tools would have flagged the orphaned DNS entry as a
  risk.]{#dd21}
- [**Cloud Resource Management:** Proper cloud resource management,
  including ensuring that DNS records are updated when resources are
  decommissioned, is critical in preventing similar incidents.]{#df06}

#### 6.3. Case Study 3: Legacy Services and Neglect {#6c9a .graf .graf--h4 .graf-after--li name="6c9a"}

A financial services firm suffered a subdomain takeover due to
neglecting legacy services. The firm had moved away from using an older
third-party SaaS platform but failed to remove the corresponding DNS
entries.

**The Issue:**

- [The subdomain `oldportal.example.com`{.markup--code .markup--li-code}
  still pointed to the SaaS platform, which the company no longer used.
  The account with the SaaS provider had been terminated, but the DNS
  entry remained.]{#12da}
- [An attacker identified the abandoned subdomain and registered it on
  the SaaS platform, gaining control over the subdomain.]{#436d}

**The Impact:**

- [The attacker leveraged the subdomain to send spear-phishing emails to
  the firm's clients, resulting in significant data breaches and
  financial losses.]{#2f9f}

**Lessons Learned:**

- [**Legacy Service Cleanup:** Organizations must have a clear process
  for cleaning up after migrating away from legacy services. This
  includes removing or updating all associated DNS records.]{#f0b3}
- [**Ownership and Accountability:** Assigning clear ownership for DNS
  entries, even for legacy services, can prevent such
  oversights.]{#2869}
:::
::::
::::::

:::::: {#6778 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 7. The Role of Bug Bounty Programs in Identifying Subdomain Takeovers {#5060 .graf .graf--h3 .graf--leading name="5060"}

One of the consistent themes in the 217\* bug reports was the role that
bug bounty programs played in identifying and mitigating subdomain
takeover vulnerabilities.

#### 7.1. The Value of Crowdsourcing Security {#607f .graf .graf--h4 .graf-after--p name="607f"}

Bug bounty programs allow organizations to leverage the skills of a
global community of security researchers. In many cases, the subdomain
takeovers were discovered by independent researchers participating in
these programs.

**Benefits:**

- [**Diverse Perspectives:** Security researchers from different
  backgrounds can bring fresh perspectives to identifying
  vulnerabilities that might be overlooked by internal teams.]{#c21b}
- [**Incentivized Reporting:** By offering rewards, companies
  incentivize researchers to report vulnerabilities rather than exploit
  them maliciously.]{#53f1}

#### 7.2. Common Findings Through Bug Bounties {#1d38 .graf .graf--h4 .graf-after--li name="1d38"}

Many of the subdomain takeovers were identified through bug bounty
programs, with common findings including:

- [**Orphaned DNS Records:** Researchers frequently found subdomains
  pointing to decommissioned services that could be taken over.]{#23ef}
- [**Misconfigurations:** Misconfigured DNS records and CNAME entries
  were also common, often leading to potential subdomain
  takeovers.]{#eac9}

#### 7.3. Strengthening Your Bug Bounty Program {#a325 .graf .graf--h4 .graf-after--li name="a325"}

To maximize the effectiveness of a bug bounty program in identifying
subdomain takeover risks:

- [**Clear Scope Definition:** Clearly define the scope of the program,
  including which subdomains and DNS records should be tested.]{#bd36}
- [**Collaborative Engagement:** Engage with the security community,
  providing clear guidelines and prompt feedback to researchers who
  report vulnerabilities.]{#7b3f}
:::
::::
::::::

:::::: {#c68f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 8. Future-Proofing Against Subdomain Takeovers {#7201 .graf .graf--h3 .graf--leading name="7201"}

As the threat landscape evolves, so too must the strategies for
defending against subdomain takeovers. Here are some forward-looking
practices that can help secure your organization.

#### 8.1. Proactive Security Culture {#f356 .graf .graf--h4 .graf-after--p name="f356"}

Cultivating a proactive security culture is essential in staying ahead
of vulnerabilities like subdomain takeovers:

- [**Continuous Education:** Regularly educate your teams about the
  latest security threats, including subdomain takeovers, and how to
  prevent them.]{#ef0f}
- [**Security-First Mindset:** Encourage a security-first mindset where
  security considerations are integrated into every aspect of your
  operations, from development to infrastructure management.]{#3755}

#### 8.2. Integrating Security into DevOps (DevSecOps) {#6418 .graf .graf--h4 .graf-after--li name="6418"}

By integrating security into your DevOps processes, you can automate
many of the tasks necessary to prevent subdomain takeovers:

- [**Infrastructure as Code (IaC):** Manage your DNS configurations and
  cloud resources through IaC tools like Terraform, allowing for
  automated checks and audits.]{#8ef3}
- [**Continuous Monitoring:** Implement continuous monitoring tools that
  integrate with your CI/CD pipeline to automatically detect and alert
  on potential security issues.]{#db30}

#### 8.3. Embracing AI and Machine Learning {#4df6 .graf .graf--h4 .graf-after--li name="4df6"}

AI and machine learning can play a significant role in identifying and
mitigating subdomain takeovers:

- [**Anomaly Detection:** Machine learning models can be trained to
  detect anomalies in DNS configurations, flagging potential
  vulnerabilities before they can be exploited.]{#0c8e}
- [**Automated Response:** AI-driven automated response systems can take
  immediate action when a potential subdomain takeover is detected, such
  as removing or updating the DNS entry.]{#c97c}
:::
::::
::::::

:::::: {#991b .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 9. Conclusion {#34b2 .graf .graf--h3 .graf--leading name="34b2"}

The journey through 217\* subdomain takeover bug reports has been
eye-opening, revealing the many ways in which this vulnerability can
arise and the significant damage it can cause. However, it has also
highlighted the proactive measures that organizations can take to
protect themselves.

From understanding the common patterns and mistakes that lead to
subdomain takeovers to implementing advanced detection and mitigation
strategies, the key to preventing these incidents lies in vigilance,
education, and the adoption of robust security practices.

In a digital world where your brand's reputation and user trust are
paramount, ensuring that your subdomains are secure is not just a
technical necessity but a critical component of your overall security
posture. By learning from the past and adopting a forward-thinking
approach, you can defend against subdomain takeovers and keep your
digital assets safe.

Remember, in cybersecurity, the smallest oversight can lead to the
largest vulnerabilities. Stay vigilant, stay informed, and most
importantly, stay secure.

### Promote and Collaborate on Cybersecurity Insights {#48b7 .graf .graf--h3 .graf-after--p name="48b7"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#bba1 .graf .graf--h3 .graf-after--p name="bba1"}

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
:::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [August 24, 2024](https://medium.com/p/5c6caae2b5da).

[Canonical
link](https://medium.com/@bevijaygupta/what-i-learned-from-reading-217-subdomain-takeover-bug-reports-5c6caae2b5da){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
