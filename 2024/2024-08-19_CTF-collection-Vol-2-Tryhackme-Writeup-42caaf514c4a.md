---
title: "CTF collection Vol 2 Tryhackme Writeup 42caaf514c4a"
platform: Medium
original_file: 2024-08-19_CTF-collection-Vol-2-Tryhackme-Writeup-42caaf514c4a.md
---

# CTF collection Vol 2 Tryhackme Writeup 42caaf514c4a

::: {}
# CTF collection Vol.2 Tryhackme Writeup {#ctf-collection-vol.2-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "CTF collection Vol.2"
:::

::::::: {.section .e-content field="body"}
:::::: {#82bf .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### CTF collection Vol.2 Tryhackme Writeup {#7478 .graf .graf--h3 .graf--leading .graf--title name="7478"}

**This is a Writeup of Tryhackme room "CTF collection Vol.2"**

<figure id="94d2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*sdWQEUyCewVm0I1e.png"
class="graf-image" data-image-id="0*sdWQEUyCewVm0I1e.png"
data-width="477" data-height="265" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/ctfcollectionvol2](https://tryhackme.com/room/ctfcollectionvol2){.markup--anchor
.markup--p-anchor
data-href="https://tryhackme.com/room/ctfcollectionvol2"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

**Difficulty: Medium**

Welcome, welcome and welcome to another CTF collection. This is the
second installment of the CTF collection series. For your information,
the second serious focuses on the web-based challenge. There are a total
of 20 easter eggs a.k.a flags can be found within the box. Let see how
good is your CTF skill.

Now, deploy the machine and collect the eggs!

Warning: **The challenge contains seizure images and background. If you
feeling uncomfortable, try removing the background on \<style\> tag.**

Note: All the challenges flag are formatted as `THM{flag}`{.markup--code
.markup--p-code}, unless stated otherwise

Fact: **Eggs** contain the highest quality protein you can buy.

### Task 2 : Easter egg {#559d .graf .graf--h3 .graf-after--p name="559d"}

**Enumeration**

<figure id="844c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QB3MRRicoxeckfue.png"
class="graf-image" data-image-id="0*QB3MRRicoxeckfue.png"
data-width="598" data-height="411" />
</figure>

we have two ports open, the first one is 22 serving us SSH, the second
one is 80 for HTTP running Apache, and I noticed something weird in the
results, something that looks like a base64, but let us move on and
discover what it is.

**Port 80**

<figure id="fed6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4zLxoJc06EUriiNA.png"
class="graf-image" data-image-id="0*4zLxoJc06EUriiNA.png"
data-width="875" data-height="374" />
</figure>

**Gobuster**

``` {#4cb4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://10.10.159.96 -w directory-list-2.3-medium.txt -x php,html,txt
```

<figure id="e5ec" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*30Xs0sj7BhPnNEkR.png"
class="graf-image" data-image-id="0*30Xs0sj7BhPnNEkR.png"
data-width="430" data-height="334" />
</figure>

[http://10.10.159.96/robots.txt](http://10.10.159.96/robots.txt){.markup--anchor
.markup--p-anchor data-href="http://10.10.159.96/robots.txt"
rel="noopener ugc nofollow noopener" target="_blank"}

<figure id="659b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Jg0BwS2-gi04z0mK.png"
class="graf-image" data-image-id="0*Jg0BwS2-gi04z0mK.png"
data-width="728" data-height="202" />
</figure>

### Easter 1 {#fe11 .graf .graf--h3 .graf-after--figure name="fe11"}

<figure id="692c" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*t8Tg_laS-trDwBxQ.png"
class="graf-image" data-image-id="0*t8Tg_laS-trDwBxQ.png"
data-width="743" data-height="350" />
</figure>

[https://www.duplichecker.com/hex-to-text.php](https://www.duplichecker.com/hex-to-text.php){.markup--anchor
.markup--p-anchor
data-href="https://www.duplichecker.com/hex-to-text.php"
rel="noopener ugc nofollow noopener" target="_blank"}

**Another Method**

<figure id="f7b6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*T4J6_1zRsJgkax5Z.png"
class="graf-image" data-image-id="0*T4J6_1zRsJgkax5Z.png"
data-width="863" data-height="101" />
</figure>

### Easter 2 {#45be .graf .graf--h3 .graf-after--figure name="45be"}

*Hint: Decode the base64 multiple times. Don't forget there are
something being encoded.*

From the `robots.txt`{.markup--code .markup--p-code} file, there is a
hidden resource:

Install urlencode tool

``` {#2ffb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
sudo apt-get install gridsite-clients
```

<figure id="3032" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*6OsJGc7IIj5REN0e.png"
class="graf-image" data-image-id="0*6OsJGc7IIj5REN0e.png"
data-width="875" data-height="145" />
</figure>

<figure id="671b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*7bPsXo3NSueAOvTS.png"
class="graf-image" data-image-id="0*7bPsXo3NSueAOvTS.png"
data-width="737" data-height="409" />
</figure>

<figure id="9afc" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*L_tycmsIMQjQetkH.png"
class="graf-image" data-image-id="0*L_tycmsIMQjQetkH.png"
data-width="674" data-height="289" />
</figure>

### Easter 3 {#28a5 .graf .graf--h3 .graf-after--figure name="28a5"}

*Hint: Directory buster with common.txt might help.*

Dirsearch found `/login/`{.markup--code .markup--p-code}. The page
itself contains an easter egg:

<figure id="77bf" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EqcPBfR3Qdxq-Eaq.png"
class="graf-image" data-image-id="0*EqcPBfR3Qdxq-Eaq.png"
data-width="875" data-height="114" />
</figure>

### Easter 4 {#ba75 .graf .graf--h3 .graf-after--figure name="ba75"}

*Hint: time-based sqli*

The `/login/`{.markup--code .markup--p-code} page was found by
dirsearch. Let's check if fields are vulnerable to SQL injection. We'll
first use Burp Suite to intercept a POST request to the login form, save
it from the HTTP history as **request.txt**

<figure id="d0dd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*66SKlEmAJIlhLpx-.png"
class="graf-image" data-image-id="0*66SKlEmAJIlhLpx-.png"
data-width="583" data-height="553" />
</figure>

<figure id="590d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*QTo1X15jc1ccT9MA.png"
class="graf-image" data-image-id="0*QTo1X15jc1ccT9MA.png"
data-width="457" data-height="222" />
</figure>

This process will take 10 minutes

<figure id="1414" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*zVPsEDvb64VwUW98.png"
class="graf-image" data-image-id="0*zVPsEDvb64VwUW98.png"
data-width="519" data-height="276" />
</figure>

Now that we have the database, let's dump the tables:

<figure id="4bc3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WLSqEBNQk4QrOGuh.png"
class="graf-image" data-image-id="0*WLSqEBNQk4QrOGuh.png"
data-width="630" data-height="211" />
</figure>

<figure id="57c6" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*q53nRmv6-FrsYASp.png"
class="graf-image" data-image-id="0*q53nRmv6-FrsYASp.png"
data-width="330" data-height="204" />
</figure>

Let's see the structure of the `nothing_inside`{.markup--code
.markup--p-code} table:

