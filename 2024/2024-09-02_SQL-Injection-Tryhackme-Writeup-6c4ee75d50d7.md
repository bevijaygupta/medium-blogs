---
title: "SQL Injection Tryhackme Writeup 6c4ee75d50d7"
platform: Medium
original_file: 2024-09-02_SQL-Injection-Tryhackme-Writeup-6c4ee75d50d7.md
---

# SQL Injection Tryhackme Writeup 6c4ee75d50d7

::: {}
# SQL Injection Tryhackme Writeup {#sql-injection-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/sqlibasics Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#94d0 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### SQL Injection Tryhackme Writeup {#077e .graf .graf--h3 .graf--leading .graf--title name="077e"}

<figure id="fa80" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*1bUJ3UjPh6AunrOP.png"
class="graf-image" data-image-id="0*1bUJ3UjPh6AunrOP.png"
data-width="535" data-height="229" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/sqlibasics](https://tryhackme.com/room/sqlibasics){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/sqlibasics"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### Definition {#0a88 .graf .graf--h3 .graf-after--p name="0a88"}

Union-based SQLi is a SQL injection technique that leverages the UNION
SQL operator to combine the results of two or more SELECT statements
into a single result which is then returned as part of the HTTP
response.

Approach

The UNION keyword lets you execute one or more additional SELECT queries
and append the results to the original query. For example:

``` {#f12f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT 1, 2 FROM usernames UNION SELECT 1, 2 FROM passwords
```

This SQL query will return a single result taken from 2 columns: first
and second positions from usernames and passwords.

UNION SQLi **attack** consists of 3 stages:

1\. You need to determine the number of columns you can retrieve.

2\. You make sure that the columns you found are in a suitable format

3\. Attack and get some interesting data.

\> Determining the number of columns required in an SQL injection UNION
attack

There are exactly two ways to detect one:

The first one involves injecting a series of ORDER BY queries until an
error occurs. For example:

``` {#564d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
# and so on until an error occurs
```

(The last value before the error would indicate the number of columns.)

The second one (most effective in my opinion), would involve submitting
a series of UNION SELECT payloads with a number of NULL values:

``` {#1e28 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
# until the error occurs
```

No error = number of NULL matches the number of columns.

\> Finding columns with a useful data type in an SQL injection UNION
attack

Generally, the interesting data that you want to retrieve will be in
string form. Having already determined the number of required columns,
(for example 4) you can probe each column to test whether it can hold
string data by replacing one of the UNION SELECT payloads with a string
value. In case of 4 you would submit:

``` {#83a4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--
```

No error = data type is useful for us (string).

\> Using an SQL injection UNION attack to retrieve interesting data

When you have determined the number of columns and found which columns
can hold string data, you can finally start retrieving interesting data.

Suppose that:

\* The first two steps showed exactly two existing columns with the
useful datatype.

\* The database contains a table called users with the columns username
and password.

(This can be figured out by using the boolean technique from Unit 6)

In this situation, you can retrieve the contents of the user's table by
submitting the input:

``` {#e404 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
' UNION SELECT username, password FROM users --
```

Practice

Go ahead the deploy the provided machine at the beginning of the task.
Browse to `10.10.208.189:3000`{.markup--code .markup--p-code}

A given small lab is a **highly** vulnerable web application, with a lot
of misconfigurations and developer mistakes.

<figure id="50ee" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zTq6Hiu5nt83-YtT.png"
class="graf-image" data-image-id="0*zTq6Hiu5nt83-YtT.png"
data-width="875" data-height="606" />
</figure>

First, browse to `10.10.208.189:3000/resetdb.php`{.markup--code
.markup--p-code} to set up the database.\
Then, go to `10.10.208.189:3000/register.php`{.markup--code
.markup--p-code} and register a new account. Make sure you input
something interesting, as you\'ll be able to interact with that data
later on! (Question 4)

<figure id="862d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*P1vbp50_OPHucAWV.png"
class="graf-image" data-image-id="0*P1vbp50_OPHucAWV.png"
data-width="704" data-height="462" />
</figure>

ow let's proceed to the main objective --- exploiting the web app. A
vulnerable search field is located at
10.10.208.189:3000/searchproducts.php

<figure id="46e0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6k6rCmIG7pBcT9zw.png"
class="graf-image" data-image-id="0*6k6rCmIG7pBcT9zw.png"
data-width="875" data-height="282" />
</figure>

Let's start our exploitation process!

As you might remember, we, first, need to determine the number of
available columns by inputting a series of\
`' UNION SELECT NULL --`{.markup--code .markup--p-code} into the search
field.\
To spice things up, I\'ve configured the database to also throw an error
when having a **\--** at the end. To bypass that, we need to include an
additional comment after the **\--**. You can use either **//** or
**/\*** do bypass that configuration.

<figure id="660d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*D4OOc8Lre4E83NNY.png"
class="graf-image" data-image-id="0*D4OOc8Lre4E83NNY.png"
data-width="523" data-height="214" />
</figure>

As you can see on the screenshot above, a single NULL value causes an
error, meaning that there are more columns. Try inputting NULL values
until you finally get the number. Note it down to answer the questions
later on.

``` {#bdb1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
' UNION SELECT NULL,NULL,NULL,NULL,NULL -- //
```

**Question 1**.How many columns are being returned by the query?

> ***Answer: 5***

Now, try inputting **'a'** instead of random NULL values and see if
there's an error. An error will indicate that the given column format is
not suitable for us and cannot be exploited.

<figure id="3973" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MRC2gSjfxvUTWD-x.png"
class="graf-image" data-image-id="0*MRC2gSjfxvUTWD-x.png"
data-width="875" data-height="177" />
</figure>

**Question 2**. How many of these columns can accept strings? ('a')

``` {#babd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
' UNION SELECT NULL,NULL,NULL,NULL,'a' -- //
' UNION SELECT NULL,NULL,NULL,'a',NULL -- //
' UNION SELECT NULL,NULL,'a',NULL,NULL -- //
' UNION SELECT NULL,'a',NULL,NULL,NULL -- //
' UNION SELECT 'a',NULL,NULL,NULL,NULL -- //
```

> ***Answer: 5***

Finally, we can start getting some valuable information. Simply replace
some null values with SQL keywords to get information about the
database.\
Here's a small list of thing you'd want to retrieve:

1\. database()

2\. user()

3\. @@version

4\. username

5\. password

6\. table_name

7\. column_name

Use the **database()** to answer Question 3.

**Question 3**. What's the database name?

``` {#1a81 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
' UNION SELECT NULL,database(),NULL,NULL,NULL -- //
```

> ***Answer: sqlitraining***

### Task 8. Automating exploitation {#8fba .graf .graf--h3 .graf-after--blockquote name="8fba"}

Question 1. How would you get an OS shell on website
**"sqli.thm/login.php"**? (URL switch comes first)

> ***Answer: sqlmap -u sqli.thm/login.php --- os-shell***

Question 2. What about listing all databases on the same website? (URL
switch comes first)

> ***Answer: sqlmap -u sqli.thm/login.php --- dbs***

### Resources and Practices {#d2f7 .graf .graf--h3 .graf-after--blockquote name="d2f7"}

Payload Lists:

Project link: [http://sqlmap.org/](http://sqlmap.org/){.markup--anchor
.markup--p-anchor data-href="http://sqlmap.org/"
rel="noopener ugc nofollow noopener" target="_blank"}

Github:
[https://github.com/sqlmapproject/sqlmap](https://github.com/sqlmapproject/sqlmap){.markup--anchor
.markup--p-anchor data-href="https://github.com/sqlmapproject/sqlmap"
rel="noopener ugc nofollow noopener" target="_blank"}

**Command examples:**

[https://www.security-sleuth.com/sleuth-blog/2017/1/3/sqlmap-cheat-sheet](https://www.security-sleuth.com/sleuth-blog/2017/1/3/sqlmap-cheat-sheet){.markup--anchor
.markup--p-anchor
data-href="https://www.security-sleuth.com/sleuth-blog/2017/1/3/sqlmap-cheat-sheet"
rel="noopener ugc nofollow noopener" target="_blank"}

**All-in-one cheat sheet:**

[https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/](https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/){.markup--anchor
.markup--p-anchor
data-href="https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/"
rel="noopener ugc nofollow noopener" target="_blank"}

1\.
[https://github.com/payloadbox/sql-injection-payload-list](https://github.com/payloadbox/sql-injection-payload-list){.markup--anchor
.markup--p-anchor
data-href="https://github.com/payloadbox/sql-injection-payload-list"
rel="noopener ugc nofollow noopener" target="_blank"}

2\.
[https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection){.markup--anchor
.markup--p-anchor
data-href="https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection"
rel="noopener ugc nofollow noopener" target="_blank"}

### Guides & Blogs: {#90e8 .graf .graf--h3 .graf-after--p name="90e8"}

1\.
[https://www.sqlinjection.net/](https://www.sqlinjection.net/){.markup--anchor
.markup--p-anchor data-href="https://www.sqlinjection.net/"
rel="noopener ugc nofollow noopener" target="_blank"}

2\.
[http://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet](http://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet){.markup--anchor
.markup--p-anchor
data-href="http://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet"
rel="noopener ugc nofollow noopener" target="_blank"}

3\.
[https://github.com/trietptm/SQL-Injection-Payloads](https://github.com/trietptm/SQL-Injection-Payloads){.markup--anchor
.markup--p-anchor
data-href="https://github.com/trietptm/SQL-Injection-Payloads"
rel="noopener ugc nofollow noopener" target="_blank"}

4\.
[https://pentestlab.blog/2012/12/24/sql-injection-authentication-bypass-cheat-sheet](https://pentestlab.blog/2012/12/24/sql-injection-authentication-bypass-cheat-sheet){.markup--anchor
.markup--p-anchor
data-href="https://pentestlab.blog/2012/12/24/sql-injection-authentication-bypass-cheat-sheet"
rel="noopener ugc nofollow noopener" target="_blank"}

5\.
[https://resources.infosecinstitute.com/dumping-a-database-using-sql-injection/](https://resources.infosecinstitute.com/dumping-a-database-using-sql-injection/){.markup--anchor
.markup--p-anchor
data-href="https://resources.infosecinstitute.com/dumping-a-database-using-sql-injection/"
rel="noopener ugc nofollow noopener" target="_blank"}

1\.
[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection){.markup--anchor
.markup--p-anchor
data-href="https://portswigger.net/web-security/sql-injection"
rel="noopener ugc nofollow noopener" target="_blank"}

2\.
[https://github.com/Audi-1/sqli-labs](https://github.com/Audi-1/sqli-labs){.markup--anchor
.markup--p-anchor data-href="https://github.com/Audi-1/sqli-labs"
rel="noopener ugc nofollow noopener" target="_blank"}

3\.
[https://github.com/appsecco/sqlinjection-training-app](https://github.com/appsecco/sqlinjection-training-app){.markup--anchor
.markup--p-anchor
data-href="https://github.com/appsecco/sqlinjection-training-app"
rel="noopener ugc nofollow noopener" target="_blank"}

4\.
[https://tryhackme.com/room/gamezone](https://tryhackme.com/room/gamezone){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/gamezone"
rel="noopener ugc nofollow noopener" target="_blank"}

5\.
[https://tryhackme.com/room/avengers](https://tryhackme.com/room/avengers){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/avengers"
rel="noopener ugc nofollow noopener" target="_blank"}

6\.
[https://tryhackme.com/room/uopeasy](https://tryhackme.com/room/uopeasy){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/uopeasy"
rel="noopener ugc nofollow noopener" target="_blank"}

7\.
[https://tryhackme.com/room/jurassicpark](https://tryhackme.com/room/jurassicpark){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/jurassicpark"
rel="noopener ugc nofollow noopener" target="_blank"}

### Promote and Collaborate on Cybersecurity Insights {#4ea6 .graf .graf--h3 .graf-after--p name="4ea6"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#173b .graf .graf--h3 .graf-after--p name="173b"}

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
.h-card} on [September 2, 2024](https://medium.com/p/6c4ee75d50d7).

[Canonical
link](https://medium.com/@bevijaygupta/sql-injection-tryhackme-writeup-6c4ee75d50d7){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
