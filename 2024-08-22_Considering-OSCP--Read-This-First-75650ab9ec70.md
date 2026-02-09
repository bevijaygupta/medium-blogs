::: {}
# Considering OSCP? Read This First {#considering-oscp-read-this-first .p-name}
:::

::: {.section .p-summary field="subtitle"}
Last year, I passed the OSCP and this is a write-up to reflect a bit on
the process. You'll find plenty of write-ups and talks on the OSCP...
:::

::::::: {.section .e-content field="body"}
:::::: {#4d0d .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Considering OSCP? Read This First {#66b3 .graf .graf--h3 .graf--leading .graf--title name="66b3"}

<figure id="12dc" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*Ok5iG9XOLdJo1s5-ZJIikw.png"
class="graf-image" data-image-id="1*Ok5iG9XOLdJo1s5-ZJIikw.png"
data-width="2240" data-height="1260" />
</figure>

Last year, I passed the
[OSCP](https://www.offsec.com/courses/pen-200/){.markup--anchor
.markup--p-anchor data-href="https://www.offsec.com/courses/pen-200/"
rel="noopener ugc nofollow noopener" target="_blank"} and this is a
write-up to reflect a bit on the process. You'll find plenty of
write-ups and talks on the OSCP certification with titles like "How I
passed the OSCP-exam with max points in X hours on my first try". This
is not one of those. This is the write-up I was looking for before I
started my own OSCP certification. The one trying to summarize the OSCP
certification course as a whole so other cybersecurity professionals can
decide whether or not it's worth it for themselves.

As a disclaimer to the following, I'll just say that the following is
very colored by my own personal opinions and personal experiences. You
are free to disagree with anything I say in this write-up. But I thought
I would make this, as I have some thoughts on the course that I have not
seen anyone else bring up out there. I will be focusing on a few of the
negative sides of the experience as they don't get mentioned much in the
usual posts on the topic. It seems to me that people get a slightly
rose-colored view of the experience if they manage to get through the
certification.

### The Good --- A Great Foundation {#dbc0 .graf .graf--h3 .graf-after--p name="dbc0"}

Well-rounded course with lots of different, relevant topics, resulting
in a very thorough foundation for cybersecurity professionals, not only
pentesters. Below I have just thrown a few points on the great things
about the course.

- [The course material had lots of exercises relevant to all the topics
  you just read about, giving you a chance to try out a decent chunk of
  the theory right away.]{#f954}
- [The course hits a good balance between teaching you "a lot about a
  lot" without actually going **extremely** deep everywhere. You will
  notice plenty of places throughout the course, where the material
  makes a few assumptions to make things easier for the student. This is
  to give a good introduction to subjects like security on a Windows
  machine, without the student having to understand **every** aspect of
  Windows security. Instead, there will still be plenty of things to get
  better at on the other side of the course.]{#0fca}
- [The pivoting, networking, and AD material is brilliant. You need a
  proper lab environment to get this stuff under your nails and you get
  that with the OSCP.]{#883b}
- [The course forces you to quickly pick up new tools and technologies.
  You won't always be intimately familiar with the technologies you face
  in the wild while pen-testing and the OSCP reflects that very well. To
  get through the exam, you have to quickly understand the problem space
  you are in and find a way through it.]{#6bf3}

<figure id="09da" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*DHu_YGdGHHrBYTPp.jpg"
class="graf-image" data-image-id="0*DHu_YGdGHHrBYTPp.jpg"
data-width="714" data-height="1000" data-is-featured="true" />
</figure>

What non-pen-testers think, when they hear "Pivot"

### The Bad --- The Course Material Isn't Perfect {#f834 .graf .graf--h3 .graf-after--p name="f834"}

The first thing I noticed about the course is that the course material
is made to teach you pen-testing, not passing the exam. This means the
course will sometimes go into tools that are not allowed in the exam.
Yes, Sqlmap is awesome for SQL-injections, but there's spent a little
too much time on it in my opinion. The same goes for the Metasploit
Framework, which is soft-banned, if you ask me. These tools are
essential to know as a pen-tester, but I just felt like a little too
much emphasis was put on showing them off, rather than showing "how to
do things the manual way" like in the exam.

The second problem I have with the material, is the ramp-up between the
exercises in the course material and the latter challenge machines. The
skill-difference between these two phases is too steep. Looking back, I
should have been quicker to look outside the course and focus on e.g.
the [NetSecFocus
list](https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview#){.markup--anchor
.markup--p-anchor
data-href="https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview#"
rel="noopener ugc nofollow noopener" target="_blank"} to get a more
well-rounded feeling for how to attack machines. I assumed the course
had a "paved path" through the material that would teach things at a
natural pace. This is not the case. It felt more like playing a Dark
Souls game in which you should expect to get hard-stuck at certain
points until you simply sit down and grind away until you "git gud"
enough to move on. It may have been naive to expect a paved path through
a course as feared as the OSCP, but honestly... I don't see why you
should need to look outside the course material to get through the
course, to be honest.

<figure id="c201" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zTgI_7kaG_SPyNY2.jpg"
class="graf-image" data-image-id="0*zTgI_7kaG_SPyNY2.jpg"
data-width="500" data-height="676" />
</figure>

Don't expect an easy time

### The Ugly --- Technical Difficulties and Community Management {#1408 .graf .graf--h3 .graf-after--p name="1408"}

The platform is not without technical difficulties. I had a lot of
instances where the practice machines were unreachable, the environment
was down as a whole or the VPN connection just broke for no reason. I
can unfortunately also say that the exam experience was not free of
technical difficulties either. I tried to hash it out with the proctors,
who ended up being very unhelpful all in all. All in all, I was honestly
shocked at some of the technical problems I experienced with the offsec
platform at times. I went in expecting a top of the class platform for
learning cybersecurity and that is not what I got (at least from a
technical point of view).

I also had plenty of unpleasant interactions with community guides on
Discord. My very first interaction on the discord was someone asking for
a hint in the #pen-200 discord channel, to which I gave a useful hint
that in didn't spoil anything about the course. I was then profoundly
scolded by a moderator, "as I was not following the Discord guidelines",
in a very hit-and-run manner. The subject of the #pen-200 discord
channel is "General discussion around the pen-200 course", so I couldn't
tell what I had done wrong. I had to reach out asking "What did I do?",
to which another mod explained that questions, like the one I answered,
are supposed to be asked in a private channel where only verified course
members can ask questions and get answers. They do this to protect their
IP, which is of course very reasonable. But to scold a new community
member in that way seems like bad community management in my book. I had
even attempted to brush up on the rules beforehand and still ended up
not following the rules.

Similar situations happened during the course. some of the time, when
students ask questions on Discord, mods simply answer "Try Harder". This
can be a fair response in some cases. But when you start your question
stating that you have been stuck for days, maybe an actual hint is
needed.

The bad sides of the course increase the barrier to entry for students
to pass. I don't think courses should be structured to be intentionally
harder than necessary. Unfortunately, I get the feeling that OffSec
likes the fact that the course is so hard that the barrier to entry is
high and that so many students fail. This gives the whole experience an
air of prestige, which increases interest and keeps the customers
coming. However, I don't believe having a high failure rate is the mark
of a great course. I believe even complicated topics can be taught to
"most" people who are interested if it is done well.

<figure id="0821" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jwzEg0soM0y9StpB.jpeg"
class="graf-image" data-image-id="0*jwzEg0soM0y9StpB.jpeg"
data-width="788" data-height="445" />
</figure>

Sometimes, going through the OSCP felt like it was more nefarious than
it needed to be. I think many people who have taken any sort of
education can relate to teachers or courses with that kind of philosophy

### What would I have done differently? {#86b9 .graf .graf--h3 .graf-after--p name="86b9"}

The OSCP course has taught me a lot about cybersecurity but also a lot
about what the "certification scene" is like. Knowing what I know now, I
would probably do more to "over-prepare", before the course even
started, if I were to do it again. Looking back at a lot of the "How I
passed the OSCP with maximum points"-write-ups out there, that also
seems to be a common theme with them. Often, the authors of those
write-ups mention how they had been grinding hard for the OSCP even
before buying the course. That way, you would also lessen the "sharp
edges" of the course and turn some of those bad experiences into minor
inconveniences. One way to over-prepare could be to do a large number of
the practice machines mentioned in the [NetSecFocus
list](https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview#){.markup--anchor
.markup--p-anchor
data-href="https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview#"
rel="noopener ugc nofollow noopener" target="_blank"} before starting
the course. This is a compiled list of practice machines relevant to the
OSCP. It contains machines from the OffSec play/practice environments as
well as from HTB and other sources.

Another great resource is [IppSec's videos on the \@TJ_NULL OSCP prep
list](https://www.youtube.com/playlist?list=PLidcsTyj9JXK-fnabFLVEvHinQ14Jy5tf){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com/playlist?list=PLidcsTyj9JXK-fnabFLVEvHinQ14Jy5tf"
rel="noopener ugc nofollow noopener" target="_blank"}. Complementary
material like this can greatly help improve your methodology for
attacking the machines later in the OSCP course. The downside is that if
you want to attack the machines

<figure id="c69c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PjT_gBCJFH69wD1C.jpg"
class="graf-image" data-image-id="0*PjT_gBCJFH69wD1C.jpg"
data-width="400" data-height="400" />
</figure>

Over-preparation through material outside of the course can help a lot.
I ended up using the NetSecFocus list to supplement the course exercises

### What did I Learn and Was It Worth It? {#c72f .graf .graf--h3 .graf-after--p name="c72f"}

With the last few sections, you may think this write-up is meant to
scare people away from the OSCP. That is not the case. The point is more
to reflect on the process. The certification taught me a lot about "the
basics" of both Linux and Windows as well as networking. But I also
learned a lot about a myriad of tools and techniques in red teaming
engagements. As previously mentioned, the OSCP forces you to quickly
pick up new tools and technologies, which is always useful when working
in IT.

So all in all, was it worth it? Yes, definitely. It has improved my
foundation in so many areas that I would otherwise have a hard time
covering to the same extent. However, the experience was, in my opinion,
much harder than it needed to be due to some of the negative things
mentioned in this write-up.

Would I recommend the course? yes, to some people. However, it is not a
course I would recommend to many people, to be honest. Depending on your
needs, you could come a long way by doing similar training with other
solutions. But if the piece of paper of the certification is important
to you, my best advice would be to over-prepare and not expect to learn
all you need directly from the course material. In the same vein, make
sure to over-prepare before the course if you are spending your own
hard-earned money in an attempt to pivot from a previous career into
cybersecurity.

All in all, I'm happy to have taken the OSCP, and I cannot say whether I
will be taking more of their certifications in the future. But if I do,
I will be going into it with a different mindset than I did the first
time around.

### Promote and Collaborate on Cybersecurity Insights {#f680 .graf .graf--h3 .graf-after--p name="f680"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#5153 .graf .graf--h3 .graf-after--p name="5153"}

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
.h-card} on [August 22, 2024](https://medium.com/p/75650ab9ec70).

[Canonical
link](https://medium.com/@bevijaygupta/considering-oscp-read-this-first-75650ab9ec70){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
