---
title: "Intro to Python TryHackme 5e0fc5f0fe89"
platform: Medium
original_file: 2024-09-07_Intro-to-Python-TryHackme-5e0fc5f0fe89.md
---

# Intro to Python TryHackme 5e0fc5f0fe89

::: {}
# Intro to Python TryHackme {#intro-to-python-tryhackme .p-name}
:::

::: {.section .p-summary field="subtitle"}
Task 3. Mathematical Operators
:::

::::::: {.section .e-content field="body"}
:::::: {#1f68 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Intro to Python TryHackme {#d2c0 .graf .graf--h3 .graf--leading .graf--title name="d2c0"}

<figure id="8542" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*6fxCK0MN3J0uYbn_.png"
class="graf-image" data-image-id="0*6fxCK0MN3J0uYbn_.png"
data-width="692" data-height="233" />
</figure>

### Task 3. Mathematical Operators {#8c48 .graf .graf--h3 .graf-after--figure name="8c48"}

Question 1. What is the name of \>

> ***Answer: greater than***

Question 2. What is the name of !=

> ***Answer: not equal to***

Question 3. 1 != 0 will this return **true** or **false** (T or F)

> ***Answer: T***

Question 4. What is the name of \<=

> ***Answer: less than or equal to***

Question 5. Will this sample code return **truee** or **false**

<figure id="ba90" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Eg7_PItFVsV2i8HU.png"
class="graf-image" data-image-id="0*Eg7_PItFVsV2i8HU.png"
data-width="290" data-height="280" />
</figure>

> ***Answer: truee***

### Task 5. Variables and Data Types {#2ec0 .graf .graf--h3 .graf-after--blockquote name="2ec0"}

Question 1. What data type is 13

> ***Answer: integer***

Question 2. What data type is "65"

> ***Answer: string***

Question 3. What data type is 62.193

> ***Answer: float***

### Task 12. Challenge Time! {#374c .graf .graf--h3 .graf-after--blockquote name="374c"}

Question 1. Enter the decoded flag to complete the room!

The script **chal.py** decoded the string which is in the file
**encodedflag.txt** to get the final flag. This one has been base64'd 5
times, based32'd 5 times and base16'd 5 times.

``` {#e3c5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="go"}
import base64file = open("encodedflag.txt","r")flag = file.read()code = ""for i in range(0,5):
 code = base64.b16decode(flag)
 flag = codefor i in range(0,5):
 code = base64.b32decode(flag)
 flag = codefor i in range(0,5):
 code = base64.b64decode(code)
 flag = codeprint(flag)
file.close()
```

<figure id="eb1d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*otB97e9ptQmGWGY6.png"
class="graf-image" data-image-id="0*otB97e9ptQmGWGY6.png"
data-width="555" data-height="210" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#ade0 .graf .graf--h3 .graf-after--figure name="ade0"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#169b .graf .graf--h3 .graf-after--p name="169b"}

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
.h-card} on [September 7, 2024](https://medium.com/p/5e0fc5f0fe89).

[Canonical
link](https://medium.com/@bevijaygupta/intro-to-python-tryhackme-5e0fc5f0fe89){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