<figure id="c7a9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jbEiMPjGB_YhfExQ.png"
class="graf-image" data-image-id="0*jbEiMPjGB_YhfExQ.png"
data-width="827" data-height="142" />
</figure>

<figure id="182e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*We8rrrEJo3Qft-v5.png"
class="graf-image" data-image-id="0*We8rrrEJo3Qft-v5.png"
data-width="370" data-height="243" />
</figure>

Only 1 field, let's dump the table:

<figure id="3edd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*chyheTT6An6DieLE.png"
class="graf-image" data-image-id="0*chyheTT6An6DieLE.png"
data-width="875" data-height="94" />
</figure>

<figure id="a129" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*P6H4RfIHxlSZvZK0.png"
class="graf-image" data-image-id="0*P6H4RfIHxlSZvZK0.png"
data-width="449" data-height="199" />
</figure>

### Easter 5 {#7f21 .graf .graf--h3 .graf-after--figure name="7f21"}

*Hint: Another sqli*

Still using the same SQL injection as for easter 4, let's dump the user
table:

<figure id="bdcb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bP119lmv2GIiJif5.png"
class="graf-image" data-image-id="0*bP119lmv2GIiJif5.png"
data-width="659" data-height="122" />
</figure>

<figure id="6836" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*NL5UcstvicJTuvdv.png"
class="graf-image" data-image-id="0*NL5UcstvicJTuvdv.png"
data-width="325" data-height="250" />
</figure>

<figure id="c29f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*SYsB8XrYvG_U1Wkv.png"
class="graf-image" data-image-id="0*SYsB8XrYvG_U1Wkv.png"
data-width="875" data-height="159" />
</figure>

<figure id="ccd0" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*Gc-JqBhUmBIGHd2l.png"
class="graf-image" data-image-id="0*Gc-JqBhUmBIGHd2l.png"
data-width="533" data-height="193" />
</figure>

Search for the `05f3672ba34409136aa71b8d00070d1b`{.markup--code
.markup--p-code} hash on Google, it corresponds to the following
password: \*\*\*\*\*

