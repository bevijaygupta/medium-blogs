---
title: "Physical Security Intro Tryhackme Writeup 6fbb6c4ec98c"
platform: Medium
original_file: 2024-09-04_Physical-Security-Intro-Tryhackme-Writeup-6fbb6c4ec98c.md
---

# Physical Security Intro Tryhackme Writeup 6fbb6c4ec98c

::: {}
# Physical Security Intro Tryhackme Writeup {#physical-security-intro-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/physicalsecurityintro
:::

::::::: {.section .e-content field="body"}
:::::: {#8fd5 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Physical Security Intro Tryhackme Writeup {#2c4f .graf .graf--h3 .graf--leading .graf--title name="2c4f"}

<figure id="10d9" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*Jl_uua_oIPwSi3ol.png"
class="graf-image" data-image-id="0*Jl_uua_oIPwSi3ol.png"
data-width="495" data-height="229" data-is-featured="true" />
</figure>

**Room link**:
[https://tryhackme.com/room/physicalsecurityintro](https://tryhackme.com/room/physicalsecurityintro){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/physicalsecurityintro"
rel="noopener ugc nofollow noopener" target="_blank"}

### Task 1. Introduction {#328d .graf .graf--h3 .graf-after--p name="328d"}

**Learn the basics of physical security**

A lot of times physical security is overlooked during red team
engagements. Sure, it's not as popular as cyber security, however having
some basic knowledge of lock picking and bypasses are an important tool
to have in your repertoire.

Below are some great videos that are a perfect introduction to physical
security. If you have a basic knowledge of physical security already,
you might be able to breeze through the room, however if you don't,
these videos will be one of the best introductions you could get.

**I'll Let Myself In: Tactics of Physical Pen Testers --- Deviant
Ollam**

<figure id="9b96" class="graf graf--figure graf--iframe graf-after--p">
<div class="iframe">
<div id="player">

</div>
<div class="player-unavailable">
<h1 id="an-error-occurred." class="message">An error occurred.</h1>
<div class="submessage">
Unable to execute JavaScript.
</div>
</div>
</div>
</figure>

Video used with permission of Deviant Ollam

**The Right Way To Do Wrong --- Patrick McNeil**

<figure id="85e1" class="graf graf--figure graf--iframe graf-after--p">
<div class="iframe">
<div id="player">

</div>
<div class="player-unavailable">
<h1 id="an-error-occurred." class="message">An error occurred.</h1>
<div class="submessage">
Unable to execute JavaScript.
</div>
</div>
</div>
</figure>

Video used with permission of Patrick McNeil

### Task 2. Overt, Covert, and Surreptitious Entry {#55f4 .graf .graf--h3 .graf-after--p name="55f4"}

**Learn the different methods of entry**

Overt entry is when the method of entry causes damage or destruction.
This could be damage or destruction to locks, doors, windows, walls or
other objects.

Covert entry is usually undetectable to un-trained people. However,
during a forensic investigation by trained professionals, the method of
entry would be discovered.

Surreptitious entry is when the method of entry is undetectable to both
un-trained and trained people. This method would most likely go
unnoticed even during a forensic investigation.

**For the questions below, we will use a multiple choice format. When
answering, use the number next to the answer as your submitted answer.**

1.  [**Overt**]{#2ec1}
2.  [**Covert**]{#3367}
3.  [**Surreptitious**]{#c984}

**Question 1**. Using an angle grinder to cut a lock open is what type
of entry?

> ***Answer: 1***

**Question 2.** Lock picking could be considered what type of entry?

> ***Answer: 2***

**Question 3.** Lock bypassing can be considered what type of entry?

> ***Answer: 2***

**Question 4.** Taking a photo of a key, decoding it and duplicating it
can be considered what type of entry?

> ***Answer: 3***

**Question 5.** Determining the combination of a safe through
surveillance can be considered what type of entry?

> ***Answer: 3***

**Question 6.** Breaking a window to gain entry can be considered what
type of entry?

> ***Answer: 1***

### Task 3. Lock Picking {#2bfe .graf .graf--h3 .graf-after--blockquote name="2bfe"}

**Show that you have the basic knowledge of lock picking**

Answer the questions below. If you are struggling with the questions, go
back to the videos in the introduction. If you are still struggling, a
quick Google search will help you answer the questions.

**Question 1.** What is the name of the tool which is used to apply
torque to the core of a lock when picking?

> ***Answer: Tension Wrench***

**Question 2.** What is the term used for picking a single pin at a
time?

> ***Answer: Single Pin Picking***

**Question 3.** What is the abbreviation commonly used to reference the
above answer?

> ***Answer: SPP***

**Question 4.** What is the term used when you try to randomly set pins?

> ***Answer: Raking***

**Question 5.** This type of lock is typically cheap, low quality, and
found on low security applications such as office desk cabinets.

> ***Answer: Wafer Lock***

**Question 6.** This type of pick profile is usually used when single
pin picking.

> ***Answer: Hook***

**Question 7.** When single pin picking, this term refers to when you
feel like you have set a pin and the core rotates slightly

> ***Answer: False Set***

**Question 8.** This type of security driver pin gives several clicks as
it is being picked.

> ***Answer: Serrated***

### Task 4. Lock Anatomy {#d5e7 .graf .graf--h3 .graf-after--blockquote name="d5e7"}

**Show that you have a basic understanding of a locks anatomy**

There are many different types of locks, but below we will cover some of
the more common locks such as pin tumbler locks. Some questions below
work for more than just pin tumblers, but they usually cover a part of
the lock that doesn't have to do with the keyway.

**Question 1**. What is the interface between the two pins in a pin
stack referred to as?

> ***Answer: Shear Line***

**Question 2.** What are the pins on the bottom half of a pin stack
referred to as? (you don't have to enter the word pin in the answer)

> ***Answer: Key***

**Question 3.** What are the pins on the top half of a pin stack
referred to as? (you don't have to enter the word pin in the answer)

> ***Answer: Driver***

**Question 4.** What non-shimmable elements do padlocks use to keep the
shackle in place?

> ***Answer: Ball Bearings***

**Question 5.** What is the piece that allows locking lugs to retract
when the core is turned?

> ***Answer: Actuator***

**Question 6.** What piece of a standard door latch should remain
completely depressed when the door is closed to prevent loiding/slipping
of the latch?

> ***Answer: Dead latch***

**Question 7.** What is the locking mechanism that has a bolt which
protrudes into the frame of the door preventing it from opening?

> ***Answer: Deadbolt***

### Task 5. Padlock Bypassing {#5b19 .graf .graf--h3 .graf-after--blockquote name="5b19"}

**Show that you have a basic knowledge of bypassing padlocks**

Padlocks are a common security feature in many places. Have a basic
knowledge of padlock bypassing can get you into server cages, lockers
and more.

**Question 1**. A lock which is unshielded is susceptible to what bypass
tool?

> ***Answer: Knife***

**Question 2.** A lock which has spring loaded locking lugs rather than
ball bearings can be bypassed with what tool?

> ***Answer: Shim***

**Question 3.** Combination locks such as the Masterlock 5400D are
susceptible to a bypass which reveals the combination What is this
method known as?

> ***Answer: Decoding***

**Question 4.** The Masterlock 175 is infamous for its ability to be
bypassed using what type of bypass?

> ***Answer: Mini Knife***

**Question 5.** What bypass method uses a key cut to the lowest depths
and kinetic energy to bounce the driver pins above the shear line and
allow a lock to be opened?

> ***Answer: Bumping***

**Question 6.** Locks which have spring loaded locking lugs can be
opened by tapping a hammer on the side of the lock. What is this attack
method called?

> ***Answer: Rapping***

**Question 7.** What type of pick takes advantage of lazy manufacturing
practices by lifting all the key pins and driver pins above the shear
line to bypass a lock?

> ***Answer: Comb***

**Question 8**. What tools can be wiggled inside the keyway of wafer
locks to roughly simulate the biting of the key and open the lock?

> ***Answer: Jiggler***

### Task 6. Hardware Bypassing {#10b3 .graf .graf--h3 .graf-after--blockquote name="10b3"}

**Show your know some basic hardware bypasses**

Physical security isn't all about lock picking. Sometimes there are
easier and more creative ways to get a door open.

**Question 1**. What tool is used to reach under a door and actuate a
handle from the interior?

> ***Answer: Under The Door Tool***

**Question 2.** What tool can be used to bypass a set of double doors
which have a crash bar on the secure side?

> ***Answer: Double Door Tool***

**Question 3.** What item can be used to widen the gaps between doors
and door frames or between double doors to allow for other bypass tools
to be used? This tool is also common for automobile entry.

> ***Answer: Air Wedge***

**Question 4.** An improperly hung door which opens away from you can be
bypassed using this type of tool?

> ***Answer: Shim***

**Question 5.** An improperly hung door which opens away from you can be
bypassed using this type of tool?

> ***Answer: traveler hook***

**Question 6.** What type of material can be used to go over the door to
grab the secure side handles when an under the door tool is not able to
be used?

> ***Answer: Film***

**Question 7.** Canned air can be used to bypass what type of door
controller hardware?

> ***Answer: REX sensor***

**Question 8.** Adams Rite hardware fixtures are susceptible to a bypass
where a wire is snaked through the keyway and actuates the locking
mechanism behind it, what could prevent this bypass?

> ***Answer: shielding***

### Promote and Collaborate on Cybersecurity Insights {#293f .graf .graf--h3 .graf-after--blockquote name="293f"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#8e01 .graf .graf--h3 .graf-after--p name="8e01"}

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
.h-card} on [September 4, 2024](https://medium.com/p/6fbb6c4ec98c).

[Canonical
link](https://medium.com/@bevijaygupta/physical-security-intro-tryhackme-writeup-6fbb6c4ec98c){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
