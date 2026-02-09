::: {}
# Linux Challenges Tryhackme Writeup {#linux-challenges-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room : https://tryhackme.com/room/linuxctf
:::

::::::: {.section .e-content field="body"}
:::::: {#1c62 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Linux Challenges Tryhackme Writeup {#a0b3 .graf .graf--h3 .graf--leading .graf--title name="a0b3"}

<figure id="c689" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*rbFqEJQccTg8A9gE.png"
class="graf-image" data-image-id="0*rbFqEJQccTg8A9gE.png"
data-width="510" data-height="311" data-is-featured="true" />
</figure>

**Room :**
[https://tryhackme.com/room/linuxctf](https://tryhackme.com/room/linuxctf){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxctf"
rel="noopener ugc nofollow noopener" target="_blank"}

**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

The [**Linux
Challenges**](https://tryhackme.com/room/linuxctf){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/linuxctf"
rel="noopener ugc nofollow noopener" target="_blank"} **room** on the
TryHackMe platform is great for brushing up your Linux skills. This
write-up goes through finding flags on a Linux Machine using different
commands, services, and tools found in Linux Operating System. We will
be going through the entire room and finding flags hidden throughout the
systems which will lead to the completion of each task systematically.

**I recommend you folks try solving the challenges on your own and if
you get stuck somewhere you can always come back here.**

### Objectives {#89d9 .graf .graf--h3 .graf-after--p name="89d9"}

1.  [Learn to use commands such as find, locate, ls, grep, tar,
    etc.]{#4e2b}
2.  [Understand Cron jobs, MOTDs, locate hidden directories and files on
    the system.]{#3757}
3.  [Learn to SSH into different user account using private
    keys.]{#ad15}
4.  [Understand system files, paths, variables and file
    permissions.]{#67f3}
5.  [Learn to transfer files using SCP and remote desktop via GUI
    etc.]{#3a6a}

### Task 1- Linux Challenges Introduction {#bc78 .graf .graf--h3 .graf-after--li name="bc78"}

First things first, we need to connect to the TryHackMe network to
access our target machine. For this, we can either connect to OpenVPN or
use the in-browser machine access (Available for subscribed users). We
could use the following credentials in case we need to log in via SSH
manually.

**Question 1.** How many visible files can you see in garrys home
directory?

<figure id="e453" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QUwi18IgS5CHb4g7.png"
class="graf-image" data-image-id="0*QUwi18IgS5CHb4g7.png"
data-width="550" data-height="138" />
</figure>

> ***Answer: 3***

### Task 2. The Basics {#4ef2 .graf .graf--h3 .graf-after--blockquote name="4ef2"}

This section covers the basics of Linux. We are required to look for
hidden flags and we might need to switch to another user account for our
objectives. We need to find **10 flags** to complete this section's
challenge.

Let's find out our **first flag** by using the cat command as seen
below.

<figure id="9160" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9hVBMPHQr2s-j4m-.png"
class="graf-image" data-image-id="0*9hVBMPHQr2s-j4m-.png"
data-width="735" data-height="231" />
</figure>

We have to log in to bobs account to find our **Flag 2.**

<figure id="08a3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pqSNOVvo2TRfLaEK.png"
class="graf-image" data-image-id="0*pqSNOVvo2TRfLaEK.png"
data-width="759" data-height="246" />
</figure>

**Flag 3** is hidden where the **bash history** of the current user is
stored. We don't know the exact location of the bash history file which
is hidden so we can use the **locate** command and find the **flag 3**
as seen below.

<figure id="7b38" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hYdtj7P9j_LoRcgx.png"
class="graf-image" data-image-id="0*hYdtj7P9j_LoRcgx.png"
data-width="429" data-height="235" />
</figure>

Our **Flag 4** is located in crontab. **Crontab** is a list of commands
that are used to run on a specified schedule. Crontab is related to
**cronjobs** whose purpose is to execute specified instructions or
commands at a specified schedule or time. **crontab -e** allows to edit
the crontab entries.

<figure id="f0b5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kZoQdIn5vjMdcZow.png"
class="graf-image" data-image-id="0*kZoQdIn5vjMdcZow.png"
data-width="356" data-height="40" />
</figure>

<figure id="87a3" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Vg8dMwagkuIL-d0r.png"
class="graf-image" data-image-id="0*Vg8dMwagkuIL-d0r.png"
data-width="817" data-height="596" />
</figure>

Moving to our next flag i.e. **Flag 5**. Let's use the grep command
which comes in handy while finding any file, directory, or content of
the file. grep -r 'flag5' will recursively search for the content flag5.
As seen below we find the path to our **Flag5.**

<figure id="100d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*E34d5qHkLsv5jyQ4.png"
class="graf-image" data-image-id="0*E34d5qHkLsv5jyQ4.png"
data-width="524" data-height="481" />
</figure>

We are going to find the flag 6 similarly. The task gives us a hint that
the flag contains the letters '**c9**' in it. First, locate the Flag 6
directory using the **locate** command. As we output the file there is
too much text so here **grep** comes into action

<figure id="1e5a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bVBQvrRUBeDspnr6.png"
class="graf-image" data-image-id="0*bVBQvrRUBeDspnr6.png"
data-width="543" data-height="211" />
</figure>

Moving on to our next flag. The challenge hints us to look into the path
were processes are found. e will use the **ps** command which is used to
list down all the active processes on the system. The **flags** we set
with the **ps** commands allow us to list down active connections in a
list format.

<figure id="5cb0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Grpu-nvmlzIjZ_ms.png"
class="graf-image" data-image-id="0*Grpu-nvmlzIjZ_ms.png"
data-width="875" data-height="94" />
</figure>

**Flag 8** can be found on the home directory of the user bob. This file
needs to be decompressed to output the content of **Flag 8**

<figure id="d65f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IWRObN9yPTgpCJPI.png"
class="graf-image" data-image-id="0*IWRObN9yPTgpCJPI.png"
data-width="548" data-height="479" />
</figure>

The challenge hints us to look in the hosts' file to find our **Flag
9.**

<figure id="ae90" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0Q6Af2xRMh8wL8PM.png"
class="graf-image" data-image-id="0*0Q6Af2xRMh8wL8PM.png"
data-width="593" data-height="269" />
</figure>

For our final flag i.e. **Flag 10** we need to look into the directories
where we find all the users mainly password hashes are stored in this
file and if you are already familiar with the Linux files system and
directories you might have guessed it until now. Yes, it is the
**etc/passwd** file we have to look into. Analyzing the file we get our
final **flag 10.**

<figure id="5d24" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iwVJTKU18o9oL8q7.png"
class="graf-image" data-image-id="0*iwVJTKU18o9oL8q7.png"
data-width="875" data-height="95" />
</figure>

### Task 3- Linux Functionality {#c08a .graf .graf--h3 .graf-after--figure name="c08a"}

Moving on to the next challenge task, we would be using more of the
Linux commands here. Let's run the **flag11** and see what it says. As
the output says we have to look in where alias is created so .bashrc is
the right place to look and as seen below we have our **flag 11.**

<figure id="32c6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*la_OUqQ1aTr-mTTb.png"
class="graf-image" data-image-id="0*la_OUqQ1aTr-mTTb.png"
data-width="875" data-height="58" />
</figure>

**Flag 12** is found in the motd (Message of the day ) directory. So
navigate to the directory as shown below. Checking the header file we
have our flag12.

<figure id="032f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wacpfCsEDmMX9Uov.png"
class="graf-image" data-image-id="0*wacpfCsEDmMX9Uov.png"
data-width="852" data-height="194" />
</figure>

For the next flag, we navigate to the **Flag13** directory. There are
two scripts contained in this directory. As the challenge says to use
the **diff** command, diff command compares the content line by line and
produces the output. Doing so we get our **Flag 13**

<figure id="9e70" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zpoM67XIMKiR7Yd1.png"
class="graf-image" data-image-id="0*zpoM67XIMKiR7Yd1.png"
data-width="696" data-height="254" />
</figure>

Moving on to the next flag i.e. **Flag14**. We can find the flag where
logs are stored, navigate to the var/log directory as seen below. It can
be seen that our Flag14 is named **flagtourteen.txt** , there is a lot
of text and you will find the flag at the end. For simplicity, I use
**grep 3** as my flag contained the number three you can skip this
command as it is not necessary

<figure id="46a5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*P_Oz6C8PwDBbO3o9.png"
class="graf-image" data-image-id="0*P_Oz6C8PwDBbO3o9.png"
data-width="775" data-height="237" />
</figure>

**Flag15** can be found where system information is stored and that can
be found in the release directory. Navigating to this directory we find
our flag 15.

<figure id="0548" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9zJTHR_nzzMjJEZ7.png"
class="graf-image" data-image-id="0*9zJTHR_nzzMjJEZ7.png"
data-width="523" data-height="370" />
</figure>

Moving on to our next flag i.e Flag 16. This is hidden on one of the
mounts of the files system usually found in the directory of media.
Let's navigate to this directory. Seems like there are more directories
in each having a prefix of the word "**Flag16is**" as seen below.

<figure id="b814" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jPghJrbWn2dYviq7.png"
class="graf-image" data-image-id="0*jPghJrbWn2dYviq7.png"
data-width="470" data-height="171" />
</figure>

**Flag17** is found on Alice Account. So lets ssh into Alice's account,
her password is "TryHackMe123". Use **ls** to list all the files in the
directory and here we find our flag as seen below

<figure id="9f9a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*n_MEQw84BPoV_iZB.png"
class="graf-image" data-image-id="0*n_MEQw84BPoV_iZB.png"
data-width="546" data-height="203" />
</figure>

Moving on to our next hidden flag i.e. **Flag18,** it's hidden so we use
ls -la to list down all the hidden files and directories. Use **cat** to
output the result of the hidden flag

<figure id="dc39" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*uVsxHjSV045jTXQ4.png"
class="graf-image" data-image-id="0*uVsxHjSV045jTXQ4.png"
data-width="598" data-height="441" />
</figure>

The last flag for this section is flag19. We have to find the 2435 line
which will show us our flag19. We need to read a specific line of file
so we would use sed. **-n** flag is used to suppress the unmatched text
while the flag **p** is used to print the matched lines.

<figure id="7e17" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4Q3FXdivruWoHlFW.png"
class="graf-image" data-image-id="0*4Q3FXdivruWoHlFW.png"
data-width="511" data-height="108" />
</figure>

### Task 4- Data Representation, Strings, and Permissions {#5a83 .graf .graf--h3 .graf-after--figure name="5a83"}

This section will focus mainly on how data is represented on the Linux
System. In addition to that don't forget to use searching skills as some
of the tasks may require independent research using Google or any other
reference material.

We find our **Flag20** in Alice directory. When we cat the output we
find that the content is encoded using base64 and we need to decode it.
As seen below we can recognize if some string is encoded with base64 by
looking at the character set \[A-Z, a-z, 0--9, + /\]. So let's decode
the string to obtain our flag. Use the following command to decode.

<figure id="e774" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aiUsSKo0HPxdzxk3.png"
class="graf-image" data-image-id="0*aiUsSKo0HPxdzxk3.png"
data-width="587" data-height="137" />
</figure>

Moving on to our next **flag21.** This flag is a PHP file and by using
**less** command we find our flag as seen below. **Less** basically
outputs the content of files one page at a time, it's similar to
**more** but with more functionalities.

<figure id="7d9e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZFtxufS6LNCY4yEC.png"
class="graf-image" data-image-id="0*ZFtxufS6LNCY4yEC.png"
data-width="684" data-height="151" />
</figure>

When we output the content of our **Flag22,** the output is in the hex
format. We need to convert this is into ASCII as shown below. **xxd**
creates the hex dump of a file and converts the hex dump back to its
original binary.

<figure id="bb9f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1AdO2wUzWlxVeAcl.png"
class="graf-image" data-image-id="0*1AdO2wUzWlxVeAcl.png"
data-width="875" data-height="121" />
</figure>

**Flag23** is found very easily just by reversing the order of the
string found in the content of Flag23 as seen below.

<figure id="d78d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yGpE4ZLB5eRKJzVF.png"
class="graf-image" data-image-id="0*yGpE4ZLB5eRKJzVF.png"
data-width="512" data-height="122" />
</figure>

**Flag24** is a c program file. We will use the commands **strings** so
that human-readable strings are shown.

<figure id="6d1d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NBPF7HeRyUCqDvXP.png"
class="graf-image" data-image-id="0*NBPF7HeRyUCqDvXP.png"
data-width="518" data-height="123" />
</figure>

After we use the string command, we get our **Flag24** as seen below.

<figure id="5bbf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yZBcHH-pKmIVcE6d.png"
class="graf-image" data-image-id="0*yZBcHH-pKmIVcE6d.png"
data-width="402" data-height="239" />
</figure>

Locating flag26 is a bit tough as we need to find a string that is 32
characters long and starts with 4bceb. So here we are going to use the
find command in conjunction with grep as shown below

<figure id="f955" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*F8vZslkGiK0YcH2B.png"
class="graf-image" data-image-id="0*F8vZslkGiK0YcH2B.png"
data-width="820" data-height="131" />
</figure>

Moving on to our next **Flag27. Flag27** is owned by the root user so we
need to know that if Alice is allowed to execute certain commands to
extract the output of Flag27. So here we use Sudo -l that will tell me
which commands can be executed by the user Alice as seen below. So
running the commands that are permitted by root to the user Alice we
obtain our F**lag27.**

<figure id="8a8f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*T7vAaf_j1d87kZmR.png"
class="graf-image" data-image-id="0*T7vAaf_j1d87kZmR.png"
data-width="521" data-height="191" />
</figure>

Next, we need to find the kernel version which can be obtained using the
uname command as seen below. uname is used to display information about
the system version, OS, etc. **-r** flag shows the kernel release as
seen below.

<figure id="2a70" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zZQ08hI-AmJWBWd9.png"
class="graf-image" data-image-id="0*zZQ08hI-AmJWBWd9.png"
data-width="332" data-height="85" />
</figure>

We need to remove all spaces in the file and lines, split them by a
comma to get our final flag i.e. Flag29 for this section. As seen below
**tr** is used to translate or delete characters which in our case is
spaces.

<figure id="b1ca" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pc4iRe83XmvapyHm.png"
class="graf-image" data-image-id="0*pc4iRe83XmvapyHm.png"
data-width="584" data-height="84" />
</figure>

Once spaces are removed we can get our **Flag29** as seen below

<figure id="10a7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*t5rldPhC324Y9Vgu.png"
class="graf-image" data-image-id="0*t5rldPhC324Y9Vgu.png"
data-width="429" data-height="96" />
</figure>

### Task 5. SQL, FTP, Groups & RDP {#a5bc .graf .graf--h3 .graf-after--figure name="a5bc"}

This task challenges include playing with the databases by finding
flags, downloading, and transferring files to your local systems. So
let's get started!

We need to find our First flag i.e. Flag30 for our current task. We need
to look for any service running on the localhost. The command curl will
come in handy here. curl is a tool that is used to transfer to a server
or from a server using different supported protocols. Using curl in the
current scenario we find our flag.

<figure id="a629" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9P9cCzTJIhx6Jxoi.png"
class="graf-image" data-image-id="0*9P9cCzTJIhx6Jxoi.png"
data-width="501" data-height="60" />
</figure>

To find our Flag31 we need to login to the Database. Credentials of the
database are already given. Log into the database and use the command
**SHOW DATABASES;** which will list down the whole database and here we
find out **Flag31.**

<figure id="b17f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cT9gxS_ue6HkFSib.png"
class="graf-image" data-image-id="0*cT9gxS_ue6HkFSib.png"
data-width="774" data-height="532" />
</figure>

There is a bonus flag hidden in the database. For that we navigate to
the database we found earlier. Under that database there is a table
called **flag**, let's access it to find our bonus flag as seen below.

<figure id="ca1b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*c6-zCWJeY2rhDJeh.png"
class="graf-image" data-image-id="0*c6-zCWJeY2rhDJeh.png"
data-width="671" data-height="598" />
</figure>

The next flag is an mp3 file that needs to be downloaded to our local
system to see what's in it. We can either use SCP(Secure Copy) or
Filezilla to download it. I prefer using SCP. You can find the syntax
for SCP simply by googling.

``` {#a6f5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
scp alice@10.10.56.255:/home/alice/flag32.mp3 .
```

<figure id="4c52" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Nr8VrW3MPnT5xjix.png"
class="graf-image" data-image-id="0*Nr8VrW3MPnT5xjix.png"
data-width="875" data-height="70" />
</figure>

Listen to the file. It says: Try hack Me 13 37

We get our **Flag33** by navigating to. profile where personal paths are
stored as seen below.

<figure id="3dd0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*GlhDfPQ_-fZ74M1C.png"
class="graf-image" data-image-id="0*GlhDfPQ_-fZ74M1C.png"
data-width="607" data-height="104" />
</figure>

Let's switch to Bob's account and output the environment variable by
using **env** or **printenv** which will print all the environment
variables as shown below. We find our **Flag34** here.

<figure id="ea6b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3v9IqyfrSv3HHmx9.png"
class="graf-image" data-image-id="0*3v9IqyfrSv3HHmx9.png"
data-width="512" data-height="452" />
</figure>

We need to look into a place where all groups are created on the system.
Use the **getent group** command to do that, notice I have used grep in
conjunction with this command so that I get specific results. We find
our Flag35 as seen below.

<figure id="aae1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AwV3Y_pAGfv_kvo5.png"
class="graf-image" data-image-id="0*AwV3Y_pAGfv_kvo5.png"
data-width="614" data-height="66" />
</figure>

Our Final Flag for this section is related to the previous command. In
this challenging task, we need to find the user that is in the **hacker
group**. Through that, we are going to get our final flag. We use the
same command which we used to display all the groups on the system and
navigate to the specific user to find our Flag36 as seen below.

<figure id="2792" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*27iECMSpMgkg_EO2.png"
class="graf-image" data-image-id="0*27iECMSpMgkg_EO2.png"
data-width="514" data-height="145" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#fd0e .graf .graf--h3 .graf-after--figure name="fd0e"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#914a .graf .graf--h3 .graf-after--p name="914a"}

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
.h-card} on [August 26, 2024](https://medium.com/p/22d8f031b419).

[Canonical
link](https://medium.com/@bevijaygupta/linux-challenges-tryhackme-writeup-22d8f031b419){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