<figure id="6a3b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2SNzvmEayREhnGgy.png"
class="graf-image" data-image-id="0*2SNzvmEayREhnGgy.png"
data-width="817" data-height="297" />
</figure>

<figure id="cf45" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*m817N7A_xtU4gsk3.png"
class="graf-image" data-image-id="0*m817N7A_xtU4gsk3.png"
data-width="393" data-height="109" />
</figure>

<figure id="6699" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*shtwb1beFc2nOkDQ.png"
class="graf-image" data-image-id="0*shtwb1beFc2nOkDQ.png"
data-width="423" data-height="267" />
</figure>

Now, let's authenticate with **Deskel:\*\*\*\*\***:

<figure id="63d0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*qEHAT4NEAZMHGyuj.png"
class="graf-image" data-image-id="0*qEHAT4NEAZMHGyuj.png"
data-width="524" data-height="485" />
</figure>

### Easter 6 {#210b .graf .graf--h3 .graf-after--figure name="210b"}

*Hint: Look out for the response header.*

<figure id="6c52" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*IU9OqllfG05HsxmH.png"
class="graf-image" data-image-id="0*IU9OqllfG05HsxmH.png"
data-width="730" data-height="328" />
</figure>

### Easter 7 {#25e8 .graf .graf--h3 .graf-after--figure name="25e8"}

*Hint: Cookie is delicious*

When you visit the home page, you see the following title:

<figure id="ec4f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*aaSMZkxgU9g8qbfZ.png"
class="graf-image" data-image-id="0*aaSMZkxgU9g8qbfZ.png"
data-width="673" data-height="84" />
</figure>

From the header, we see that there is a cookie named
`Invited`{.markup--code .markup--p-code} set to 0:

<figure id="e90e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ovMG4hQYgJeCaY_k.png"
class="graf-image" data-image-id="0*ovMG4hQYgJeCaY_k.png"
data-width="705" data-height="219" />
</figure>

Let's set `1`{.markup--code .markup--p-code} instead:

<figure id="5432" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*lrH6Jc9DFWZQNzxM.png"
class="graf-image" data-image-id="0*lrH6Jc9DFWZQNzxM.png"
data-width="742" data-height="130" />
</figure>

### Easter 8 {#4370 .graf .graf--h3 .graf-after--figure name="4370"}

Hint: Mozilla/5.0 (iPhone; CPU iPhone OS 13_1_2 like Mac OS X)
AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.1 Mobile/15E148
Safari/604.1

<figure id="0b24" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*AfO1rHv19kpx74CW.png"
class="graf-image" data-image-id="0*AfO1rHv19kpx74CW.png"
data-width="875" data-height="119" />
</figure>

``` {#d51e .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="perl"}
curl -s --user-agent "Mozilla/5.0 (iPhone; CPU iPhone OS 13_1_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.1 Mobile/15E148 Safari/604.1" http://10.10.159.96 | grep "THM"
```

<figure id="fefa" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*7o_GKuRhxBGrOYdO.png"
class="graf-image" data-image-id="0*7o_GKuRhxBGrOYdO.png"
data-width="875" data-height="147" />
</figure>

### Easter 9 {#13ec .graf .graf--h3 .graf-after--figure name="13ec"}

*Hint: Something is redirected too fast. You need to capture it.*

<figure id="8f6b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Il2Mf0Z6JoS15fRX.png"
class="graf-image" data-image-id="0*Il2Mf0Z6JoS15fRX.png"
data-width="763" data-height="284" />
</figure>

### Easter 10 {#bcd9 .graf .graf--h3 .graf-after--figure name="bcd9"}

*Hint: Look at THM URL without https:// and use it as a referrer.*

When we try to visit the `/free_sub/`{.markup--code .markup--p-code}
page (link provided in the home page), we are told that only people
coming from tryhackme are allowed:

<figure id="b604" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pfbZ54HR8ZaY52AE.png"
class="graf-image" data-image-id="0*pfbZ54HR8ZaY52AE.png"
data-width="683" data-height="81" />
</figure>

Let's modify our referer:

<figure id="5c01" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*09YOJg3CQ6s1bMvX.png"
class="graf-image" data-image-id="0*09YOJg3CQ6s1bMvX.png"
data-width="869" data-height="118" />
</figure>

### Easter 11 {#dff3 .graf .graf--h3 .graf-after--figure name="dff3"}

*Hint: Temper the html*

There is a dropdown on the main page, in the menu section. It allows to
choose between salad, sandwich, tyre or DesKel.

