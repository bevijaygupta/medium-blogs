::: {}
# MAL: REMnux The Redux TryHackme {#mal-remnux-the-redux-tryhackme .p-name}
:::

::: {.section .p-summary field="subtitle"}
https://tryhackme.com/room/malremnuxv2
:::

::::::: {.section .e-content field="body"}
:::::: {#b672 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### MAL: REMnux The Redux TryHackme {#e10f .graf .graf--h3 .graf--leading .graf--title name="e10f"}

<figure id="2b92" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*ga4-GkcM4sE8SfNT.png"
class="graf-image" data-image-id="0*ga4-GkcM4sE8SfNT.png"
data-width="697" data-height="238" data-is-featured="true" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

### What we learn in this room {#b417 .graf .graf--h3 .graf-after--p name="b417"}

- [Identifying and analysing malicious payloads of various formats
  embedded in PDF's, EXE's and Microsoft Office Macros (the most common
  method that malware developers use to spread malware today)]{#1ca3}
- [Learning how to identify obfuscated code and packed files --- and in
  turn --- analyse these.]{#3769}
- [Analysing the memory dump of a PC that became infected with the
  Jigsaw ransomware in the real-world using Volatility.]{#31d6}

IP Address: 10.10.32.28\
Username: **remnux**\
Password: **malware**

``` {#1d9c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
ssh remnux@10.10.32.28
```

<figure id="dd12" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*BM6VliBHY0wRGXFA.png"
class="graf-image" data-image-id="0*BM6VliBHY0wRGXFA.png"
data-width="395" data-height="164" />
</figure>

### Task 3. Analysing Malicious PDF's {#8b4a .graf .graf--h3 .graf-after--figure name="8b4a"}

**Question 1**. How many types of categories of "Suspicious elements"
are there in "notsuspicious.pdf"

<figure id="2aae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*061zeWtc7pKy2tZf.png"
class="graf-image" data-image-id="0*061zeWtc7pKy2tZf.png"
data-width="712" data-height="578" />
</figure>

> ***Answer: 3***

**Question 2**. Use peepdf to extract the javascript from
"notsuspicious.pdf". What is the flag?

Note the output confirming that there's Javascript present, but also how
it is executed? OpenAction will execute the code when the PDF is
launched.\
To extract this Javascript, we can use peepdf's "extract" module. This
requires a few steps to set up but is fairly trivial.\
The following command will create a script file for peepdf to use:

<figure id="c9d9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QpW7d3ed4PfwGNXP.png"
class="graf-image" data-image-id="0*QpW7d3ed4PfwGNXP.png"
data-width="875" data-height="82" />
</figure>

The script will extract all javascript via extract js and pipe \> the
contents into "javascript-from-notsuspicious.pdf"\
We now need to tell peepdf the name of the script
(extracted_javascript.txt) and the PDF file that we want to extract from
(notsuspicious.pdf):

<figure id="99bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5kFKS_MvVKht17GI.png"
class="graf-image" data-image-id="0*5kFKS_MvVKht17GI.png"
data-width="875" data-height="103" />
</figure>

Remembering that the Javascript will output into a file called
"javascript-from-demo_nonsuspicious.pdf" because of our script.\
To recap: "extracted_javascript.txt" (highlighted in red) is our script,
where "notsuspicious.pdf" (highlighted in green) is the original PDF
file that we think is malicious.

<figure id="c5ac" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VVs2l4_qNk6V2SFc.png"
class="graf-image" data-image-id="0*VVs2l4_qNk6V2SFc.png"
data-width="806" data-height="103" />
</figure>

**Question 3**.How many types of categories of "Suspicious elements" are
there in "advert.pdf"

Now Run this command **peepdf advert.pdf**

<figure id="4ca4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*onS_h8TNEod8v7U2.png"
class="graf-image" data-image-id="0*onS_h8TNEod8v7U2.png"
data-width="508" data-height="272" />
</figure>

> ***Answer: 6***

**Question 4**. Now use peepdf to extract the javascript from
"advert.pdf". What is the value of "cName"?

<figure id="54a8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TzStotj3RexA00sl.png"
class="graf-image" data-image-id="0*TzStotj3RexA00sl.png"
data-width="875" data-height="236" />
</figure>

> ***Answer: notsuspicious***

### Task 4. Analysing Malicious Microsoft Office Macros {#2d57 .graf .graf--h3 .graf-after--blockquote name="2d57"}

**Question 1**. What is the name of the Macro for
"DefinitelyALegitInvoice.doc"

<figure id="e624" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FntUD9r-DpSKiT9u.png"
class="graf-image" data-image-id="0*FntUD9r-DpSKiT9u.png"
data-width="732" data-height="360" />
</figure>

<figure id="11ee" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qQc1gXoaAgQXe__V.png"
class="graf-image" data-image-id="0*qQc1gXoaAgQXe__V.png"
data-width="793" data-height="382" />
</figure>

> ***Answer: DefoLegit***

**Question 2**. What is the URL the Macro in "Taxes2020.doc" would try
to launch?

<figure id="d6ec" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QxCpwMHevXLNct92.png"
class="graf-image" data-image-id="0*QxCpwMHevXLNct92.png"
data-width="716" data-height="245" />
</figure>

<figure id="7c29" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ane98Ji4uLJagul5.png"
class="graf-image" data-image-id="0*ane98Ji4uLJagul5.png"
data-width="658" data-height="201" />
</figure>

> ***Answer:***
> [***http://tryhackme.com/notac2cserver.sh***](http://tryhackme.com/notac2cserver.sh){.markup--anchor
> .markup--blockquote-anchor
> data-href="http://tryhackme.com/notac2cserver.sh"
> rel="noopener ugc nofollow noopener" target="_blank"}

### Task 5. I Hope You Packed Your Bags {#74f3 .graf .graf--h3 .graf-after--blockquote name="74f3"}

But first: Entropy 101

There's a reason why I've waited until now to discuss file entropy in
the malware series.

REMnux provides a nice range of command-line tools that allow for bulk
or semi-automated classification and static analysis. File entropy is
very indicative of the suspiciousness of a file and is a prominent
characteristic that these tools look for within a Portable Executable
(PE).

At it's very simplest, file entropy is a rating that scores how random
the data within a PE file is. With a scale of 0 to 8. 0 meaning the less
"randomness" of the data in the file, where a scoring towards 8
indicates this data is more "random".

For example, files that are encrypted will have a very high entropy
score. Where files that have large chunks of the same data such as
"1\'s" will have a low entropy score.

Okay...so?

Malware authors use techniques such as encryption or packing (we'll come
onto this next) to obfuscate their code and to attempt to bypass
anti-virus. Because of this, these files will have high entropy. If an
analyst had 1,000 files, they could rank the files by their entropy
scoring, of course, the files with the higher entropy should be analysed
first.

To illustrate, this file would have a low entropy because the data has a
pattern to it.

<figure id="8608" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*o6cCF621nQbXBLOD.png"
class="graf-image" data-image-id="0*o6cCF621nQbXBLOD.png"
data-width="559" data-height="225" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

Whereas however, this file would have a high entropy because there's no
pattern to the data --- it's a lot more random in comparison.

<figure id="df40" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2DmvRtiApv5d-eJj.png"
class="graf-image" data-image-id="0*2DmvRtiApv5d-eJj.png"
data-width="577" data-height="136" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

Packing and Unpacking

I briefly discussed this in my [MAL:
Introductory](https://tryhackme.com/room/malmalintroductory){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/malmalintroductory"
rel="noopener ugc nofollow noopener" target="_blank"} room, but that
doesn't do this topic justice.

We'll start with a bit of theory (so bare with me here) on how packing
works and why it's used. Packer's use an executable as a source and
output's it to another executable. This executable will have had some
modifications made depending on the packer. For example, the new
executable could be compressed and/or obfuscated by using mathematics.

Legitimate software developers use packing to reduce the size of their
applications and to ultimately protect their work from being stolen. It
is, however, a double-edged sword, malware authors reap the benefits of
packing to make the reverse engineering and detection of the code hard
to impossible.

Executables have what's called an entry point. When launched, this entry
point is simply the location of the first pieces of code to be executed
within the file --- as illustrated below:

<figure id="fbe8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*KNzk4_Fwfgp_7HSd.png"
class="graf-image" data-image-id="0*KNzk4_Fwfgp_7HSd.png"
data-width="604" data-height="473" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

*(Sikorski and Honig, 2012)*

When an executable is packed, it must unpack itself before any code can
execute. Because of this, packers change the entry point from the
original location to what's called the "Unpacking Stub".

<figure id="a809" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*_2OqeRPJrzfEex0Z.png"
class="graf-image" data-image-id="0*_2OqeRPJrzfEex0Z.png"
data-width="587" data-height="260" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

*(Sikorski and Honig, 2012)*

The "Unpacking Stub" will begin to unpack the executable into its
original state. Once the program is fully unpacked, the entry point will
now relocate back to its normal place to begin executing code:

<figure id="a4ce" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EdZgs3S0TSw90T4_.png"
class="graf-image" data-image-id="0*EdZgs3S0TSw90T4_.png"
data-width="539" data-height="545" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

*(Sikorski and Honig, 2012)*

It is only at this point can an analyst begin to understand what the
executable is doing as it is now in it's true, original form.

Determining if an Executable is Packed

Don't worry, learning how to manually unpack an executable is
out-of-scope for this pathway. We have a few tools at our arsenal that
should do a sufficient job for most of the samples we come across in the
wild.

Packed files have a few characteristics that may indicate whether or not
they are packed:

- [Remember about file entropy? Packed files will have a high
  entropy!]{#14a9}
- [There are very few "Imports", packed files may only have
  "GetProcAddress" and "LoadLibrary".]{#9959}
- [The executable may have sections named after certain packers such as
  UPX.]{#f1c2}

Demonstration

I have two copies of my application, one not packed and another has been
packed.

Below we can see that this copy has 34 imports, so a noticeable amount
and the imports are quite revealing in what we can expect the
application to do:

<figure id="2f56" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*yH2_t8zMpQo5y0M9.png"
class="graf-image" data-image-id="0*yH2_t8zMpQo5y0M9.png"
data-width="351" data-height="385" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

Whereas the other copy only presents us with 6 imports.

<figure id="d02a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*7k7LJq0nUQuVvX_D.png"
class="graf-image" data-image-id="0*7k7LJq0nUQuVvX_D.png"
data-width="198" data-height="140" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

We can verify that this was packed using UPX via tools such as
[PEID](https://www.aldeid.com/wiki/PEiD){.markup--anchor
.markup--p-anchor data-href="https://www.aldeid.com/wiki/PEiD"
rel="noopener ugc nofollow noopener" target="_blank"}, or by manually
comparing the executables sections and filesize differences.

<figure id="8bf7" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*494blc7Oqk4cYkUy.png"
class="graf-image" data-image-id="0*494blc7Oqk4cYkUy.png"
data-width="622" data-height="78" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

Look at that entropy! **7.526** out of **8**! Also, note the name of the
sections. `UPX0`{.markup--code .markup--p-code} and the entry point
being at `UPX1`{.markup--code .markup--p-code}\...that\'s our packer.

<figure id="a9ad" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bPXBrHc5MEyAnQ5j.png"
class="graf-image" data-image-id="0*bPXBrHc5MEyAnQ5j.png"
data-width="510" data-height="107" />
</figure>

[https://tryhackme.com/room/malremnuxv2](https://tryhackme.com/room/malremnuxv2){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malremnuxv2"
rel="noopener ugc nofollow noopener" target="_blank"}

Question 1. What is the highest file entropy a file can have?

> ***Answer: 8***

Question 2. What is the lowest file entropy a file can have?

> ***Answer: 0***

**Question 3**. Name a common packer that can be used for applications?

> ***Answer: UPX***

**Additional Reading**

[A Look At Entropy
Analysis](https://fsec404.github.io/blog/Shanon-entropy/){.markup--anchor
.markup--p-anchor
data-href="https://fsec404.github.io/blog/Shanon-entropy/"
rel="noopener ugc nofollow noopener" target="_blank"}

[\[BlackHat 2019\] Investigating Malware Using Memory Forensics
(Video)](https://www.youtube.com/watch?v=BMFCdAGxVN4){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com/watch?v=BMFCdAGxVN4"
rel="noopener ugc nofollow noopener" target="_blank"}

[Malware Threat Report --- Q2 2020
(Avira)](https://www.avira.com/en/blog/malware-threat-report-q2-2020-statistics-and-trends){.markup--anchor
.markup--p-anchor
data-href="https://www.avira.com/en/blog/malware-threat-report-q2-2020-statistics-and-trends"
rel="noopener ugc nofollow noopener" target="_blank"}

[Malware Detection in PDF and Office Documents: A
survey](https://api.semanticscholar.org/CorpusID:212680542%20%28P.%20Singh,%20S.%20Tapaswi,%20S.Gupta%29){.markup--anchor
.markup--p-anchor
data-href="https://api.semanticscholar.org/CorpusID:212680542%20(P.%20Singh,%20S.%20Tapaswi,%20S.Gupta)"
rel="noopener ugc nofollow noopener" target="_blank"}

**Cheatsheets**

[REMnux 7.0 Documentation](https://docs.remnux.org/){.markup--anchor
.markup--p-anchor data-href="https://docs.remnux.org/"
rel="noopener ugc nofollow noopener" target="_blank"}

[Volatility 2.4. Windows & Linux Profile
Cheatsheets](https://downloads.volatilityfoundation.org/releases/2.4/CheatSheet_v2.4.pdf){.markup--anchor
.markup--p-anchor
data-href="https://downloads.volatilityfoundation.org/releases/2.4/CheatSheet_v2.4.pdf"
rel="noopener ugc nofollow noopener" target="_blank"}

### Promote and Collaborate on Cybersecurity Insights {#ee15 .graf .graf--h3 .graf-after--p name="ee15"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#433b .graf .graf--h3 .graf-after--p name="433b"}

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
.h-card} on [September 4, 2024](https://medium.com/p/60af53271100).

[Canonical
link](https://medium.com/@bevijaygupta/mal-remnux-the-redux-tryhackme-60af53271100){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
