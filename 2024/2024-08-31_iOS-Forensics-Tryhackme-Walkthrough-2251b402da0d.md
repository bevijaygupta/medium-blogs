::: {}
# iOS Forensics Tryhackme Walkthrough {#ios-forensics-tryhackme-walkthrough .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/malstrings Note: This room is for
Premium Members Only. who purchased THM premium membership.
:::

::::::: {.section .e-content field="body"}
:::::: {#8b2f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### iOS Forensics Tryhackme Walkthrough {#81d6 .graf .graf--h3 .graf--leading .graf--title name="81d6"}

<figure id="b96e" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*u1-rv-9H8XhB2fSy.png"
class="graf-image" data-image-id="0*u1-rv-9H8XhB2fSy.png"
data-width="875" data-height="372" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/malstrings](https://tryhackme.com/room/malstrings){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/malstrings"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is for Premium Members Only. who purchased THM premium
membership.**

### Task 2. What is Digital Forensics and how is it Used Today? {#1898 .graf .graf--h3 .graf-after--p name="1898"}

**Question 1**. What would look more suspicious? **an empty hard drive**
or **a full hard drive**?

> ***Answer: an empty hard drive***

**Question 2**. What is the definition for an abstract view of a hard
drive?

> ***Answer: image***

### Task 6. Data Acquisition & Trust Certificates {#e39f .graf .graf--h3 .graf-after--blockquote name="e39f"}

Question 1. What is the name of a forensics tool that couldn't be used
in a court of law, because data could be written to the device being
analysed?

> ***Answer: iFunbox***

**Question 2**. You've found an iPhone with no passcode lock, what
acquisition method would you use?

> ***Answer: direct Acquisition***

**Question 3**. What is the name of the certificate that gets stored on
a computer when it becomes trusted?

> ***Answer: trust certificate***

### Task 9. Scenario: Operation JustEncase (Deploy) {#b07c .graf .graf--h3 .graf-after--blockquote name="b07c"}

Access in Browser

<figure id="9fc0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xeCnGjD3JcCQRNsK.png"
class="graf-image" data-image-id="0*xeCnGjD3JcCQRNsK.png"
data-width="532" data-height="603" />
</figure>

Open **DB Browser (SQLite)**

and click on open database option and select sms db file

<figure id="3b03" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jRUn1q-TdTKwSDeL.png"
class="graf-image" data-image-id="0*jRUn1q-TdTKwSDeL.png"
data-width="875" data-height="502" />
</figure>

Now click on **Browse data** option

<figure id="fa2f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*smp_9nojoBYLUH0n.png"
class="graf-image" data-image-id="0*smp_9nojoBYLUH0n.png"
data-width="687" data-height="499" />
</figure>

And select message

<figure id="0fde" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jeAKJrZdxf1LNWPl.png"
class="graf-image" data-image-id="0*jeAKJrZdxf1LNWPl.png"
data-width="575" data-height="501" />
</figure>

You will see two messages

<figure id="10ec" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*252vUUNZpJyLYO9A.png"
class="graf-image" data-image-id="0*252vUUNZpJyLYO9A.png"
data-width="784" data-height="365" />
</figure>

<figure id="01c8" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*w59Hz7qA6o0BAKuS.png"
class="graf-image" data-image-id="0*w59Hz7qA6o0BAKuS.png"
data-width="517" data-height="256" />
</figure>

**Question 1**. Who was the recepient of the SMS message sent on 23rd of
August 2020?

> ***Answer: Lewis Randall***

**Question 2**. What did the SMS message say?

> ***Answer: Did you get the goods?***

**Question 3**. Looking at the address book, what is the first name of
the other person in the contacts?

<figure id="0f4a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MEFwQfh2Wu7hAMV4.png"
class="graf-image" data-image-id="0*MEFwQfh2Wu7hAMV4.png"
data-width="379" data-height="142" />
</figure>

Now drag and drop first file, Right click on **ABPerson** select
**Browse Table**

<figure id="dbb3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kkaUgryGMCSw1DJa.png"
class="graf-image" data-image-id="0*kkaUgryGMCSw1DJa.png"
data-width="760" data-height="474" />
</figure>

<figure id="dc95" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*__ygbbxbqvkCIK-7.png"
class="graf-image" data-image-id="0*__ygbbxbqvkCIK-7.png"
data-width="555" data-height="302" />
</figure>

> ***Answer: Jenny***

**Question 4**. Following on from Question #3, what is their listed
"Organization"

<figure id="6fd5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nVc1GFudule0CHpf.png"
class="graf-image" data-image-id="0*nVc1GFudule0CHpf.png"
data-width="512" data-height="254" />
</figure>

> ***Answer: Transportation***

**Question 5**. Investigate their browsing history, what is the address
of the website that they have bookmarked?

drag and drop **Bookmarks** file into **Browse data** option

<figure id="dccb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Z7FEQMMLwq1gj6ME.png"
class="graf-image" data-image-id="0*Z7FEQMMLwq1gj6ME.png"
data-width="854" data-height="522" />
</figure>

Right click on **Bookmarks** and select **Browse Table**

<figure id="2697" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MR_8c0E6-Ao9sK-e.png"
class="graf-image" data-image-id="0*MR_8c0E6-Ao9sK-e.png"
data-width="503" data-height="469" />
</figure>

<figure id="5036" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*QkdIsbffdmSBXM5Z.png"
class="graf-image" data-image-id="0*QkdIsbffdmSBXM5Z.png"
data-width="499" data-height="225" />
</figure>

> ***Answer:***
> [***https://blog.cmnatic.co.uk***](https://blog.cmnatic.co.uk/){.markup--anchor
> .markup--blockquote-anchor data-href="https://blog.cmnatic.co.uk/"
> rel="noopener ugc nofollow noopener" target="_blank"}

**Question 6**. The suspected received an email, what is the
**remote_id** of the sender?

drag and drop **Envelope Index** file into **Browse Data** tab

<figure id="6874" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OGn4e0JJpr1oUlyl.png"
class="graf-image" data-image-id="0*OGn4e0JJpr1oUlyl.png"
data-width="852" data-height="497" />
</figure>

<figure id="6881" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*51LhDeyX9hPYsAML.png"
class="graf-image" data-image-id="0*51LhDeyX9hPYsAML.png"
data-width="506" data-height="364" />
</figure>

> ***Answer: 51.32.56.12***

**Question 7**. What is the name of the company on one of the images
stored on the suspects phone?

<figure id="e432" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TR6Sw0U4eA2it_of.png"
class="graf-image" data-image-id="0*TR6Sw0U4eA2it_of.png"
data-width="669" data-height="155" />
</figure>

> ***Answer: Tryhackme***

**Question 8.** What is the value of the cookie that was left behind?

Open the Second file with Notepad++

<figure id="615b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8mtgiBd5lQ5jac6W.png"
class="graf-image" data-image-id="0*8mtgiBd5lQ5jac6W.png"
data-width="637" data-height="496" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#cfa7 .graf .graf--h3 .graf-after--figure name="cfa7"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#0838 .graf .graf--h3 .graf-after--p name="0838"}

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
.h-card} on [August 31, 2024](https://medium.com/p/2251b402da0d).

[Canonical
link](https://medium.com/@bevijaygupta/ios-forensics-tryhackme-walkthrough-2251b402da0d){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
