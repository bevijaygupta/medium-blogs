::: {}
# OSINT Tools for Investigative Journalists {#osint-tools-for-investigative-journalists .p-name}
:::

::: {.section .p-summary field="subtitle"}
It was a rainy evening in November when Clara, an investigative
journalist with years of experience, sat in front of her computer. She
had...
:::

::::::::::::::: {.section .e-content field="body"}
:::::: {#bc00 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### OSINT Tools for Investigative Journalists {#5006 .graf .graf--h3 .graf--leading .graf--title name="5006"}

<figure id="0922" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*ljKlPry1KC2F5K1pPFwg5Q.jpeg"
class="graf-image" data-image-id="1*ljKlPry1KC2F5K1pPFwg5Q.jpeg"
data-width="1200" data-height="675" data-is-featured="true" />
</figure>

*It was a rainy evening in November when Clara, an investigative
journalist with years of experience, sat in front of her computer. She
had just received a tip that a government official was involved in shady
offshore deals. The evidence was scarce, but Clara was determined to
uncover the truth. She had an arsenal of tools at her disposal, and she
was about to embark on a digital treasure hunt --- a journey fueled by
Open-Source Intelligence (OSINT).*

Investigative journalism, at its core, is about digging deeper into the
layers of secrecy and manipulation. With governments, corporations, and
individuals becoming increasingly secretive, journalists need the right
tools to keep up. The internet is a treasure trove of information, much
of which is publicly available. OSINT refers to collecting, analyzing,
and using publicly available data from the internet and other open
sources for investigative purposes.

This blog will guide you through the world of OSINT tools that
investigative journalists like Clara use to uncover hidden truths. We'll
explore a variety of tools, each designed for a specific purpose, and
even dive into how to use some of these tools with practical examples
and code snippets.

### 1. The Power of Google Dorking {#3059 .graf .graf--h3 .graf-after--p name="3059"}

*Clara knew her first step would be to gather as much information as
possible. She started by using Google --- but not in the way most people
do. Instead, Clara relied on "Google Dorks," an advanced search
technique used to locate information that is not easily accessible
through normal search queries.*

Google Dorking is an OSINT technique where specific search operators are
used to uncover hidden information that might not appear in general
search results. It allows you to look for specific file types, open
directories, or even sensitive information left unprotected on websites.

**Common Google Dork Commands:**

- [**`site:`{.markup--code .markup--li-code}** Restrict your search to a
  particular domain.\
  Example: `site:example.com "confidential"`{.markup--code
  .markup--li-code}]{#31fc}
- [**`filetype:`{.markup--code .markup--li-code}** Search for specific
  types of files (PDFs, docs, etc.).\
  Example: `filetype:pdf "salary report"`{.markup--code
  .markup--li-code}]{#3a75}
- [**`inurl:`{.markup--code .markup--li-code}** Find URLs that contain
  specific words.\
  Example: `inurl:login "admin"`{.markup--code .markup--li-code}]{#1b9b}

**Example:**\
Clara wanted to find documents related to a government project, so she
typed into Google:

``` {#61d9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
filetype:pdf "government project" site:gov
```

This query returned dozens of official documents that had not been
properly secured.

Google Dorking is powerful because many websites don't safeguard their
sensitive files. However, ethical journalists must tread carefully and
avoid accessing illegal or restricted content. It's about finding
publicly available information, not hacking.

### 2. Shodan: The Search Engine for Connected Devices {#e79c .graf .graf--h3 .graf-after--p name="e79c"}

*Next, Clara decided to dive into the world of connected devices. She
needed to see if any unsecured servers or databases could give her more
clues.*

Shodan is known as the most dangerous search engine on the web. It
indexes internet-connected devices, from traffic lights to web servers
and even security cameras. Investigative journalists can use Shodan to
uncover open databases, unsecured cameras, and even vulnerable
industrial systems.

Shodan is particularly useful for understanding how a company's
infrastructure is exposed to the internet. For example, if Clara wanted
to investigate a company's servers, she could search Shodan for any
exposed servers belonging to that organization.

**Example Search Query:**

``` {#27ac .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
"organization:ABC Corporation" port:80
```

This query would list all HTTP servers associated with ABC Corporation
that are exposed on the internet.

**Using Shodan's API in Python:**

``` {#7dc8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
import shodan
```

``` {#7d5c .graf .graf--pre .graf-after--pre}
API_KEY = "YOUR_SHODAN_API_KEY"
api = shodan.Shodan(API_KEY)
```

``` {#15d5 .graf .graf--pre .graf-after--pre}
# Perform a search for open MongoDB databases
results = api.search('product:MongoDB')
```

``` {#a923 .graf .graf--pre .graf-after--pre}
# Display the results
for result in results['matches']:
    print(f"IP: {result['ip_str']}")
    print(f"Port: {result['port']}")
    print(f"Data: {result['data']}")
    print("="*20)
```

In this example, Clara could find unsecured MongoDB databases, which
often contain sensitive data. Investigative journalists should use
Shodan responsibly to ensure they don't cross ethical lines or violate
laws.

### 3. Maltego: Visualizing Connections {#d522 .graf .graf--h3 .graf-after--p name="d522"}

*After gathering raw data from various sources, Clara needed to
visualize how these pieces of information connected. She turned to
Maltego, a powerful OSINT tool that allowed her to create a web of
interconnected data points.*

Maltego is a tool that helps investigative journalists visualize
relationships between people, organizations, domains, IP addresses, and
more. It uses "transforms" to gather data from various sources and
presents them as nodes in a network graph. Maltego can be a game-changer
when you're trying to make sense of a large dataset or uncover hidden
connections.

**Example Use Case:**

Clara wanted to investigate the connections between a corrupt
businessman and a series of offshore companies. She used Maltego to map
the relationships between the businessman, his email addresses,
associated domains, and companies.

**Steps:**

1.  [Start Maltego and create a new graph.]{#3c46}
2.  [Enter the businessman's name and run transforms to find email
    addresses, websites, and related companies.]{#98ca}
3.  [Use the "Person to Company" transform to find the companies he's
    associated with.]{#fce6}
4.  [Use the "Email to Domain" transform to find domains connected to
    his email address.]{#c0ba}

This helped Clara visualize the entire network, making it easier to
identify potential leads.

### 4. SpiderFoot: The OSINT Automation Tool {#256c .graf .graf--h3 .graf-after--p name="256c"}

*Clara was on a tight deadline, and manually searching through hundreds
of data points was time-consuming. She needed a way to automate her
OSINT efforts. That's when she turned to SpiderFoot.*

SpiderFoot is an OSINT tool that automates the process of gathering
data. It can collect information on domains, IP addresses, email
addresses, names, and more. SpiderFoot integrates with a variety of data
sources, including Shodan, Have I Been Pwned, and VirusTotal, making it
a one-stop-shop for OSINT automation.

**Example SpiderFoot Usage:**

Clara wanted to investigate a particular domain, so she used SpiderFoot
to gather information about its IP address, domain history, associated
email addresses, and possible breaches.

**Running SpiderFoot:**

``` {#b4e9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
spiderfoot -s example.com -o full
```

SpiderFoot will then run a scan on `example.com`{.markup--code
.markup--p-code} and produce a comprehensive report of its findings,
including who owns the domain, past DNS records, and even any associated
emails found in data breaches.

### 5. Recon-ng: The Swiss Army Knife of OSINT {#7a6c .graf .graf--h3 .graf-after--p name="7a6c"}

*Clara wanted to dig deeper into her target's online presence. To do
that, she used Recon-ng, a powerful web reconnaissance framework
designed specifically for OSINT.*

Recon-ng is a tool similar to Metasploit but built for reconnaissance.
It's modular, meaning you can add specific modules to perform various
tasks like gathering information from social media, WHOIS lookups, and
more.

**Example Recon-ng Workflow:**

Clara wanted to find information about the domain
`example.com`{.markup--code .markup--p-code}:

1.  [Start Recon-ng:]{#9a49}

``` {#b3d0 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
recon-ng
```

1.  [Add a workspace:]{#2c79}

``` {#f39d .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
workspaces add investigation_workspace
```

1.  [Use the domain profiler module:]{#8726}

``` {#3fa0 .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
modules load recon/domains-hosts/bing_domain_web
options set SOURCE example.com
run
```

This workflow allowed Clara to gather a list of hosts related to the
domain, giving her valuable insight into the company's online
infrastructure.

### 6. OSINT with Social Media: Twint for Twitter Investigations {#f39a .graf .graf--h3 .graf-after--p name="f39a"}

*Clara suspected that social media could hold valuable clues. She needed
to track Twitter accounts linked to her investigation but couldn't rely
on the platform's limited search capabilities. That's when she turned to
Twint.*

Twint is an advanced Twitter scraping tool that allows journalists to
gather information without using the Twitter API. It can be used to
search tweets, profiles, followers, and more.

**Twint Example:**

Clara wanted to see all the tweets from a particular account mentioning
offshore bank accounts.

``` {#0040 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
twint -u target_account --search "offshore bank"
```

This returned a list of tweets from the target account that mentioned
offshore banking, providing Clara with valuable clues.

**Python Integration:**

``` {#e91d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
import twint
```

``` {#f334 .graf .graf--pre .graf-after--pre}
c = twint.Config()
c.Username = "target_account"
c.Search = "offshore bank"
c.Store_csv = True
c.Output = "tweets.csv"
```

``` {#064b .graf .graf--pre .graf-after--pre}
twint.run.Search(c)
```

Twint allowed Clara to quickly search through thousands of tweets
without the restrictions imposed by Twitter's official API.

### 7. The Human Element: OSINT Isn't Just About Tools {#a111 .graf .graf--h3 .graf-after--p name="a111"}

*After days of investigation, Clara had gathered more than enough data.
However, she knew that OSINT isn't just about tools --- it's about
understanding human behavior.*

One of the most important aspects of OSINT is the ability to analyze
human interactions online. Social media profiles, public forums, and
even online marketplaces can provide crucial information. Investigative
journalists must always remember to look beyond the tools and focus on
the human element. Every piece of data leads to a person, a motive, or
an action. OSINT tools are only as good as the investigator using them.
:::
::::
::::::

:::::: {#8fca .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
**Conclusion:**

OSINT has revolutionized investigative journalism. Journalists like
Clara can now dig deeper and faster than ever before. With tools like
Google Dorking, Shodan, Maltego, SpiderFoot, Recon-ng, and Twint, the
internet becomes a goldmine of publicly available information. However,
with great power comes great responsibility. Investigative journalists
must always be mindful of ethics, privacy, and legality when conducting
their investigations.

The tools we've explored in this blog are just the beginning. The OSINT
world is vast and ever-evolving, but these foundational tools will help
any investigative journalist uncover the truth, no matter how deep it's
buried.
:::
::::
::::::

:::::: {#32f6 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
*As the rain finally stopped, Clara leaned back in her chair. Her
investigation had uncovered more than she had ever expected. Thanks to
OSINT, the truth was no longer hidden.*

### Promote and Collaborate on Cybersecurity Insights {#8754 .graf .graf--h3 .graf-after--p name="8754"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#59d7 .graf .graf--h3 .graf-after--p name="59d7"}

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
:::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 28, 2024](https://medium.com/p/5b55640769ea).

[Canonical
link](https://medium.com/@bevijaygupta/osint-tools-for-investigative-journalists-5b55640769ea){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
