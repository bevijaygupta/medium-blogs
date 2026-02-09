---
title: "Wekor Tryhackme Writeup e7af9ae56445"
platform: Medium
original_file: 2024-08-18_Wekor-Tryhackme-Writeup-e7af9ae56445.md
---

# Wekor Tryhackme Writeup e7af9ae56445

::: {}
# Wekor Tryhackme Writeup {#wekor-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
This is a Writeup of Tryhackme room "Wekor"
:::

::::::: {.section .e-content field="body"}
:::::: {#68eb .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Wekor Tryhackme Writeup {#3dce .graf .graf--h3 .graf--leading .graf--title name="3dce"}

<figure id="7a62" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*Tn3KseJtU5DETueFscWbVQ.png"
class="graf-image" data-image-id="1*Tn3KseJtU5DETueFscWbVQ.png"
data-width="1882" data-height="911" />
</figure>

**This is a Writeup of Tryhackme room "Wekor"**

<figure id="cb64" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*hKTXovdGFBuOXMuU.png"
class="graf-image" data-image-id="0*hKTXovdGFBuOXMuU.png"
data-width="447" data-height="263" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/wekorra](https://tryhackme.com/room/wekorra){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/wekorra"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is Free**

Add Taget to hosts file

``` {#c2e6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
echo "10.10.62.4      wekor.thm" >> /etc/hosts
```

### Enumeration {#95b3 .graf .graf--h3 .graf-after--pre name="95b3"}

<figure id="50a5" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*lNQJyEraMXZV04jp.png"
class="graf-image" data-image-id="0*lNQJyEraMXZV04jp.png"
data-width="627" data-height="417" />
</figure>

On Port 80

<figure id="9d43" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*CgpkswunN4JIuq3b.png"
class="graf-image" data-image-id="0*CgpkswunN4JIuq3b.png"
data-width="536" data-height="120" />
</figure>

<figure id="052b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*HcVpq_mZ7Vc4JA77.png"
class="graf-image" data-image-id="0*HcVpq_mZ7Vc4JA77.png"
data-width="416" data-height="267" />
</figure>

There was also a robots.txt on the website, on visiting the robots.txt,
we get many different directory paths. Sadly, all of them redirect us to
404(Not Found), except for one "/comingreallysoon"

<figure id="b946" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*rELlQu_cKsdKo3Ts.png"
class="graf-image" data-image-id="0*rELlQu_cKsdKo3Ts.png"
data-width="848" data-height="209" />
</figure>

here we found another directory

<figure id="c54d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*kkzJBB06m1VmdmHI.png"
class="graf-image" data-image-id="0*kkzJBB06m1VmdmHI.png"
data-width="1250" data-height="632" />
</figure>

After some poking around, we see that there is a form field on the
checkout portion of the website, there they ask for a coupon code.\
Testing for a possible SQL injection, trying to put just a single quote,
the website reflects an error message.

<figure id="eb31" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bUu_vBzS2ejvYXAz.png"
class="graf-image" data-image-id="0*bUu_vBzS2ejvYXAz.png"
data-width="667" data-height="279" />
</figure>

Using " **' or 1=1 --- -**," without the double quotes, will get the
actual coupon code.

use Burpsuite to capture request

<figure id="aa72" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*xm-ff8jrqzzGBnlF.png"
class="graf-image" data-image-id="0*xm-ff8jrqzzGBnlF.png"
data-width="536" data-height="137" />
</figure>

<figure id="170d" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*a05OKSmYm2lNvdOi.png"
class="graf-image" data-image-id="0*a05OKSmYm2lNvdOi.png"
data-width="698" data-height="619" />
</figure>

Run SQLMAP

> *sqlmap -r request.txt*

This confirms that we have SQL injection possible:

<figure id="790a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*PQEZndhraqs9dXNM.png"
class="graf-image" data-image-id="0*PQEZndhraqs9dXNM.png"
data-width="843" data-height="275" />
</figure>

Check for available Databases:

> *sqlmap -r request.txt --- dbs*

<figure id="16fd" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*XT4iRRcIL_38k_u8.png"
class="graf-image" data-image-id="0*XT4iRRcIL_38k_u8.png"
data-width="668" data-height="280" />
</figure>

Check tables in WordPress database:

> *sqlmap -r request.txt -D wordpress -tables*

<figure id="d50f" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*nsT96w7bY_xl-t-G.png"
class="graf-image" data-image-id="0*nsT96w7bY_xl-t-G.png"
data-width="618" data-height="383" />
</figure>

Dump the table "wp_users"

> *sqlmap -r request.txt --- dump -D wordpress -T wp_users*

<figure id="8b4a" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*T22vqc_UHh7_wLkX.png"
class="graf-image" data-image-id="0*T22vqc_UHh7_wLkX.png"
data-width="1250" data-height="386" />
</figure>

So we have hash for user "admin" for the site:
[http://site.wekor.thm/wordpress](http://site.wekor.thm/wordpress){.markup--anchor
.markup--p-anchor data-href="http://site.wekor.thm/wordpress"
rel="noopener ugc nofollow noopener" target="_blank"}

From
[here](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"} we can see the
type of has is "phpass":

<figure id="4630" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*NPpBBxJUN7sFJxza.png"
class="graf-image" data-image-id="0*NPpBBxJUN7sFJxza.png"
data-width="668" data-height="254" />
</figure>

[https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes){.markup--anchor
.markup--p-anchor
data-href="https://hashcat.net/wiki/doku.php?id=example_hashes"
rel="noopener ugc nofollow noopener" target="_blank"}

Put all the hashes in a text file and crack then using JTR:

> *john --- wordlist=rockyou.txt --- format=phpass hash.txt*

<figure id="5c29" class="graf graf--figure graf-after--blockquote">
<img
src="https://cdn-images-1.medium.com/max/800/0*BxT9JUQtbfsTDJjy.png"
class="graf-image" data-image-id="0*BxT9JUQtbfsTDJjy.png"
data-width="630" data-height="286" />
</figure>

Got some hashes cracked and trying the cracked password for user
"wp_yura" we were able to login to
[http://site.wekor.thm/wordpress/wp-](http://site.wekor.thm/wordpress/wp-){.markup--anchor
.markup--p-anchor data-href="http://site.wekor.thm/wordpress/wp-"
rel="noopener ugc nofollow noopener" target="_blank"}login.php.

<figure id="6bd3" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*fpnKHHUNs992T9WC.png"
class="graf-image" data-image-id="0*fpnKHHUNs992T9WC.png"
data-width="875" data-height="503" />
</figure>

### Reverse Shell {#07bb .graf .graf--h3 .graf-after--figure name="07bb"}

Now it is possible to get a reverse shell from here by injecting a [php
reverse
shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php){.markup--anchor
.markup--p-anchor
data-href="https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php"
rel="noopener ugc nofollow noopener" target="_blank"} via
Appearance-\>Theme Editor-\>404 Template(404.php):

<figure id="9fbb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*1ax5LL0_tkr3ZP0J.png"
class="graf-image" data-image-id="0*1ax5LL0_tkr3ZP0J.png"
data-width="1250" data-height="539" />
</figure>

Remember to put in the IP Address and Port Number of the machine where
we want to get a reverse shell back. Also start a netcat session on that
machine. Now acess the 404.php using the following link:

> [*http://site.wekor.thm/wordpress/wp-content/themes/twentytwentyone/404.php*](http://site.wekor.thm/wordpress/wp-content/themes/twentytwentyone/404.php){.markup--anchor
> .markup--blockquote-anchor
> data-href="http://site.wekor.thm/wordpress/wp-content/themes/twentytwentyone/404.php"
> rel="noopener ugc nofollow noopener" target="_blank"}

And we got a reverse shell:

<figure id="86da" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*O6uOa_U_v0y0M2HV.png"
class="graf-image" data-image-id="0*O6uOa_U_v0y0M2HV.png"
data-width="728" data-height="248" />
</figure>

What users we have

``` {#621d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
cat /etc/passwd
```

<figure id="a973" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*S3Pku_qWsKNwzm5R.png"
class="graf-image" data-image-id="0*S3Pku_qWsKNwzm5R.png"
data-width="587" data-height="157" />
</figure>

Only Orka and root are have shell config.

Looking for open ports you can find something running in port 11211.

<figure id="522a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*4r0LvRmihu4xJmB9.png"
class="graf-image" data-image-id="0*4r0LvRmihu4xJmB9.png"
data-width="834" data-height="361" />
</figure>

After searching in Google we discover that is a memcached server. Some
more searches and we got the command to dump the cached data.

<figure id="d056" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*0zem3DWN951uG_sc.png"
class="graf-image" data-image-id="0*0zem3DWN951uG_sc.png"
data-width="875" data-height="363" />
</figure>

Ok, now we have Orka password.

As Orka, what you can do?

<figure id="f4ae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*O5ORfcqWVUuIsB9M.png"
class="graf-image" data-image-id="0*O5ORfcqWVUuIsB9M.png"
data-width="498" data-height="252" />
</figure>

### Privilege Escalation {#ee04 .graf .graf--h3 .graf-after--figure name="ee04"}

Now it's time to do privilege escalation. First of all before running
any script let's check if Orka can run anything using
`sudo -l`{.markup--code .markup--p-code} :

<figure id="55e0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*k4df_U-LE9y9TUUN.png"
class="graf-image" data-image-id="0*k4df_U-LE9y9TUUN.png"
data-width="594" data-height="271" />
</figure>

You can execute bitcoin as sudo. Also you can't change bitcoin but, you
are can change the Desktop folder. Let's replace the bitcoin with bash
and get the root.

<figure id="b483" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*cT_ptDLq-SzpeFFB.png"
class="graf-image" data-image-id="0*cT_ptDLq-SzpeFFB.png"
data-width="539" data-height="502" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#2478 .graf .graf--h3 .graf-after--figure name="2478"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#8778 .graf .graf--h3 .graf-after--p name="8778"}

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
.h-card} on [August 18, 2024](https://medium.com/p/e7af9ae56445).

[Canonical
link](https://medium.com/@bevijaygupta/wekor-tryhackme-writeup-e7af9ae56445){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
