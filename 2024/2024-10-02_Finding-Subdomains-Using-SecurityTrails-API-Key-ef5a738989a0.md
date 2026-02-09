---
title: "Finding Subdomains Using SecurityTrails API Key ef5a738989a0"
platform: Medium
original_file: 2024-10-02_Finding-Subdomains-Using-SecurityTrails-API-Key-ef5a738989a0.md
---

# Finding Subdomains Using SecurityTrails API Key ef5a738989a0

::: {}
# Finding Subdomains Using SecurityTrails API Key {#finding-subdomains-using-securitytrails-api-key .p-name}
:::

::: {.section .p-summary field="subtitle"}
In the realm of cybersecurity, subdomain enumeration is one of the key
steps in reconnaissance for penetration testers and bug bounty...
:::

::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#fd7b .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Finding Subdomains Using SecurityTrails API Key {#43f2 .graf .graf--h3 .graf--leading .graf--title name="43f2"}

<figure id="e67c" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*egnYbAgIWMLwRn2a"
class="graf-image" data-image-id="0*egnYbAgIWMLwRn2a" data-width="1200"
data-height="627" data-is-featured="true" />
</figure>

In the realm of cybersecurity, subdomain enumeration is one of the key
steps in reconnaissance for penetration testers and bug bounty hunters.
By uncovering all the subdomains of a target, security professionals can
identify additional attack surfaces that may harbor vulnerabilities.
While there are many tools available for subdomain enumeration,
SecurityTrails has emerged as one of the most reliable and powerful
resources for this purpose.

In this blog post, we will delve deep into the process of finding
subdomains using the SecurityTrails API. We will cover the following
topics:

