::: {}
# Sysinternals Tryhackme Writeup {#sysinternals-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/btsysinternalssg Note: This room
is for Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#dd69 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Sysinternals Tryhackme Writeup {#cd9d .graf .graf--h3 .graf--leading .graf--title name="cd9d"}

<figure id="775b" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*IPRznclJX6xro4j-.png"
class="graf-image" data-image-id="0*IPRznclJX6xro4j-.png"
data-width="539" data-height="236" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

Here i am Use Tryhackme Attach-box

### Task 1. Introduction {#d419 .graf .graf--h3 .graf-after--p name="d419"}

What are the tools known as **Sysinternals**?

The Sysinternals tools is a compilation of over 70+ Windows-based tools.
Each of the tools falls into one of the following categories:

- [**File and Disk Utilities**]{#a6a2}
- [**Networking Utilities**]{#b1ad}
- [**Process Utilities**]{#a8c2}
- [**Security Utilities**]{#14ac}
- [**System Information**]{#95a3}
- [**Miscellaneous**]{#cff9}

The Sysinternals tools and its website (sysinternals.com) were created
by Mark Russinovich back in the late '90s, along with an individual
named Bryce Cogswell under the company Wininternals Software.

In 2005, Microsoft acquired Wininternals Software, and Mark Russinovich
joined Microsoft. Today he is the CTO of Microsoft Azure

**Question 1**. When did Microsoft acquire the Sysinternals tools?

> ***Answer: 2005***

### Task 2. Install the Sysinternals Suite {#ba89 .graf .graf--h3 .graf-after--blockquote name="ba89"}

Time to get our hands dirty with Sysinternals.

The Sysinternals tool(s) can be downloaded and run from the local
system, or the tool(s) can be run from the web.

Regarding local install/run, you can download the entire suite or just
the tool(s) you need.

If you wish to download a tool or two but not the entire suite, you can
navigate to the **Sysinternals Utilities Index** page,
[https://docs.microsoft.com/en-us/sysinternals/downloads/](https://docs.microsoft.com/en-us/sysinternals/downloads/){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/sysinternals/downloads/"
rel="noopener ugc nofollow noopener" target="_blank"}, and download the
tool(s). If you know which tool you want to download, then this is fine.
The tools are listed in alphabetical order are not separated by
categories.

<figure id="7d81" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*JwK2XKDxHxNNQlhA.png"
class="graf-image" data-image-id="0*JwK2XKDxHxNNQlhA.png"
data-width="875" data-height="376" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Alternatively, you can use the category links to find and download the
tool(s). This route is better since there are so many tools you can
focus on all the tools of interest instead of the entire index.

For example, let's say you need tools to inspect Windows processes;
then, you can navigate to the **Process Utilities** page,
[https://docs.microsoft.com/en-us/sysinternals/downloads/process-utilities/](https://docs.microsoft.com/en-us/sysinternals/downloads/process-utilities/){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/sysinternals/downloads/process-utilities/"
rel="noopener ugc nofollow noopener" target="_blank"}, for all the tools
that fall under this category.

<figure id="1da5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oNu9R7NxMTUQ2YWl.png"
class="graf-image" data-image-id="0*oNu9R7NxMTUQ2YWl.png"
data-width="875" data-height="517" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Notice that you are conveniently supplied with a brief explanation for
each tool.

Lastly, you can do the same from the Sysinternals Live URL,
[https://live.sysinternals.com/](https://live.sysinternals.com/){.markup--anchor
.markup--p-anchor data-href="https://live.sysinternals.com/"
rel="noopener ugc nofollow noopener" target="_blank"}. This is the same
URL to use if you wish to run the tool from the web. We will look at how
to accomplish this in the next section.

If you chose to download from this page, it is similar to the
Sysinternals Utilities Index page. The tools are listed in alphabetical
order and are not separated by categories.

<figure id="a00b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hXBmJMKtSpgCxIlZ.png"
class="graf-image" data-image-id="0*hXBmJMKtSpgCxIlZ.png"
data-width="547" data-height="275" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

If you wish to download the Sysinternals Suite, you can download the zip
file from
[here](https://docs.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite){.markup--anchor
.markup--p-anchor
data-href="https://docs.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite"
rel="noopener ugc nofollow noopener" target="_blank"}.

The suite has a select number of Sysinternal tools. See below for a
rundown of the tools included in the suite.

<figure id="a8af" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*38tcTF3H46dL_j3a.png"
class="graf-image" data-image-id="0*38tcTF3H46dL_j3a.png"
data-width="875" data-height="166" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

After you download the zip file, you need to extract the files. After
the files are extracted, the extra step, which is by choice, is to add
the folder path to the environment variables. By doing so, you can
launch the tools via the command line without navigating to the
directory the tools reside in.

**Environment Variables** can be edited from **System Properties**.

The System Properties can be launched via the command line by running
**sysdm.cpl** . Click on the **Advanced** **tab.**

<figure id="5a53" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xoT9BIKO02HYMUHR.png"
class="graf-image" data-image-id="0*xoT9BIKO02HYMUHR.png"
data-width="463" data-height="525" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Select **Path** under **System Variables** and select Edit... then OK.

<figure id="fdcc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*f8PFgF18EryvvrJf.png"
class="graf-image" data-image-id="0*f8PFgF18EryvvrJf.png"
data-width="603" data-height="237" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

In the next screen select **`New`{.markup--code .markup--p-code}** and
enter the folder path where the Sysinternals Suite was extracted to.
Press OK to confirm the changes.

<figure id="0b82" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rYwcfxUIQtNKff5h.png"
class="graf-image" data-image-id="0*rYwcfxUIQtNKff5h.png"
data-width="526" data-height="190" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Open a new command prompt (elevated) to confirm that the Sysinternals
Suite can be executed from any location.

<figure id="fcb5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xGT65ZDFB-V8q7Pc.png"
class="graf-image" data-image-id="0*xGT65ZDFB-V8q7Pc.png"
data-width="592" data-height="384" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

A local copy of the Sysinternals Suite is located in
**C:\\Tools\\Sysint**.

Alternatively, a PowerShell module can download and install all of the
Sysinternals tools.

- [PowerShell command: **Download-SysInternalsTools
  C:\\Tools\\Sysint**]{#ecfa}

Now let's look at how to run the Sysinternals tools from the web.

**Question 2.** What is the last tool listed within the Sysinternals
Suite?

> ***Answer: zoomIt***

### Task 3. Using Sysinternals Live {#afe1 .graf .graf--h3 .graf-after--blockquote name="afe1"}

Per the Sysinternals website, "Sysinternals Live is a service that
enables you to execute Sysinternals tools directly from the Web without
hunting for and manually downloading them. Simply enter a tool's
Sysinternals Live path into Windows Explorer or a command prompt as
**live.sysinternals.com/\<toolname\>** or
**\\\\live.sysinternals.com\\tools\\\<toolname\>**."

Let's take a look at how we can do this.

Based on the instructions, to launch Process Monitor from the web the
syntax is **\\\\live.sysinternals.com\\tools\\procmon.exe**.

And it fails.

<figure id="ed08" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1J6Ex5tHTuUtXevh.png"
class="graf-image" data-image-id="0*1J6Ex5tHTuUtXevh.png"
data-width="526" data-height="47" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

To resolve this issue the WebDAV client must be installed and running on
the machine. The WebDAV protocol is what allows a local machine to
access a remote machine running a WebDAV share and perform actions in
it.

On a Windows 10 client, the WebDAV client is installed but the client is
most likely not running. If you try to run a Sysinternals tool it will
fail with a message "The network path was not found."

<figure id="bfa8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zFpw-2FZvUd4M6Ae.png"
class="graf-image" data-image-id="0*zFpw-2FZvUd4M6Ae.png"
data-width="494" data-height="337" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

The service needs to be started before attempting to call any
Sysinternals tool in this fashion.

<figure id="53e3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dnnmhZxJkSfd_508.png"
class="graf-image" data-image-id="0*dnnmhZxJkSfd_508.png"
data-width="372" data-height="81" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Verify it's running before proceeding.

<figure id="f268" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bNyTywTmAamtlWyu.png"
class="graf-image" data-image-id="0*bNyTywTmAamtlWyu.png"
data-width="600" data-height="88" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Also, **Network Discovery** needs to be enabled as well. This setting
can be enabled in the **Network and Sharing Center**.

There are a few ways to open the Network and Sharing Center. Here is a
neat command line to launch it.

<figure id="2864" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_7pLZCwGqK6fTzty.png"
class="graf-image" data-image-id="0*_7pLZCwGqK6fTzty.png"
data-width="608" data-height="21" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Click on **Change advanced sharing settings** and select **Turn on
network discovery** for your current network profile.

The attached VM is a Windows Server 2019 edition. The WebDAV client is
not installed by default.

The feature to install on Windows Server is **WebDAV Redirector**. This
feature can be installed via **Server Manager** or using **PowerShell**.

To install with **PowerShell, Install-WindowsFeature WebDAV-Redirector
--Restart**. The server needs to reboot for the installation to
complete.

After reboot, the installation can be verified with the following
PowerShell command, **Get-WindowsFeature WebDAV-Redirector \|
Format-Table --Autosize.**

<figure id="0ade" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ZpI-cexAVkKxMYVA.png"
class="graf-image" data-image-id="0*ZpI-cexAVkKxMYVA.png"
data-width="714" data-height="88" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

The same process as with a Windows 10 client applies from this point:

- [Make sure the WebClient service is running]{#5bf3}
- [Make sure Network Discovery is enabled]{#0e21}

Now with all the necessary components installed and enabled the local
machine is ready to run Sysinternals tools from the web.

There are 2 ways the tools can be run:

- [Run the tool from the command line (as shown above from the Windows
  10 machine)]{#d820}
- [Create a network drive and run the tool from the mapped drive]{#6716}

Method 1 --- Run tool from command line

<figure id="0d3b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WJHwdIA4QhYXxeiL.png"
class="graf-image" data-image-id="0*WJHwdIA4QhYXxeiL.png"
data-width="874" data-height="416" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Method 2 --- Run tool from a mapped drive

<figure id="f197" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ywoMulVT6OUlgJMS.png"
class="graf-image" data-image-id="0*ywoMulVT6OUlgJMS.png"
data-width="517" data-height="85" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

**Note**: The asterick will auto-assign a drive letter. The asterick can
be replaced with an actual drive letter instead.

<figure id="5523" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*siYUr4WmXAC93lrf.png"
class="graf-image" data-image-id="0*siYUr4WmXAC93lrf.png"
data-width="273" data-height="103" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

The website is now browsable within the local machine.

<figure id="1219" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LZcNjXeO7etnWT8C.png"
class="graf-image" data-image-id="0*LZcNjXeO7etnWT8C.png"
data-width="450" data-height="221" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="d010" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DOhxvvjfPz50jd0N.png"
class="graf-image" data-image-id="0*DOhxvvjfPz50jd0N.png"
data-width="523" data-height="246" />
</figure>

[https://tryhackme.com/room/btsysinternalssg](https://tryhackme.com/room/btsysinternalssg){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/btsysinternalssg"
rel="noopener ugc nofollow noopener" target="_blank"}

Now that we got that out of the way time to start exploring some of
these tools.

**Question 3**. What service needs to be enabled on the local host to
interact with live.sysinternals.com?

> ***Answer: webclient***

### Task 4. File and Disk Utilities {#29f7 .graf .graf--h3 .graf-after--blockquote name="29f7"}

**Streams**

"The NTFS file system provides applications the ability to create
alternate data streams of information. By default, all data is stored in
a file's main unnamed data stream, but by using the syntax
'file:stream', you are able to read and write to alternates."
(**official definition**)

**Alternate Data Streams** (ADS) is a file attribute specific to Windows
**NTFS** (New Technology File System). Every file has at least one data
stream (\$DATA) and ADS allows files to contain more than one stream of
data. Natively Window Explorer doesn't display ADS to the user. There
are 3rd party executables that can be used to view this data, but
Powershell gives you the ability to view ADS for files.

Malware writers have used ADS to hide data in an endpoint, but not all
its uses are malicious. When you download a file from the Internet unto
an endpoint, there are identifiers written to ADS to identify that it
was downloaded from the Internet.

**Question 3**. There is a txt file on the desktop named file.txt. What
is the text within the ADS?

<figure id="4d7a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YcAFnzG__j4PGNWj.png"
class="graf-image" data-image-id="0*YcAFnzG__j4PGNWj.png"
data-width="677" data-height="458" />
</figure>

> ***Answer: i am hidding in the stream.***

Question 4. Using WHOIS tools, what is the ISP/Organization for the
remote address in the screenshots below?

<figure id="1b4a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jw2J9PACxdI3LK5h.png"
class="graf-image" data-image-id="0*jw2J9PACxdI3LK5h.png"
data-width="875" data-height="153" />
</figure>

ip=52.154.170.73

<figure id="e1e7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dSND8T1uht_VdS4H.png"
class="graf-image" data-image-id="0*dSND8T1uht_VdS4H.png"
data-width="726" data-height="492" />
</figure>

[https://www.whatismyip.com/ip-address-lookup/](https://www.whatismyip.com/ip-address-lookup/){.markup--anchor
.markup--p-anchor
data-href="https://www.whatismyip.com/ip-address-lookup/"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: Microsoft Corporation***

### Task 6. Process Utilities {#28e5 .graf .graf--h3 .graf-after--blockquote name="28e5"}

Run Autoruns and inspect what are the new entries in the Image Hijacks
tab compared to the screenshots above.

**Question 1**. What entry was updated?

> ***Answer: taskmgr.exe***

**Question 2**. What is the updated value?

Right click on taskmgr.exe to jump to entry now right click on debugger
and modify

<figure id="0d5f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UiUD2xJWtc84sszF.png"
class="graf-image" data-image-id="0*UiUD2xJWtc84sszF.png"
data-width="875" data-height="433" />
</figure>

> ***Answer: C:\\TOOLS\\SYSINT\\PROCEXP.EXE***

Question 1. Run the Strings tool on ZoomIt.exe. What is the full path to
the .pdb file?

<figure id="dcab" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ajL1CVup34X6twZB.png"
class="graf-image" data-image-id="0*ajL1CVup34X6twZB.png"
data-width="779" data-height="347" />
</figure>

> ***Answer: C:\\agent\\\_work\\112\\s\\Win32\\Release\\ZoomIt.pdb***

When you read the Sysinternals documentation, it might hint these tools
are for troubleshooting purposes only, but that is not entirely the
case.

You should know or be familiar with the Sysinternals tools whether
you're a Desktop Engineer, Systems Analyst, or Security Engineer.

**Real-world scenario**: As a security engineer, I had to work with
vendors to troubleshoot why an agent wasn't responding on an
endpoint --- the tools used were **ProcExp**, **ProcMon**, and
**ProcDump**.

- [ProcExp = to inspect the agent process, its properties, and
  associated threads and handles.]{#74e2}
- [ProcMon = to investigate if there were any indicators on why the
  agent was not operating as it should.]{#6156}
- [ProcDump = to create a dump of the agent process to send to the
  vendor for further analysis.]{#bd2c}

And guess what? Asking questions about Sysinternals became part of the
interview questions when hiring additional staff.

Remember, red teamers and adversaries even use these tools.

Below are some additional links to further your knowledge on how to use
these tools as a Security Analyst, Security Engineer, or even an
Incident Responder:

- [Mark's
  Blog --- [https://docs.microsoft.com/en-us/archive/blogs/markrussinovich/](https://docs.microsoft.com/en-us/archive/blogs/markrussinovich/){.markup--anchor
  .markup--li-anchor
  data-href="https://docs.microsoft.com/en-us/archive/blogs/markrussinovich/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#86a8}
- [Windows Blog
  Archive --- [https://techcommunity.microsoft.com/t5/windows-blog-archive/bg-p/Windows-Blog-Archive/label-name/Mark%20Russinovich](https://techcommunity.microsoft.com/t5/windows-blog-archive/bg-p/Windows-Blog-Archive/label-name/Mark%20Russinovich){.markup--anchor
  .markup--li-anchor
  data-href="https://techcommunity.microsoft.com/t5/windows-blog-archive/bg-p/Windows-Blog-Archive/label-name/Mark%20Russinovich"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#c80a}
- [License to Kill: Malware Hunting with Sysinternals
  Tools --- [https://www.youtube.com/watch?v=A_TPZxuTzBU](https://www.youtube.com/watch?v=A_TPZxuTzBU){.markup--anchor
  .markup--li-anchor
  data-href="https://www.youtube.com/watch?v=A_TPZxuTzBU"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#9c39}
- [Malware Hunting with Mark Russinovich and the Sysinternals
  Tools --- [https://www.youtube.com/watch?v=vW8eAqZyWeo](https://www.youtube.com/watch?v=vW8eAqZyWeo){.markup--anchor
  .markup--li-anchor
  data-href="https://www.youtube.com/watch?v=vW8eAqZyWeo"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#3c54}

### Promote and Collaborate on Cybersecurity Insights {#5383 .graf .graf--h3 .graf-after--li name="5383"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#6cfc .graf .graf--h3 .graf-after--p name="6cfc"}

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
.h-card} on [September 3, 2024](https://medium.com/p/cd77b6ed8b01).

[Canonical
link](https://medium.com/@bevijaygupta/sysinternals-tryhackme-writeup-cd77b6ed8b01){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
