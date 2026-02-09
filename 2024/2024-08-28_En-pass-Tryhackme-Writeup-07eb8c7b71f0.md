::: {}
# En-pass Tryhackme Writeup {#en-pass-tryhackme-writeup .p-name}
:::

::: {.section .p-summary field="subtitle"}
Room link: https://tryhackme.com/room/enpass Note: This room is free
:::

::::::: {.section .e-content field="body"}
:::::: {#34da .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### En-pass Tryhackme Writeup {#123e .graf .graf--h3 .graf--leading .graf--title name="123e"}

<figure id="e3bc" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*vII7p0cTuLh3BoOQ.png"
class="graf-image" data-image-id="0*vII7p0cTuLh3BoOQ.png"
data-width="446" data-height="247" data-is-featured="true" />
</figure>

**Room link:**
[https://tryhackme.com/room/enpass](https://tryhackme.com/room/enpass){.markup--anchor
.markup--p-anchor data-href="https://tryhackme.com/room/enpass"
rel="noopener ugc nofollow noopener" target="_blank"}\
**Note: This room is free**

**Nmap Scan**

<figure id="cda4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*wAeDTfsJ-nRctVYV.png"
class="graf-image" data-image-id="0*wAeDTfsJ-nRctVYV.png"
data-width="547" data-height="312" />
</figure>

We have only two ports open. SSH is running on port 80 and a HTTP server
is running on port 8081 and the banner is telling us this is a ubuntu
box. Since there is not much to look into the SSH service, let us start
the enumeration with HTTP service on port 8001

### HTTP service on Port 8001 {#46fa .graf .graf--h3 .graf-after--p name="46fa"}

<figure id="cc10" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*Os39yAjfd2lFlIJx.png"
class="graf-image" data-image-id="0*Os39yAjfd2lFlIJx.png"
data-width="759" data-height="600" />
</figure>

### Gobuster {#9624 .graf .graf--h3 .graf-after--figure name="9624"}

``` {#56e9 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://10.10.200.74:8001/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
```

<figure id="7e28" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*84kUW8hvJ611b4eV.png"
class="graf-image" data-image-id="0*84kUW8hvJ611b4eV.png"
data-width="491" data-height="316" />
</figure>

### Gobuster on /web {#ff68 .graf .graf--h3 .graf-after--figure name="ff68"}

``` {#1180 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://10.10.200.74:8001/web -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
```

<figure id="1adf" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*k1XW-ZLtG-7_YlTf.png"
class="graf-image" data-image-id="0*k1XW-ZLtG-7_YlTf.png"
data-width="489" data-height="186" />
</figure>

**Gobuster on /web/resources**

``` {#782e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
gobuster dir -u http://10.10.200.74:8001/web/resources -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
```

<figure id="58d7" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*zkzIk6KEc1NMjst3.png"
class="graf-image" data-image-id="0*zkzIk6KEc1NMjst3.png"
data-width="481" data-height="193" />
</figure>

**Gobuster on /web/resources/infoseek**

``` {#ae0d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://10.10.200.74:8001/web/resources/infoseek -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
```

<figure id="26ae" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*taic-ySyTHsSsiuK.png"
class="graf-image" data-image-id="0*taic-ySyTHsSsiuK.png"
data-width="480" data-height="190" />
</figure>

**Gobuster on /web/resources/infoseek/configure**

``` {#5efa .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
gobuster dir -u http://10.10.200.74:8001/web/resources/infoseek -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
```

<figure id="d58c" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*lXu07XgI_JbSAFdo.png"
class="graf-image" data-image-id="0*lXu07XgI_JbSAFdo.png"
data-width="502" data-height="197" />
</figure>

### visiting /web/resources/infoseek/configure/ key {#ca5a .graf .graf--h3 .graf-after--figure name="ca5a"}

<figure id="3a59" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*lquVziDhPz29y8wD.png"
class="graf-image" data-image-id="0*lquVziDhPz29y8wD.png"
data-width="724" data-height="353" />
</figure>

We get a encrpyted private key.

When i will try to decrypt the key using **ssh2john.** And the password
was not cracked by john as it was not available on **rockyou.txt**

``` {#fb91 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
curl http://10.10.200.74:8001/web/resources/infoseek/configure/key > hash
```

### Visiting /zip {#a7fc .graf .graf--h3 .graf-after--pre name="a7fc"}

<figure id="2ecc" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*Lu-5sRLL64qg4GuA.png"
class="graf-image" data-image-id="0*Lu-5sRLL64qg4GuA.png"
data-width="478" data-height="678" />
</figure>

We get a list of zip files. There are about 100 zip files. As we can see
on the picture, all the zip files have exact date of modification and
size, except the file **a.zip**

### Downloading a.zip first {#5a03 .graf .graf--h3 .graf-after--p name="5a03"}

<figure id="c02a" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*c7jumU81w_bcs5Ub.png"
class="graf-image" data-image-id="0*c7jumU81w_bcs5Ub.png"
data-width="750" data-height="447" />
</figure>

Extracting the content

<figure id="b06c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WHelW1Nptz-ZbO-9.png"
class="graf-image" data-image-id="0*WHelW1Nptz-ZbO-9.png"
data-width="536" data-height="463" />
</figure>

As I was manually extracting the zip files, all of the zip files have a
file called **a** inside them and the content on the file was
**sadman.**

### Downloading and extracting remaining zip files {#ee8d .graf .graf--h3 .graf-after--p name="ee8d"}

``` {#9281 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
for i in `seq 1 100`; do wget -q http://10.10.200.74:8001/zip/a$i.zip && unzip a$i.zip && cat a && rm a && rm a$i.zip; done
```

<figure id="e058" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*1Nsljk1RYlQ9IEKM.png"
class="graf-image" data-image-id="0*1Nsljk1RYlQ9IEKM.png"
data-width="875" data-height="221" />
</figure>

This went on and all I got was sadman.

This was a dead end. So, lets continue with our enumeration.

### Visiting /reg.php {#3ab0 .graf .graf--h3 .graf-after--p name="3ab0"}

<figure id="84cc" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*BBa7riuYYuc3Gvl1.png"
class="graf-image" data-image-id="0*BBa7riuYYuc3Gvl1.png"
data-width="682" data-height="432" />
</figure>

If we input something e.g. 1234 we see in the response back from the
server contains the following php code:

So we need to bypass the filter in the above code to move forward.
Reading the code the following conditions should met for the input to
pass the filters:

- [Lowercase/uppercase alphabets and numbers are not allowed.]{#c78a}
- [Input is splited in to chunks with ',' as the delimiter and
  individual chunks should have certain lengths as mentioned in the
  code.A sum variable is calculated based on all the conditions match
  and compared with value 9 to give is the result, which is the way
  forward.]{#c954}

I used an [**online php
compiler**](https://www.w3schools.com/php/phptryit.asp?filename=tryphp_compiler){.markup--anchor
.markup--p-anchor
data-href="https://www.w3schools.com/php/phptryit.asp?filename=tryphp_compiler"
rel="noopener ugc nofollow noopener" target="_blank"} to debug the code
and finally figured out the input which will give is the result. Input
can contain symbols so used '\$' and also made the individual chunks of
the required lengths.

Checking the source

<figure id="b943" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*-AQX4bHXl0JmkXwI.png"
class="graf-image" data-image-id="0*-AQX4bHXl0JmkXwI.png"
data-width="613" data-height="566" />
</figure>

There is a PHP code with some checks implemented. And the code says we
will get what we need if we pass the checks being implemented.

**Final PHP Code**

``` {#e44a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="php"}
<?php
   $title = "$$,$$,$$,$$$,$$,$$,$$,$$,$$$";
   if (!preg_match('/[a-zA-Z0-9]/i' , $title )){
          $val = explode(",",$title);
          $sum = 0;
          for($i = 0 ; $i < 9; $i++){
                if ( (strlen($val[0]) == 2) and (strlen($val[8]) ==  3 ))  {
                    if ( $val[5] !=$val[8]  and $val[3]!=$val[7] ) 
                        $sum = $sum+ (bool)$val[$i]."<br>"; 
                }
          }          if ( ($sum) == 9 ){
              echo $result;//do not worry you'll get what you need.
              echo " Congo You Got It !! Nice ";
            }
                    else{
                      echo "  Try Try!!";
                    }
          }
          else{
            echo "  Try Again!! ";
  }
```

The condition is that our POST variable **`title`{.markup--code
.markup--p-code}** should not contain any alphanumeric characters. After
that explode with **`,`{.markup--code .markup--p-code}** which will
break our title variable into arrays. Looking at the for loop, we have
to pass the title variable such that there will be 9 element in the
array. So to do that, we have to use 8 commas (,) on our title variable
and few simple check are being implemented afterwards.

<figure id="6808" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*6Inq9oDlApz_NpwN.png"
class="graf-image" data-image-id="0*6Inq9oDlApz_NpwN.png"
data-width="875" data-height="436" />
</figure>

[https://www.w3schools.com/php/php_compiler.asp](https://www.w3schools.com/php/php_compiler.asp){.markup--anchor
.markup--p-anchor
data-href="https://www.w3schools.com/php/php_compiler.asp"
rel="noopener ugc nofollow noopener" target="_blank"}

### Submiting the payload {#85f8 .graf .graf--h3 .graf-after--p name="85f8"}

``` {#81ad .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
$$,$$,$$,$$$,$$,$$,$$,$$,$$$
```

<figure id="7d87" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*EDx5GsoCsttCluX-.png"
class="graf-image" data-image-id="0*EDx5GsoCsttCluX-.png"
data-width="713" data-height="449" />
</figure>

And we get the password. Now we can try if this is the password for that
key.

### Trying to decrypt the key with the obtained password {#309b .graf .graf--h3 .graf-after--p name="309b"}

edit rockyou.txt and paste password in it and check

<figure id="59ae" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*tOzvNawxHWchgkBw.png"
class="graf-image" data-image-id="0*tOzvNawxHWchgkBw.png"
data-width="576" data-height="344" />
</figure>

Yes the password is correct

**OR you can check by this method**

<figure id="9dcb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*I3gu9UKNoq6AHUkI.png"
class="graf-image" data-image-id="0*I3gu9UKNoq6AHUkI.png"
data-width="677" data-height="227" />
</figure>

And we successfully decrypt the key. Since the SSH is open, we can try
and login with this private key, but the problem is that we do not have
a username yet.

I have spent a fair amount of time here.

### Checking /403.php {#5742 .graf .graf--h3 .graf-after--p name="5742"}

<figure id="8864" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*VqjXpkWxg09DQRdP.png"
class="graf-image" data-image-id="0*VqjXpkWxg09DQRdP.png"
data-width="696" data-height="585" />
</figure>

Looking at the page, It looked like we have to bypass this forbidden 403
to get what we are looking for, i.e. username. And also looking at the
hint provided by the creator, it seems to be the right path

<figure id="3a6c" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ll_5er9LwVVpPa9s.png"
class="graf-image" data-image-id="0*ll_5er9LwVVpPa9s.png"
data-width="498" data-height="104" />
</figure>

So I manually tried bunch of custom header and things but was not able
to bypass the check. Then I searched and downloaded few github tools
which try multiple payloads to try and bypass the 403 error. From those
tools, one seem to get what I wanted and the check was bypassed.

### Fuzzing with [403fuzzer](https://github.com/intrudir/403fuzzer){.markup--anchor .markup--h3-anchor data-href="https://github.com/intrudir/403fuzzer" rel="noopener ugc nofollow noopener" target="_blank"} {#189f .graf .graf--h3 .graf-after--p name="189f"}

Cloning the repo

<figure id="9c76" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*dKq5Y6KZcj8L0B1S.png"
class="graf-image" data-image-id="0*dKq5Y6KZcj8L0B1S.png"
data-width="679" data-height="193" />
</figure>

<figure id="0377" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*qa9lRP-KMSpzIS7x.png"
class="graf-image" data-image-id="0*qa9lRP-KMSpzIS7x.png"
data-width="864" data-height="335" />
</figure>

It is nice that it has option for proxy. Now we can analyse the whole
traffic using burpsuite.

### Running the exploit {#d0be .graf .graf--h3 .graf-after--p name="d0be"}

<figure id="470f" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*Ybe61tMmiBI4UgE0.png"
class="graf-image" data-image-id="0*Ybe61tMmiBI4UgE0.png"
data-width="875" data-height="307" />
</figure>

The exploit was running and I was observing the response on the
burpsuite. And I get a different reponse length with status code 200

**Do not On Intercepted**

<figure id="3d0f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*vbYmY4o6ZmtsN0Cs.png"
class="graf-image" data-image-id="0*vbYmY4o6ZmtsN0Cs.png"
data-width="875" data-height="588" />
</figure>

Yes we Got user **imsau**

### Another Method {#9db6 .graf .graf--h3 .graf-after--p name="9db6"}

``` {#b3ea .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
curl "http://10.10.40.95:8001/403.php/..;/"
```

<figure id="6ef8" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*962YU2ijG6xjGWlJ.png"
class="graf-image" data-image-id="0*962YU2ijG6xjGWlJ.png"
data-width="870" data-height="141" />
</figure>

Again We got user **imsau**

**Get into shell**

<figure id="4e64" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*t7qGBc6p_mufuBbo.png"
class="graf-image" data-image-id="0*t7qGBc6p_mufuBbo.png"
data-width="679" data-height="374" />
</figure>

<figure id="fded" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*ns3kHRgqNM0txkn9.png"
class="graf-image" data-image-id="0*ns3kHRgqNM0txkn9.png"
data-width="548" data-height="233" />
</figure>

### Privilege Escalation {#28c7 .graf .graf--h3 .graf-after--figure name="28c7"}

I ran linpeas first and did not get that much information from it. So as
I was manually looking through different directories, I found a script
directory on /opt.

<figure id="ac30" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WVDiuiZXMJC960lM.png"
class="graf-image" data-image-id="0*WVDiuiZXMJC960lM.png"
data-width="561" data-height="430" />
</figure>

It loads the content of file **/tmp/file.yml** and passes to
**yaml.load()** function.

Checking if /tmp/file exists

<figure id="1b5f" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*owygCrUyRaYUQa2a.png"
class="graf-image" data-image-id="0*owygCrUyRaYUQa2a.png"
data-width="552" data-height="220" />
</figure>

And there is no /tmp/file.yml.

This means that we can create a file called /tmp/file.yml with arbitary
content and this content will be passed to yaml.load() function. I
checked online and found that this can be used to execute code on the
box. This can be visualized as desearialization of untrusted user input.

Even though this code was vulnerable, we must be somehow able to execute
this script as root.

Upload
[**pspy**](https://github.com/DominicBreuker/pspy){.markup--anchor
.markup--p-anchor data-href="https://github.com/DominicBreuker/pspy"
rel="noopener ugc nofollow noopener" target="_blank"} into box

<figure id="fa45" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MeWWM5DBwKESAtzg.png"
class="graf-image" data-image-id="0*MeWWM5DBwKESAtzg.png"
data-width="820" data-height="209" />
</figure>

<figure id="7200" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*5QuKLVaIuwIXFcAR.png"
class="graf-image" data-image-id="0*5QuKLVaIuwIXFcAR.png"
data-width="768" data-height="349" />
</figure>

**Run pspy on box**

<figure id="11db" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*nNOoxBztPWVpFdOW.png"
class="graf-image" data-image-id="0*nNOoxBztPWVpFdOW.png"
data-width="660" data-height="335" />
</figure>

<figure id="04cb" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*5MeupGl_RurXNbYl.png"
class="graf-image" data-image-id="0*5MeupGl_RurXNbYl.png"
data-width="875" data-height="128" />
</figure>

We can notice few things on this image. There is a cronjob which is
being executed by root every minute. It executes the script
**/opt/scripts/file.py**, removes the file **/tmp/file.yml,** changes
the owner of the file **/tmp/file.yml** and again executes and deletes
it. It's kind of strange to be honest. But what we can do is make a file
with our malicious payload and run a infinite loop which copies this
malicious payload to **/tmp/file.yml.**

### Content of shell.yml {#7626 .graf .graf--h3 .graf-after--p name="7626"}

<figure id="4af1" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*o139jq_SBNGgu6SX.png"
class="graf-image" data-image-id="0*o139jq_SBNGgu6SX.png"
data-width="593" data-height="127" />
</figure>

We just set the SUID bit on the /bin/bash binary.

### Executing infinite loop and watching the binary using watch {#0bfe .graf .graf--h3 .graf-after--p name="0bfe"}

<figure id="74ea" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*G60BNyKesTJGWK9M.png"
class="graf-image" data-image-id="0*G60BNyKesTJGWK9M.png"
data-width="736" data-height="104" />
</figure>

press Ctrl+c

And after a minute or so, the bash binary has SUID bit set on it.

### Getting a root shell {#94a9 .graf .graf--h3 .graf-after--p name="94a9"}

<figure id="fed6" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*tf7RY1gs6eP9JGOL.png"
class="graf-image" data-image-id="0*tf7RY1gs6eP9JGOL.png"
data-width="675" data-height="347" />
</figure>

<figure id="7dca" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/0*IZPfjQPGyNp12Smn.png"
class="graf-image" data-image-id="0*IZPfjQPGyNp12Smn.png"
data-width="358" data-height="157" />
</figure>

### Promote and Collaborate on Cybersecurity Insights {#5784 .graf .graf--h3 .graf-after--figure name="5784"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#01a5 .graf .graf--h3 .graf-after--p name="01a5"}

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
.h-card} on [August 28, 2024](https://medium.com/p/07eb8c7b71f0).

[Canonical
link](https://medium.com/@bevijaygupta/en-pass-tryhackme-writeup-07eb8c7b71f0){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