<figure id="9cc1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*8VMgILVHetggWiZt.png"
class="graf-image" data-image-id="0*8VMgILVHetggWiZt.png"
data-width="791" data-height="310" />
</figure>

If you choose salad for example, you will be told to choose an egg
instead, but egg is not on the list.

<figure id="7a6e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FfOAL9eDP0_mqDED.png"
class="graf-image" data-image-id="0*FfOAL9eDP0_mqDED.png"
data-width="874" data-height="388" />
</figure>

Oh, you prefer eggs? No problem...

<figure id="cd57" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*f3HbxnopPnEil8yx.png"
class="graf-image" data-image-id="0*f3HbxnopPnEil8yx.png"
data-width="854" data-height="219" />
</figure>

### Easter 12 {#0654 .graf .graf--h3 .graf-after--figure name="0654"}

*Hint: Fake js file*

A Javscript file is included in the home page:

<figure id="cac1" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nRUwC-C-kKIC6DWO.png"
class="graf-image" data-image-id="0*nRUwC-C-kKIC6DWO.png"
data-width="577" data-height="76" />
</figure>

But this is a *fake* jquery:

<figure id="0af4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*19RxiE5OshbIvU_4.png"
class="graf-image" data-image-id="0*19RxiE5OshbIvU_4.png"
data-width="854" data-height="269" />
</figure>

in this the function **ahem()** not calling so just add one line to call
**ahem()** function in a Javascript interpreter (e.g.
[**http://math.chapman.edu/\~jipsen/js/**](http://math.chapman.edu/~jipsen/js/){.markup--anchor
.markup--p-anchor data-href="http://math.chapman.edu/~jipsen/js/"
rel="noopener ugc nofollow noopener" target="_blank"}**):**

``` {#0d8f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
function ahem()
 {
    str1 = '4561737465722031322069732054484d7b68316464336e5f6a355f66316c337d'
    var hex  = str1.toString();
    var str = '';
    for (var n = 0; n < hex.length; n += 2) {
        str += String.fromCharCode(parseInt(hex.substr(n, 2), 16));
    }
    return str;
 }
write(ahem());
```

<figure id="320e" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ft9zaD7xJylWBfo1.png"
class="graf-image" data-image-id="0*Ft9zaD7xJylWBfo1.png"
data-width="875" data-height="337" />
</figure>

### Easter 13 {#d204 .graf .graf--h3 .graf-after--figure name="d204"}

The page discovered at easter #9 redirects to
`/ready/gone.php`{.markup--code .markup--p-code}, which contains the
flag:

<figure id="462e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tdo25gHhcnblFn82.png"
class="graf-image" data-image-id="0*tdo25gHhcnblFn82.png"
data-width="868" data-height="240" />
</figure>

### Easter 14 {#f3fc .graf .graf--h3 .graf-after--figure name="f3fc"}

*Hint: Embed image code*

For flag 14, it's straight forward, the main page source code contain
the flag as a png encoded to base64, decode it, and get the flag from
the picture.

<figure id="1ffe" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SZawk-OBy6wg7mzg.png"
class="graf-image" data-image-id="0*SZawk-OBy6wg7mzg.png"
data-width="848" data-height="364" />
</figure>

decode base64

<figure id="faa0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QGqDVRBQXuU-ejVP.png"
class="graf-image" data-image-id="0*QGqDVRBQXuU-ejVP.png"
data-width="875" data-height="527" />
</figure>

[https://codebeautify.org/base64-to-image-converter](https://codebeautify.org/base64-to-image-converter){.markup--anchor
.markup--p-anchor
data-href="https://codebeautify.org/base64-to-image-converter"
rel="noopener ugc nofollow noopener" target="_blank"}

### Easter 15 {#d073 .graf .graf--h3 .graf-after--p name="d073"}

*Hint: Try guest the alphabet and the hash code*

When we connect to `/game1/`{.markup--code .markup--p-code} (found by
dirsearch), we are prompted for a combination, and we see a hash
proposed as hint:

<figure id="ca0c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*pTs0Frpppautm8Tx.png"
class="graf-image" data-image-id="0*pTs0Frpppautm8Tx.png"
data-width="430" data-height="294" />
</figure>

If we post the alphabet, we have the correspondance of numerical values.
Let's do it for the upper case letters:

