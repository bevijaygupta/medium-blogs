---
title: "WebOSINT Tryhackme Writeup 221e82d0e056"
platform: Medium
original_file: 2024-08-21_WebOSINT-Tryhackme-Writeup-221e82d0e056.md
---

# WebOSINT Tryhackme Writeup 221e82d0e056

::: {}
# WebOSINT Tryhackme Writeup {#webosint-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "WebOSINT"
:::

::::::: {.section .e-content field="body"}
:::::: {#8523 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### WebOSINT Tryhackme Writeup {#a1fa .graf .graf--h3 .graf--leading .graf--title name="a1fa"}

**This is a Writeup of Tryhackme room "WebOSINT"**

<figure id="9b12" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Rh_y7cwzoXBxbyNK.png"
class="graf-image" data-image-id="0*Rh_y7cwzoXBxbyNK.png"
data-width="502" data-height="263" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/webosint](https://tryhackme.com/room/webosint){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/webosint"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

### Task 1: When A Website Does Not Exist {#6cce .graf .graf--h3 .graf-after--p name="6cce"}

What's the first thing you do when you are given the name of a business
to check out? Fire up the ol' web browser, find the website and check it
out, right?

What if the website, or even the entire business, no longer exists?

That does NOT mean it's the end of the road.

OSINT researchers may still be able to connect the dots and find useful
information on such organizations.

Your job is to find as much information as you can about the website
RepublicofKoffee.com.

\<Spoiler alert\> the website doesn't exist, and if it does by the time
you read this, the website in its current form is not our target.

One way to collect information about a website without directly visiting
it is to simply do a search for it.

**Note:** Sometimes plugging a website into the search bar will send you
directly to the site. Avoid this by putting the site in quote marks.
Also note that this will only return results where the full domain name
is written out on the website.

Go ahead and google "**RepublicOfKoffee.com**" with and without quote
marks, just to see what happens.

### Task 2: Whois Registration {#4d1b .graf .graf--h3 .graf-after--p name="4d1b"}

Just because nothing shows up when you visit '**RepublicOfKoffee.com**,'
doesn't mean that someone doesn't own the domain. In fact, if there is
any kind of landing page at all, even a spammy one, then you can be sure
that someone does, in fact, own it. But is it currently owned by the
same person that used it for the time period we are interested in? We
may or may not be able to figure that out, but it's worth a look.

We can confirm current registration status with a whois lookup.

A 'whois' lookup is the most basic form of domain recon available. There
are multiple websites that will do it for you as well.

Personally, I recommend just going directly to
[lookup.icann.org](https://lookup.icann.org/lookup){.markup--anchor
.markup--p-anchor data-href="https://lookup.icann.org/lookup"
rel="noopener ugc nofollow noopener" target="_blank"}. This should tell
you the current hosting company used and name servers. Looking at the
raw data option will show further details.

We're looking for any data we might be able to use as pivot points.
Maybe an email address? Or better yet, a physical address or phone
number?

***Technically*** these are required in order to register any domain,
but most domain registrars offer some kind of privacy protection for a
trivial fee, if not free.

Anyway, let's see what we can find out!

<figure id="69a4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sEExeA8y9_FNKEuZ.png"
class="graf-image" data-image-id="0*sEExeA8y9_FNKEuZ.png"
data-width="874" data-height="669" />
</figure>

[https://tryhackme.com/room/webosint](https://tryhackme.com/room/webosint){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/webosint"
rel="noopener ugc nofollow noopener" target="_blank"}

**Q.1:** What is the name of the company the domain was registered with?

> ***Answer: Namecheap Inc***

**Q.2:** What phone number is listed for the registration company? (do
not include country code or special characters/spaces)

<figure id="4f88" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dP1H2OBcP57pXAX2.png"
class="graf-image" data-image-id="0*dP1H2OBcP57pXAX2.png"
data-width="831" data-height="314" />
</figure>

[https://rdap.verisign.com/com/v1/domain/republicofkoffee.com](https://rdap.verisign.com/com/v1/domain/republicofkoffee.com){.markup--anchor
.markup--p-anchor
data-href="https://rdap.verisign.com/com/v1/domain/republicofkoffee.com"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: 6613102107***

**Q.3:** What is the first nameserver listed for the site?

> ***Answer: DNS1.REGISTRAR-SERVERS.COM***

**Q.4:** What is listed for the name of the registrant?

<figure id="4122" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UUUZubcK65A5-Bep.png"
class="graf-image" data-image-id="0*UUUZubcK65A5-Bep.png"
data-width="714" data-height="339" />
</figure>

[https://rdap.namecheap.com/domain/REPUBLICOFKOFFEE.COM](https://rdap.namecheap.com/domain/REPUBLICOFKOFFEE.COM){.markup--anchor
.markup--p-anchor
data-href="https://rdap.namecheap.com/domain/REPUBLICOFKOFFEE.COM"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: redacted for privacy***

**Q.5:** What country is listed for the registrant?

<figure id="374b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oI55ArgQ8K2vhC3i.png"
class="graf-image" data-image-id="0*oI55ArgQ8K2vhC3i.png"
data-width="652" data-height="263" />
</figure>

[https://rdap.namecheap.com/domain/REPUBLICOFKOFFEE.COM](https://rdap.namecheap.com/domain/REPUBLICOFKOFFEE.COM){.markup--anchor
.markup--p-anchor
data-href="https://rdap.namecheap.com/domain/REPUBLICOFKOFFEE.COM"
rel="noopener ugc nofollow noopener" target="_blank"}

> ***Answer: Panama***

### Task 3: Ghosts of Websites Past {#6afd .graf .graf--h3 .graf-after--blockquote name="6afd"}

Don't be discouraged when your initial searches on a website turn up
empty.

That's where Archive.org and the Internet Wayback Machine come into
play.

Do yourself a favor and install the archive.org browser extension that
will automatically pull up an option to search for a site on the Wayback
Machine when it fails to load in the web browser.

Either with the browser extension, or just by going to archive.org and
searching for it, see what snapshots are available of our target domain,
**RepublicOfKoffee.com.**

Looking at the historical information available for the site, you should
be able to answer the following questions without too much trouble.

We are going to utilize the
[waybackmachine](https://web.archive.org/){.markup--anchor
.markup--p-anchor data-href="https://web.archive.org/"
rel="noopener ugc nofollow noopener" target="_blank"} which holds
archives of websites at different times of the year.

<figure id="7d51" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MJ-7anbmUHYIJGU7.png"
class="graf-image" data-image-id="0*MJ-7anbmUHYIJGU7.png"
data-width="875" data-height="398" />
</figure>

[http://web.archive.org/](http://web.archive.org/){.markup--anchor
.markup--p-anchor data-href="http://web.archive.org/"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="67ed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Lb_QpAitHjz2J2i8.png"
class="graf-image" data-image-id="0*Lb_QpAitHjz2J2i8.png"
data-width="875" data-height="476" />
</figure>

**Q.1:** What is the first name of the blog's author?

<figure id="d410" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*oq7fyFzzOWvWHzFf.png"
class="graf-image" data-image-id="0*oq7fyFzzOWvWHzFf.png"
data-width="652" data-height="214" />
</figure>

> ***Answer: Steve***

**Q.2:** What city and country was the author writing from?

<figure id="2d2c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1QKvT-PowqBte_PI.png"
class="graf-image" data-image-id="0*1QKvT-PowqBte_PI.png"
data-width="467" data-height="499" />
</figure>

> ***Answer: Gwangju, South Korea***

**Q.3:** \[Research\] What is the name (in English) of the temple inside
the National Park the author frequently visits?

<figure id="003c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LTtnnGjqWHPFXCKt.png"
class="graf-image" data-image-id="0*LTtnnGjqWHPFXCKt.png"
data-width="538" data-height="378" />
</figure>

> ***Answer: Jeungsimsa Temple***

### Task 4: Digging into DNS {#ec0d .graf .graf--h3 .graf-after--blockquote name="ec0d"}

So far we've gathered some good info about the content that was on our
target website, even though it hasn't been live for several years.

But what about technical details?

That's where ViewDNS.info comes in.

**ViewDNS.info** provides a convenient UI for looking up registration
information on a target website. Using this information, it may be
possible to draw certain conclusions that are not clearly spelled out,
such as whether the website is hosted on a shared or dedicated IP
address. The answer to this question can imply things about the
website's budget as well as traffic.

Take a look at the search options available and see if you can answer
these questions.

**Q.1:** What was RepublicOfKoffee.com's IP address as of October 2016?

<figure id="960f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Tk04ESZ2Uwf1YdGc.png"
class="graf-image" data-image-id="0*Tk04ESZ2Uwf1YdGc.png"
data-width="875" data-height="387" />
</figure>

The next thing that we need to find is the RepublicOfKoffee.com's IP
address as of October 2016. Use the IP history to extract the required
information

<figure id="10ea" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*5O0H26mh_vI7Cehm.png"
class="graf-image" data-image-id="0*5O0H26mh_vI7Cehm.png"
data-width="843" data-height="451" />
</figure>

> ***Answer: 173.248.188.152***

**Q.2:** Based on the other domains hosted on the same IP address, what
kind of hosting service can we safely assume our target uses?

> ***Answer: shared***

Now we need to find out hosting service our target uses. Using the
reverse lookup for this purpose. There is a long list of domain names
associated with the IP we found earlier. This means our target website
owner is using a shared hosting service as it costs a lot less than the
dedicated hosting service

<figure id="c8f4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jfsYTzxxX4t4J1b1.png"
class="graf-image" data-image-id="0*jfsYTzxxX4t4J1b1.png"
data-width="524" data-height="602" />
</figure>

Going back to the IP history, the IP address has changed 4 times in the
history of the domains. This answers the last answer of this task

**Q.3:** How many times has the IP address changed in the history of the
domain?

> ***Answer: 4***

### Task 5: Taking Off The Training Wheels {#5519 .graf .graf--h3 .graf-after--blockquote name="5519"}

We have a new target domain **heat.net.** We are required to find
following

**Q.1:** What is the second nameserver listed for the domain?

Visit lookup.icann.org/lookup

> ***Answer: NS2.HEAT.NET***

**Q.2:** What IP address was the domain listed on as of December 2011?

Visit viewdns.info

> ***Answer: 72.52.192.240***

**Q.3:** Based on domains that share the same IP, what kind of hosting
service is the domain owner using?

> ***Answer: shared***

**Q.4:** On what date did was the site first captured by the internet
archive? (MM/DD/YY format)

> ***Answer: 06/01/97***

**Q.5:** What is the first sentence of the first body paragraph from the
final capture of 2001?

visit **web.archives.org **,jun 1

> ***Answer: After years of great online gaming, it's time to say
> good-bye.***

**Q.6:** Using your search engine skills, what was the name of the
company that was responsible for the original version of the site?

> ***Answer: SegaSoft***

**Q.7:** What does the first header on the site on the last capture of
2010 say?

visit **web.archives.org**

> ***Answer: Heat.net --- Heating and Cooling***

### Task 6: Taking A Peek Under The Hood Of A Website {#a9a6 .graf .graf--h3 .graf-after--blockquote name="a9a6"}

Isn't it kind of interesting how the website disappeared for a period of
time and came back?

Clearly the purpose of the site is different now. Let's roll up our
sleeves and figure out what's going on.

First, do you have any gut feelings about this site? What is your
overall impression? Does it *feel* like a legitimate source of
information?

Why?

You might consider some of the following points:

- [Language --- What grade level is the writing? Does it seem to be
  written by a native English speaker?]{#c947}
- [UX --- Is it user friendly? Is the design modern?]{#0161}
- [What pages does the site have?]{#35b6}

I can tell you that this website conforms well to antiquated search
engine optimization (SEO) best practices. You can read more about [SEO
best practices on
ahrefs](https://ahrefs.com/blog/seo-best-practices/){.markup--anchor
.markup--p-anchor
data-href="https://ahrefs.com/blog/seo-best-practices/"
rel="noopener ugc nofollow noopener" target="_blank"} if you like before
you continue.

**Technical Research**

Often, clues about a website and its creator/owner may be
unintentionally left behind in the source code of the website. Pretty
much every web browser will have a method of doing this. It is well
worth taking the time to become acquainted with how this works in your
browser of choice. For Chrome on MacOS, you'll go to the top menu bar
and choose View \> Developer \> View Source.

***Note: This also works on sites you visit within Archive.org's Wayback
Machine.***

Once the source code of the page loads, it's time to look around. You
don't have to understand HTML, CSS, or Javascript to read notes that the
developers left behind for themselves. In HTML, comments begin with the
characters \<! --- . Here's an example of what a forgotten comment might
look like in practice:

`<!--Don't forget to email Bob Loblaw when the site goes live at bob@fakeemail.com-->`{.markup--code
.markup--p-code}

As easy as that may be to read, if it was buried inside a gigantic page
full of code it could still be easy to miss. That's where ctrl-F comes
in. Here are some good things to search for with ctrl-f:

<figure id="21f5" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1N3HKpvpy4xgquMG.png"
class="graf-image" data-image-id="0*1N3HKpvpy4xgquMG.png"
data-width="875" data-height="241" />
</figure>

Finding any of the above data gives you a potential pivot point. The
Bellingcat article linked above goes into more detail on how exactly to
do it but you don't have to overcomplicate things!

You can always just take any of the above information and plug it back
into your favorite search engine and you may just strike gold!

Ready to put this all into practice?

These following questions refer to
heat\[dot\]net/36/need-to-hire-a-commercial-heating-contractor/

Have at it!

<figure id="9246" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zOQtQO7XxNZ7-Nq3.png"
class="graf-image" data-image-id="0*zOQtQO7XxNZ7-Nq3.png"
data-width="875" data-height="516" />
</figure>

[http://www.heat.net/](http://www.heat.net/){.markup--anchor
.markup--p-anchor data-href="http://www.heat.net/"
rel="noopener ugc nofollow noopener" target="_blank"}

**Q.1:** How many internal links are in the text of the article?

> ***Answer: 5***

**Q.2:** How many external links are in the text of the article?

> ***Answer: 1***

**Q.3:** Website in the article's only external link ( that isn't an ad)

External Link URL

> ***Answer: purchase.org***

**Q.4:** Try to find the Google Analytics code linked to the site

Use the view page source on the article and find the google analytics
code as seen below

<figure id="b927" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*TXZ1lDwKcjD0LmAj.png"
class="graf-image" data-image-id="0*TXZ1lDwKcjD0LmAj.png"
data-width="875" data-height="491" />
</figure>

> ***Answer: UA-251372--24***

**Q.5:** Is the the Google Analytics code in use on another website? Yay
or nay

> ***Answer: nay***

**Q.6:** Does the link to this website have any obvious affiliate codes
embedded with it? Yay or Nay

> ***Answer: nay***

### Task 7: Final Exam: Connect the Dots {#1f34 .graf .graf--h3 .graf-after--blockquote name="1f34"}

Experienced OSINT researchers will tell you that chasing rabbit holes
all day and night without being able to make some solid connections is
not OSINT.

OSINT refers to the patterns that start to emerge as we connect the dots
in the analysis of the data.

Congrats! you found that our target, heat\[.\]net, links to an
interesting external site. A question remains though: ***Why???***

There is no affiliate code in the link, so there is no obvious financial
connection between the two. Maybe there's another kind of connection.

This is your final exam, and there is exactly one question.

Get busy!

**Q.1:** Use the tools in Task 4 to confirm the link between the two
sites. Try hard to figure it out without the hint.

<figure id="ef94" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*UqF5Pbf9jvLW3rX9.png"
class="graf-image" data-image-id="0*UqF5Pbf9jvLW3rX9.png"
data-width="875" data-height="444" />
</figure>

> ***Answer: Liquid Web, L.L.C***

### OSINT Resources {#6d06 .graf .graf--h3 .graf-after--blockquote name="6d06"}

A little web OSINT knowledge can go a long way in online investigations.
A few examples of where it comes into play include any kind of business
OSINT, online scams, or even political journalism. If you would like to
see a prime example of this kind of research being put into practice, I
highly recommend checking out NixIntel's expose [linking antifa.com to
Russia](https://nixintel.info/osint/website-osint-whats-the-link-between-antifa-com-and-russia/){.markup--anchor
.markup--p-anchor
data-href="https://nixintel.info/osint/website-osint-whats-the-link-between-antifa-com-and-russia/"
rel="noopener ugc nofollow noopener" target="_blank"}, which is an
amazing case study.

Make sure to check out the other OSINT boxes out there such as:

- [The [Searchlight IMINT
  Room](https://tryhackme.com/room/searchlightosint){.markup--anchor
  .markup--li-anchor
  data-href="https://tryhackme.com/room/searchlightosint"
  rel="noopener ugc nofollow noopener" target="_blank"} and
  [Geolocation](https://tryhackme.com/room/geolocatingimages){.markup--anchor
  .markup--li-anchor
  data-href="https://tryhackme.com/room/geolocatingimages"
  rel="noopener ugc nofollow noopener" target="_blank"} for Geolocation
  and Image Analysis]{#be92}
- [The [Google
  Dork](https://tryhackme.com/room/googledorking){.markup--anchor
  .markup--li-anchor
  data-href="https://tryhackme.com/room/googledorking"
  rel="noopener ugc nofollow noopener" target="_blank"} room for
  advanced search engine operators]{#a049}
- [The [OhSINT](https://tryhackme.com/room/ohsint){.markup--anchor
  .markup--li-anchor data-href="https://tryhackme.com/room/ohsint"
  rel="noopener ugc nofollow noopener" target="_blank"} room for a
  little extra IMINT practice]{#22e2}

There are also two fantastic podcasts that every OSINT practitioner
should regularly listen to. The [OSINT
Curious](https://osintcurio.us/){.markup--anchor .markup--p-anchor
data-href="https://osintcurio.us/" rel="noopener ugc nofollow noopener"
target="_blank"} podcast and [The Privacy, Security, & OSINT
Show](https://inteltechniques.com/podcast.html){.markup--anchor
.markup--p-anchor data-href="https://inteltechniques.com/podcast.html"
rel="noopener ugc nofollow noopener" target="_blank"}.

Finally, a solid paid option for OSINT training that won't break the
bank is [TheOSINTion](https://www.theosintion.com/){.markup--anchor
.markup--p-anchor data-href="https://www.theosintion.com/"
rel="noopener ugc nofollow noopener" target="_blank"}. If you enjoyed
the content of this room you would LOVE the [Business
OSINT](https://www.theosintion.com/courses/business-osint/){.markup--anchor
.markup--p-anchor
data-href="https://www.theosintion.com/courses/business-osint/"
rel="noopener ugc nofollow noopener" target="_blank"} course they offer.
I have no affiliation with the course other than being a satisfied
customer.

### Promote and Collaborate on Cybersecurity Insights {#c8e5 .graf .graf--h3 .graf-after--p name="c8e5"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#7fe5 .graf .graf--h3 .graf-after--p name="7fe5"}

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
.h-card} on [August 21, 2024](https://medium.com/p/221e82d0e056).

[Canonical
link](https://medium.com/@bevijaygupta/webosint-tryhackme-writeup-221e82d0e056){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
