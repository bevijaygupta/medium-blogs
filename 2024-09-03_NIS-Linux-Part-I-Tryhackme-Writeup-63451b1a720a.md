::: {}
# NIS Linux Part I Tryhackme Writeup {#nis-linux-part-i-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/nislinuxone Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#c0d2 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### NIS Linux Part I Tryhackme Writeup {#607e .graf .graf--h3 .graf--leading .graf--title name="607e"}

<figure id="8335" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*oLPk1BMDmMXU7KKT.png"
class="graf-image" data-image-id="0*oLPk1BMDmMXU7KKT.png"
data-width="558" data-height="225" />
</figure>

**Room link:**
[https://tryhackme.com/room/nislinuxone](https://tryhackme.com/room/nislinuxone){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/nislinuxone"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### Task 1. What is this room about? {#703e .graf .graf--h3 .graf-after--p name="703e"}

<figure id="e763" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*oR3mGdyH-1JRLAxH.png"
class="graf-image" data-image-id="0*oR3mGdyH-1JRLAxH.png"
data-width="875" data-height="176" />
</figure>

As per the Tryhackme Rules i can't show you password/hash/flag

if you want to know password complete these rooms

[Linux Fundamentals Part
1](https://tryhackme.com/room/linux1){.markup--anchor .markup--p-anchor
data-href="https://tryhackme.com/room/linux1"
rel="noopener ugc nofollow noopener" target="_blank"}

[Linux Fundamentals Part
2](https://tryhackme.com/room/linux2){.markup--anchor .markup--p-anchor
data-href="https://tryhackme.com/room/linux2"
rel="noopener ugc nofollow noopener" target="_blank"}

[Linux Fundamentals Part
3](https://tryhackme.com/room/linux3){.markup--anchor .markup--p-anchor
data-href="https://tryhackme.com/room/linux3"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 2. ls {#26f4 .graf .graf--h3 .graf-after--p name="26f4"}

**Question 1**. How do you run the ls command?

> ***Answer: ls***

**Question 2.** How do you run the ls command to show all the files
inside the folder?

> ***Answer: ls -a***

**Question 3.** How do you run the ls command to not show the current
directory and the previous directory in the output? (almost everything)

> ***Answer: ls -a***

**Question 4.** How do you show the information in a long listing format
using ls?

> ***Answer: ls -l***

**Question 5.** How do you show the size in readable format? e.g. k, Mb,
etc

> ***Answer: ls -h***

**Question 6.** How do you do a recursive ls?

> ***Answer: ls --- recursive***

**Question 7.** How many files did you locate in the home folder of the
user?(non-hidden and not inside other folders)

> ***Answer: 13***

### Task 3. cat {#7794 .graf .graf--h3 .graf-after--blockquote name="7794"}

**Question 1.** What is the content of cat.txt?

> ***Answer: THM{11adbee391acdffee901}***

**Question 2.** What is the content of tac.txt?

> ***Answer: THM{acab0111aaa687912139}***

**Question 3.** What is the content of head.txt?

> ***Answer: THM{894abac55f7962abc166}***

**Question 4.** What is the content of tail.txt?

> ***Answer: THM{1689acafdd20751acff6}***

**Question 5.** What is the content of the xxd.txt?

> ***Answer: THM{fac1aab210d6e4410acd}***

**Question 6.** What is the content of base64.txt?

> ***Answer: THM{aa462c1b2d44801c0a31}***

### Task 4. find {#5cb9 .graf .graf--h3 .graf-after--blockquote name="5cb9"}

**Question 1.** How many .txt files did you find in the current folder?

<figure id="b750" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Plwi1dmnzJlWOzUJ.png"
class="graf-image" data-image-id="0*Plwi1dmnzJlWOzUJ.png"
data-width="427" data-height="224" />
</figure>

> ***Answer: 8***

**Question 2.** How many SUID files have you found inside the home
folder?

<figure id="d277" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aTJDNxTYKTa3z4HE.png"
class="graf-image" data-image-id="0*aTJDNxTYKTa3z4HE.png"
data-width="467" data-height="68" />
</figure>

> ***Answer: 0***

### Task 5. grep {#d336 .graf .graf--h3 .graf-after--blockquote name="d336"}

**Question 1.** How many times does the word "hacker" appear in the grep
files? (including variations)

<figure id="e677" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bYb-Ny_XvDw0Miwh.png"
class="graf-image" data-image-id="0*bYb-Ny_XvDw0Miwh.png"
data-width="803" data-height="214" />
</figure>

> ***Answer: 15***

### Task 6. sudo {#1400 .graf .graf--h3 .graf-after--blockquote name="1400"}

**Question 1.** Is the user allowed to run the above command? (Yay/Nay)

> ***Answer: Nay***

### Task 8. echo {#bc97 .graf .graf--h3 .graf-after--blockquote name="bc97"}

**Question 1.** What command would you use to echo the word
"Hackerman" ?

> ***Answer: echo "Hackerman"***

### Task 9. xargs {#0e16 .graf .graf--h3 .graf-after--blockquote name="0e16"}

**Question 1.** How would you read all files with extension .bak using
xargs?

> ***Answer: find / -name \*.bak -type f print \| xargs /bin/cat***

### Task 11. curl {#9f48 .graf .graf--h3 .graf-after--blockquote name="9f48"}

**Question 1.** How would you grab the headers silently of
[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"} but grepping only
the HTTP status code?

> ***Answer: curl -I -s***
> [***https://tryhackme.com***](https://tryhackme.com/){.markup--anchor
> .markup--blockquote-anchor data-href="https://tryhackme.com/"
> rel="noopener ugc nofollow noopener" target="_blank"} ***\| grep
> http***

### Task 12. wget {#f27a .graf .graf--h3 .graf-after--blockquote name="f27a"}

**Question 1.** What command would you run to get the flag.txt from
[https://tryhackme.com/](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"} ?

> ***Answer: wget***
> [***https://tryhackme.com/flag.txt***](https://tryhackme.com/flag.txt){.markup--anchor
> .markup--blockquote-anchor data-href="https://tryhackme.com/flag.txt"
> rel="noopener ugc nofollow noopener" target="_blank"}

**Question 1.** What command would you run to download recursively up to
level 5 from
[https://tryhackme.com](https://tryhackme.com/){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/"
rel="noopener ugc nofollow noopener" target="_blank"} ?

> ***Answer: wget -r -l***
> [***https://tryhackme.com***](https://tryhackme.com/){.markup--anchor
> .markup--blockquote-anchor data-href="https://tryhackme.com/"
> rel="noopener ugc nofollow noopener" target="_blank"}

### Task 13. tar {#bdf1 .graf .graf--h3 .graf-after--blockquote name="bdf1"}

**Question 1.** What is the flag from the tar file?

``` {#caab .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
tar -xf tarball.tar
cat flag.txt
```

> ***Answer: THM{C0FFE1337101}***

### Task 14. gzip {#b318 .graf .graf--h3 .graf-after--blockquote name="b318"}

**Question 1.** What is the content of gzip.txt?

``` {#eca9 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gzip -d gzip.txt.gz
cat gzip.txt
```

> ***Answer: THM{0AFDECC951A}***

### Task 15. 7zip {#5103 .graf .graf--h3 .graf-after--blockquote name="5103"}

**Question 1.** What is the flag inside the 7zip file?

``` {#d458 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
7z x zip.7z
cat 7zip.txt
```

> ***Answer: THM{526accdf94}***

### Task 16. binwalk {#9b29 .graf .graf--h3 .graf-after--blockquote name="9b29"}

**Question 1.** What is the content of binwalk.txt?

``` {#c106 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
binwalk -e binwalk.png
cat _binwalk.png-0.extracted/binwalk.txt
```

> ***Answer: THM{af5548a12bc2de}***

### Promote and Collaborate on Cybersecurity Insights {#a000 .graf .graf--h3 .graf-after--blockquote name="a000"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#aeb4 .graf .graf--h3 .graf-after--p name="aeb4"}

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
.h-card} on [September 3, 2024](https://medium.com/p/63451b1a720a).

[Canonical
link](https://medium.com/@bevijaygupta/nis-linux-part-i-tryhackme-writeup-63451b1a720a){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