``` {#25bc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

<figure id="e404" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*Izy-TeRFdzwOdkET.png"
class="graf-image" data-image-id="0*Izy-TeRFdzwOdkET.png"
data-width="875" data-height="262" />
</figure>

And also for the lower case letters:

<figure id="0215" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3AJE5J920ElP_Lmh.png"
class="graf-image" data-image-id="0*3AJE5J920ElP_Lmh.png"
data-width="764" data-height="275" />
</figure>

We now have the numbers associated to each upper (99=A, 100=B,
101=C, ... 141=Z) and lower (89=a, 90=b, ..., 18=z) and we can now
decode the message:

``` {#4dcc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
51 89 77 93 126 14 93 10
G  a  m  e  O   v  e  r
```

Let's post our answer to get the flag:

<figure id="c759" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*e9LcBfO4rGsfd-b2.png"
class="graf-image" data-image-id="0*e9LcBfO4rGsfd-b2.png"
data-width="562" data-height="223" />
</figure>

### Easter 16 {#e2a3 .graf .graf--h3 .graf-after--figure name="e2a3"}

*Hint: Make all inputs into one form.*

The page has 3 forms whose action points to the same page, using the
same method (POST), each containing a button.

<figure id="bc48" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*b7EEWLutV9VcOPaP.png"
class="graf-image" data-image-id="0*b7EEWLutV9VcOPaP.png"
data-width="613" data-height="266" />
</figure>

<figure id="4f9e" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*WFrnkwH019uJK0u3.png"
class="graf-image" data-image-id="0*WFrnkwH019uJK0u3.png"
data-width="733" data-height="549" />
</figure>

It is not possible to push all the buttons in the same time. However, we
can send all the values in POST to the page. The server will *think*
that the buttons have all been clicked:

<figure id="e286" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*2_gkDn7KQwNtZcKw.png"
class="graf-image" data-image-id="0*2_gkDn7KQwNtZcKw.png"
data-width="875" data-height="463" />
</figure>

### Easter 17 {#0a23 .graf .graf--h3 .graf-after--figure name="0a23"}

*Hint: bin -\> dec -\> hex -\> ascii*

From the source code of the main page:

<figure id="ec9b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*HiOxjwa-swJvK8Qb.png"
class="graf-image" data-image-id="0*HiOxjwa-swJvK8Qb.png"
data-width="875" data-height="258" />
</figure>

``` {#e91c .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
<!--! Easter 17-->
<button onclick="nyan()">Mulfunction button</button><br>
<p id="nyan"></p>
<script>
function catz(){
        document.getElementById("nyan").innerHTML = "100010101100001011100110111010001100101011100100010000000110001001101110011101000100000010101000100100001001101011110110110101000110101010111110110101000110101010111110110101100110011011100000101111101100100001100110110001100110000011001000011001101111101"
}
</script>
```

Let's solve that in python:

<figure id="2c4d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*OQhMk_B6GcuV0aPn.png"
class="graf-image" data-image-id="0*OQhMk_B6GcuV0aPn.png"
data-width="859" data-height="403" />
</figure>

### Easter 18 {#e0b7 .graf .graf--h3 .graf-after--figure name="e0b7"}

*Hint: Request header. Format is egg:Yes*

<figure id="fb22" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*g-h5pUP6FU46Lmdd.png"
class="graf-image" data-image-id="0*g-h5pUP6FU46Lmdd.png"
data-width="859" data-height="137" />
</figure>

### Easter 19 {#e6f8 .graf .graf--h3 .graf-after--figure name="e6f8"}

*Hint: A thick dark line*

``` {#3afa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
$ wget http://10.10.141.149/small
$ file small.png 
small.png: PNG image data, 900 x 100, 4-bit colormap, non-interlaced
```

<figure id="fca1" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*n-tEQNElnHfbr_Jo.png"
class="graf-image" data-image-id="0*n-tEQNElnHfbr_Jo.png"
data-width="620" data-height="121" />
</figure>

### Easter 20 {#43aa .graf .graf--h3 .graf-after--figure name="43aa"}

*Hint: You need to POST the data instead of GET. Burp suite or curl
might help.*

From the source code of the main page:

<figure id="e294" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EWALaf5wq0By7P7k.png"
class="graf-image" data-image-id="0*EWALaf5wq0By7P7k.png"
data-width="862" data-height="117" />
</figure>

Now, if we send the username and password using the POST method to the
main page, we are provided with the easter egg:

<figure id="d0ed" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iBosQr4ZWn2SasVZ.png"
class="graf-image" data-image-id="0*iBosQr4ZWn2SasVZ.png"
data-width="862" data-height="187" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#69a5 .graf .graf--h3 .graf-after--figure name="69a5"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#43a3 .graf .graf--h3 .graf-after--p name="43a3"}

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
.h-card} on [August 19, 2024](https://medium.com/p/42caaf514c4a).

[Canonical
link](https://medium.com/@bevijaygupta/ctf-collection-vol-2-tryhackme-writeup-42caaf514c4a){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