- [Introduction to SecurityTrails]{#957d}
- [What is Subdomain Enumeration and Why is it Important?]{#3ebe}
- [Setting up and Configuring the SecurityTrails API]{#7c0b}
- [How to Use SecurityTrails API to Find Subdomains]{#607a}
- [Automating Subdomain Enumeration with SecurityTrails API]{#6705}
- [Handling API Limits and Rate-Limiting Issues]{#f820}
- [Case Study: Real-world Subdomain Discovery with SecurityTrails
  API]{#d14c}
- [Best Practices for Subdomain Enumeration]{#6721}
- [Conclusion]{#95d6}
:::
::::
::::::

:::::: {#4656 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 1. Introduction to SecurityTrails {#71de .graf .graf--h3 .graf--leading name="71de"}

SecurityTrails is a comprehensive domain data platform that provides
security professionals, researchers, and businesses with real-time
information about domain names, DNS, IP addresses, WHOIS data, and much
more. Its vast repository of historical and real-time data allows users
to investigate digital assets and track changes across the internet. One
of its standout features is its **subdomain enumeration capabilities**
through its API, which makes it a highly valued tool for cybersecurity
professionals.

SecurityTrails offers various APIs to help in gathering intelligence
about a target domain, and subdomain enumeration is one of the most
popular and frequently used functions.
:::
::::
::::::

:::::: {#ad47 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 2. What is Subdomain Enumeration and Why is it Important? {#dd88 .graf .graf--h3 .graf--leading name="dd88"}

Subdomain enumeration refers to the process of discovering all
subdomains associated with a given domain. A subdomain is essentially a
prefix to the main domain and can host various applications or services,
which might be overlooked during a standard security assessment.

For example, if the domain is `example.com`{.markup--code
.markup--p-code}, subdomains could include:

- [`blog.example.com`{.markup--code .markup--li-code}]{#bc5c}
- [`mail.example.com`{.markup--code .markup--li-code}]{#5fcc}
- [`dev.example.com`{.markup--code .markup--li-code}]{#d82b}

Subdomains are often prone to security misconfigurations, outdated
software, or unused and forgotten services, making them attractive
targets for attackers. Discovering subdomains allows security
professionals to:

- [Expand the attack surface for testing]{#21af}
- [Uncover misconfigured or unmonitored assets]{#2f24}
- [Identify forgotten services that may be vulnerable to attack]{#8fc2}
- [Enhance the overall understanding of an organization's web
  infrastructure]{#da01}

By performing thorough subdomain enumeration, security testers can
ensure they have a complete view of all potential entry points into a
network.
:::
::::
::::::

:::::: {#3106 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 3. Setting up and Configuring the SecurityTrails API {#4049 .graf .graf--h3 .graf--leading name="4049"}

Before we start finding subdomains, we need to set up the SecurityTrails
API. To get started, you need to sign up for a SecurityTrails account
and obtain an API key.

#### Steps to Get a SecurityTrails API Key: {#f77e .graf .graf--h4 .graf-after--p name="f77e"}

1.  [**Sign up on SecurityTrails**: Go to
    [SecurityTrails](https://securitytrails.com/){.markup--anchor
    .markup--li-anchor data-href="https://securitytrails.com/"
    rel="noopener" target="_blank"} and sign up for a free account.
    SecurityTrails offers both free and paid tiers, and the free version
    will provide limited API requests, which are sufficient for learning
    and small-scale projects.]{#2ee2}
2.  [**Get your API key**: Once logged in, navigate to the "API" section
    from your dashboard. Here, you will find your API key, which is
    required for making API requests.]{#6824}
3.  [**Install Dependencies**: Before diving into the API, ensure you
    have the right dependencies installed for making HTTP requests in
    your preferred programming language. In this tutorial, we'll use
    Python and its `requests`{.markup--code .markup--li-code} library,
    which can be installed via:]{#7e66}

- [`pip install requests`{.markup--code .markup--li-code}]{#26f5}

**Set up the environment**: Store your API key in a secure environment
variable for easy access:

- [`export SECURITYTRAILS_API_KEY="your_api_key_here"`{.markup--code
  .markup--li-code}]{#3f62}

With the API key and the environment ready, we can move on to querying
the API.
:::
::::
::::::

:::::: {#8651 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. How to Use SecurityTrails API to Find Subdomains {#063b .graf .graf--h3 .graf--leading name="063b"}

The SecurityTrails API allows you to query subdomain data for a specific
domain. Below is a simple Python script that uses the SecurityTrails API
to find subdomains.

#### Python Code Example: {#74d4 .graf .graf--h4 .graf-after--p name="74d4"}

``` {#05a5 .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
import os
import requests
```

``` {#b750 .graf .graf--pre .graf-after--pre}
# Get the API key from environment variable
API_KEY = os.getenv('SECURITYTRAILS_API_KEY')
BASE_URL = 'https://api.securitytrails.com/v1'
```

``` {#124d .graf .graf--pre .graf-after--pre}
# Function to find subdomains using SecurityTrails API
def find_subdomains(domain):
    url = f"{BASE_URL}/domain/{domain}/subdomains"
    headers = {
        "Content-Type": "application/json",
        "APIKEY": API_KEY
    }
    
    # Make the API request
    response = requests.get(url, headers=headers)
    
    # Check if the request was successful
    if response.status_code == 200:
        data = response.json()
        subdomains = data.get("subdomains", [])
        print(f"Subdomains for {domain}:")
        for subdomain in subdomains:
            print(f"- {subdomain}.{domain}")
    else:
        print(f"Failed to retrieve subdomains: {response.status_code}")
        print(response.text)
```

``` {#d693 .graf .graf--pre .graf-after--pre}
# Example usage
if __name__ == "__main__":
    domain = "example.com"
    find_subdomains(domain)
```

#### Explanation: {#83c4 .graf .graf--h4 .graf-after--pre name="83c4"}

- [**API Key**: The script retrieves your API key from the environment
  variable and sends it in the request headers.]{#37e1}
- [**API Endpoint**: The `/domain/{domain}/subdomains`{.markup--code
  .markup--li-code} endpoint provides a list of subdomains for the
  specified domain.]{#189d}
- [**Subdomains List**: The response contains the discovered subdomains,
  which are printed out in the format
  `subdomain.example.com`{.markup--code .markup--li-code}.]{#7010}

When you run this script, you will receive a list of subdomains for the
specified domain if they exist.
:::
::::
::::::

:::::: {#e350 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Automating Subdomain Enumeration with SecurityTrails API {#7df7 .graf .graf--h3 .graf--leading name="7df7"}

For large-scale assessments, you can automate the process of finding
subdomains using SecurityTrails across multiple domains. Below is an
extended script that reads a list of domains from a file, queries the
API, and stores the results in a CSV file for further analysis.

#### Extended Python Code for Bulk Enumeration: {#ae7c .graf .graf--h4 .graf-after--p name="ae7c"}

``` {#be67 .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
import os
import csv
import requests
```

``` {#4f59 .graf .graf--pre .graf-after--pre}
# Get the API key from environment variable
API_KEY = os.getenv('SECURITYTRAILS_API_KEY')
BASE_URL = 'https://api.securitytrails.com/v1'
```

``` {#46eb .graf .graf--pre .graf-after--pre}
# Function to find subdomains using SecurityTrails API
def find_subdomains(domain):
    url = f"{BASE_URL}/domain/{domain}/subdomains"
    headers = {
        "Content-Type": "application/json",
        "APIKEY": API_KEY
    }
    
    # Make the API request
    response = requests.get(url, headers=headers)
    
    # Check if the request was successful
    if response.status_code == 200:
        data = response.json()
        return data.get("subdomains", [])
    else:
        return []
```

``` {#7261 .graf .graf--pre .graf-after--pre}
# Function to save subdomains to CSV
def save_to_csv(domain, subdomains):
    with open(f"{domain}_subdomains.csv", mode="w", newline="") as file:
        writer = csv.writer(file)
        writer.writerow(["Subdomain"])
        for subdomain in subdomains:
            writer.writerow([f"{subdomain}.{domain}"])
```

``` {#f7b5 .graf .graf--pre .graf-after--pre}
# Main function to process multiple domains
def process_domains(filename):
    with open(filename, "r") as file:
        domains = [line.strip() for line in file.readlines()]
        
    for domain in domains:
        subdomains = find_subdomains(domain)
        if subdomains:
            print(f"Found {len(subdomains)} subdomains for {domain}")
            save_to_csv(domain, subdomains)
        else:
            print(f"No subdomains found for {domain}")
```

``` {#4ab9 .graf .graf--pre .graf-after--pre}
# Example usage
if __name__ == "__main__":
    # Specify the file with domains
    domains_file = "domains.txt"
    process_domains(domains_file)
```

#### Explanation: {#5551 .graf .graf--h4 .graf-after--pre name="5551"}

- [**Bulk Processing**: The script reads a list of domains from a
  `domains.txt`{.markup--code .markup--li-code} file and finds
  subdomains for each domain.]{#f0ae}
- [**CSV Output**: For each domain, the discovered subdomains are saved
  in a CSV file named after the domain.]{#c520}
- [**Automation**: This script is useful for automating subdomain
  discovery across multiple targets.]{#9e7e}
:::
::::
::::::

:::::: {#a80f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 6. Handling API Limits and Rate-Limiting Issues {#3e61 .graf .graf--h3 .graf--leading name="3e61"}

SecurityTrails enforces rate limits on API usage, especially for
free-tier accounts. To avoid hitting these limits during bulk
enumeration, you should:

- [**Implement Rate Limiting**: Add delays between API requests using
  `time.sleep()`{.markup--code .markup--li-code} in Python to prevent
  overwhelming the server.]{#7752}
- [**Upgrade to a Paid Plan**: For more extensive subdomain enumeration
  tasks, consider upgrading your SecurityTrails plan to increase your
  API request limit.]{#aefe}
- [**Handle Errors Gracefully**: Implement error handling for status
  codes like 429 (Too Many Requests) to avoid disruptions in your
  script.]{#9ad6}
:::
::::
::::::

:::::: {#1f0f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 7. Case Study: Real-World Subdomain Discovery with SecurityTrails API {#fb7e .graf .graf--h3 .graf--leading name="fb7e"}

Let's explore a real-world case study of how a security researcher used
SecurityTrails to discover subdomains for a large organization. The
researcher was targeting a financial services company and found a
critical subdomain (`dev-financial.example.com`{.markup--code
.markup--p-code}) that was hosting an outdated and vulnerable version of
an internal application. This subdomain was unprotected and accessible
to the public.

By reporting the vulnerability through the company's bug bounty program,
the researcher helped prevent a potential data breach. This case
underscores the importance of thorough subdomain enumeration in
identifying attack surfaces.
:::
::::
::::::

:::::: {#955e .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 8. Best Practices for Subdomain Enumeration {#aa19 .graf .graf--h3 .graf--leading name="aa19"}

To maximize the effectiveness of subdomain enumeration, follow these
best practices:

- [**Use Multiple Tools**: While SecurityTrails is powerful, combine it
  with other tools like Amass, Sublist3r, and crt.sh to ensure
  comprehensive coverage.]{#5bfd}
- [**Filter Subdomains**: Some subdomains may be irrelevant for testing.
  Filter out well-known services (e.g., `mail`{.markup--code
  .markup--li-code}, `cdn`{.markup--code .markup--li-code}) to focus on
  potential weak points.]{#c78c}
- [**Monitor Changes**: Subdomains may change over time, so continuously
  monitor for new subdomains to stay ahead of attackers.]{#b29b}
- [**Automate Regular Checks**: Set up periodic scans using automation
  to detect new subdomains or services as soon as they are
  deployed.]{#922d}
:::
::::
::::::

:::::: {#2a3b .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 9. Conclusion {#942a .graf .graf--h3 .graf--leading name="942a"}

Finding subdomains is a critical step in any security assessment.
SecurityTrails, with its powerful API, provides an efficient and
reliable way to perform subdomain enumeration. By following the steps
outlined in this guide, you can leverage the SecurityTrails API to
discover subdomains, automate the process, and ensure that no attack
surface goes unnoticed.

From understanding the basics of subdomain enumeration to automating
discovery across multiple domains, you now have the tools and knowledge
needed to enhance your reconnaissance efforts. By adopting best
practices and combining SecurityTrails with other tools, you'll be
well-equipped to uncover hidden assets and bolster your security
posture.

Whether you're a security researcher, penetration tester, or bug bounty
hunter, mastering subdomain enumeration with the SecurityTrails API is a
valuable skill that will help you discover vulnerabilities and protect
your target organizations from potential attacks. Happy hunting!

### Promote and Collaborate on Cybersecurity Insights {#40ce .graf .graf--h3 .graf-after--p name="40ce"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#7c5e .graf .graf--h3 .graf-after--p name="7c5e"}

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
:::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [October 2, 2024](https://medium.com/p/ef5a738989a0).

[Canonical
link](https://medium.com/@bevijaygupta/finding-subdomains-using-securitytrails-api-key-ef5a738989a0){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
