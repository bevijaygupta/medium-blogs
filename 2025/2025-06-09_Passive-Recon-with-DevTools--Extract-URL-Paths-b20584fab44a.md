::: {}
# Passive Recon with DevTools: Extract URL Paths {#passive-recon-with-devtools-extract-url-paths .p-name}
:::

::: {.section .p-summary field="subtitle"}
In the world of penetration testing and web security, reconnaissance
(RECON) is the foundational phase that scans for entry points...
:::

::::::: {.section .e-content field="body"}
:::::: {#ef2a .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Passive Recon with DevTools: Extract URL Paths {#d773 .graf .graf--h3 .graf--leading .graf--title name="d773"}

<figure id="d147" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*1vnep__loRdEnv_x"
class="graf-image" data-image-id="0*1vnep__loRdEnv_x" data-width="1280"
data-height="720" data-is-featured="true" />
</figure>

In the world of penetration testing and web security, reconnaissance
(RECON) is the foundational phase that scans for entry points, discovers
hidden resources, and prepares the roadmap for deeper investigation. One
particularly effective --- but often overlooked --- tactic is **passive
endpoint reconnaissance**: quietly harvesting URL paths or routes
without generating network requests to endpoints you don't already know.

This technique takes advantage of the fact that most websites expose
internal structure simply by referencing pages via links (anchors,
script tags, image sources, etc.) in the DOM (Document Object Model).
With a few clever lines of JavaScript run in your browser's DevTools
console, you can:

1.  [Extract *all unique URL paths* (routes) referenced on the current
    page;]{#67ad}
2.  [Save this list as a `.txt`{.markup--code .markup--li-code}
    file;]{#f8bd}
3.  [Use it as input for tools like Burp, OWASP ZAP, or Hydra for
    further analysis.]{#73fd}

Below, we'll explore two key snippets, unpack how they work, integrate
them into a hands-on walkthrough, and add nuance around use cases,
enhancements, and ethical considerations.

### The Core Snippets {#0715 .graf .graf--h3 .graf-after--p name="0715"}

You provided two concise JavaScript blocks. Let's rewrite and annotate
them for clarity:

### 1. Extract Unique URL Paths {#18e3 .graf .graf--h3 .graf-after--p name="18e3"}

``` {#9f29 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
// Step 1: Grab all anchors with href attributes, map to unique normalized paths, log them
[...new Set(
  [...document.querySelectorAll("a[href]")]
    .map(a => new URL(a.href, location.href).pathname)
)]
.forEach(path => console.log(path));
```

**What this does:**

- [`document.querySelectorAll("a[href]")`{.markup--code
  .markup--li-code}: Find every `<a>`{.markup--code .markup--li-code}
  element that includes an `href`{.markup--code
  .markup--li-code}.]{#d0d6}
- [`[...]`{.markup--code .markup--li-code} spreads the resulting
  NodeList into an Array.]{#dca6}
- [`.map(a => ...)`{.markup--code .markup--li-code}: Transform each
  anchor into a normalized `pathname`{.markup--code .markup--li-code},
  using `new URL(..., location.href)`{.markup--code .markup--li-code} to
  handle relative URLs gracefully.]{#0815}
- [`new Set(...)`{.markup--code .markup--li-code}: Remove duplicates so
  each path shows up once.]{#94c1}
- [`forEach(path => console.log(path))`{.markup--code .markup--li-code}:
  Print each unique path to the DevTools console.]{#e954}

### 2. Save Paths to `.txt`{.markup--code .markup--h3-code} File {#2a05 .graf .graf--h3 .graf-after--li name="2a05"}

``` {#0d01 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="dart"}
(() => {
  const paths = [...new Set(
    [...document.querySelectorAll("a[href]")]
      .map(a => new URL(a.href, location.href).pathname)
  )];
```

``` {#fb27 .graf .graf--pre .graf-after--pre}
  const blob = new Blob([paths.join("\n")], { type: "text/plain" });
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
```

``` {#de1e .graf .graf--pre .graf-after--pre}
  const domain = location.hostname.replace(/^www\./, "");
  a.download = `${domain}.txt`;
```

``` {#a849 .graf .graf--pre .graf-after--pre}
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
})();
```

**How it works:**

- [Wraps everything inside an Immediately Invoked Function Expression
  (IIFE) to contain the scope.]{#0c47}
- [Extracts and de-duplicates paths like before, storing them in
  `paths`{.markup--code .markup--li-code}.]{#5880}
- [Creates a `Blob`{.markup--code .markup--li-code} object from the
  joined array of paths (each separated by newline).]{#427b}
- [Creates a temporary anchor (`<a>`{.markup--code .markup--li-code})
  pointing to the Blob as an object URL.]{#15e1}
- [Auto-clicks it to initiate the download of a file named
  `<domain>.txt`{.markup--code .markup--li-code}.]{#30d8}
- [Cleans up by removing the `<a>`{.markup--code .markup--li-code} from
  the DOM.]{#f1f5}

### A Real-World Walkthrough {#69d3 .graf .graf--h3 .graf-after--li name="69d3"}

Let's simulate visiting
[**https://example.com**](https://example.com){.markup--anchor
.markup--p-anchor data-href="https://example.com" rel="noopener"
target="_blank"} (this could be any web app) and step through it.

**Open DevTools**:

- [In Chrome: `F12`{.markup--code .markup--li-code} → **Console**
  tab.]{#31c6}
- [In Firefox: `Ctrl + Shift + K`{.markup--code .markup--li-code}
  (Windows/Linux) or `Cmd + Opt + K`{.markup--code .markup--li-code}
  (macOS).]{#31e3}

**Paste Snippet #1**:

- [`[...new Set( [...document.querySelectorAll("a[href]")] .map(a => new URL(a.href, location.href).pathname) )].forEach(path => console.log(path));`{.markup--code
  .markup--li-code}]{#bdbb}

**Inspect output**:\
You might see:

- [`/ /about /contact /blog /blog/post-1 /assets/logo.png`{.markup--code
  .markup--li-code}]{#0e9a}

1.  [These are endpoints hidden in the HTML, available for further
    exploration.]{#1ea4}
2.  [**Use Snippet #2 to save them**:]{#89ee}
3.  [Paste and run:]{#0a78}

- [`` (() => { const paths = [...new Set( [...document.querySelectorAll("a[href]")] .map(a => new URL(a.href, location.href).pathname) )]; const blob = new Blob([paths.join("\n")], { type: "text/plain" }); const a = document.createElement("a"); a.href = URL.createObjectURL(blob); const domain = location.hostname.replace(/^www\./, ""); a.download = `${domain}.txt`; document.body.appendChild(a); a.click(); document.body.removeChild(a); })(); ``{.markup--code
  .markup--li-code}]{#1a22}

**Check your download**:\
You'll get a file named `example.com.txt`{.markup--code .markup--p-code}
containing:

- [`/ /about /blog /contact /blog/post-1 /assets/logo.png`{.markup--code
  .markup--li-code}]{#e61b}

**Feed it to your tools**:

- [**Burp Intruder / Scanner**: use the paths as endpoints for further
  exploration.]{#8540}
- [**Dirbuster**: combine it with a wordlist to speed up directory
  brute-forcing.]{#5912}

**Scripted workflow**:

- [`while read p; do curl -I https://example.com"$p"; done < example.com.txt`{.markup--code
  .markup--li-code}]{#09dc}
- [This quickly reveals status codes, redirects, and components.]{#2132}

### Why Passive Endpoint Enumeration Matters {#b064 .graf .graf--h3 .graf-after--li name="b064"}

You might ask: "Why bother with this, when tools like
`gobuster`{.markup--code .markup--p-code} or `ffuf`{.markup--code
.markup--p-code} exist?" Great question. Here are the subtle advantages:

1.  [**No noise created externally**\
     Since all paths are already present in the DOM, you don't generate
    extra requests simply by scraping the HTML. That means **no extra
    traffic**, fewer firewall triggers, and you stay stealthier. This is
    particularly beneficial during bug bounties or internal pen tests
    where sudden spikes in endpoint requests could raise
    suspicion.]{#99fc}
2.  [**Uncover hidden gems**\
    Some pages are only linked via dynamic JavaScript or tucked inside
    `<noscript>`{.markup--code .markup--li-code} tags, but they are
    still visible to DevTools DOM scanning. This method lets you spot
    those without needing to comb through raw JS manually.]{#09c2}
3.  [**Easy, fast, toolchain-agnostic**\
    No installation required --- just open the browser, paste, and get
    results. Works across Chrome, Edge, Firefox, and Safari.]{#97fe}
4.  [**Great starting point**\
    Run it early to seed your target list before deeper fuzzing. You
    might gain enough endpoint data to skip intense brute-forcing
    altogether.]{#80f0}

### Enhancing the Technique {#4ea8 .graf .graf--h3 .graf-after--li name="4ea8"}

### 1. Include more tags beyond `<a>`{.markup--code .markup--h3-code} {#c212 .graf .graf--h3 .graf-after--h3 name="c212"}

Frequently, routes are referenced outside anchor tags --- in
`<script src=...>`{.markup--code .markup--p-code},
`<link href=...>`{.markup--code .markup--p-code},
`<img src=...>`{.markup--code .markup--p-code}, form actions, API calls,
etc.

Try this variant:

``` {#ac0a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="dart"}
(() => {
  const selectors = ["a[href]", "script[src]", "link[href]", "img[src]", "form[action]"];
  const paths = [...new Set(selectors.flatMap(sel =>
    [...document.querySelectorAll(sel)].map(el => {
      const attr = sel.includes("[href]") ? "href" :
                   sel.includes("[src]")   ? "src"  : "action";
      return new URL(el.getAttribute(attr), location.href).pathname;
    })
  ))];
```

``` {#d061 .graf .graf--pre .graf-after--pre}
  paths.forEach(p => console.log(p));
})();
```

### 2. Capture query parameters and fragments {#ef8c .graf .graf--h3 .graf-after--pre name="ef8c"}

Sometimes the full path matters:

``` {#d043 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
new URL(a.href, location.href).pathname +
  new URL(a.href, location.href).search + 
  new URL(a.href, location.href).hash;
```

Keep in mind that this increases noise and uniqueness --- so consider
deduplicating carefully.

### 3. Integrating into bookmarklets or automation {#2093 .graf .graf--h3 .graf-after--p name="2093"}

Make a handy bookmarklet:

``` {#002c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
javascript:(() => {
  /* same code as snippet #2 */,
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
})();
```

Click it anytime you're on a site and instantly get the paths file.

### 4. Combining with custom wordlists {#2a4b .graf .graf--h3 .graf-after--p name="2a4b"}

Use the downloaded file as input for:

**Burp Intruder**: identify hidden directories by fuzzing with these
endpoints.

**wfuzz, ffuf**: generate more combinations like
`/api/v1/posts`{.markup--code .markup--p-code},
`/api/v1/users`{.markup--code .markup--p-code}, etc.

**GitHub repos**: extract routes you can test against local dev or
staging environments.

### Ethical and Legal Considerations {#112f .graf .graf--h3 .graf-after--p name="112f"}

While passive enumeration is less invasive than brute forcing, it's
**not free from risk or boundaries**. Keep the following in mind:

**Respect** **`robots.txt`{.markup--code .markup--p-code}** **and**
**`sitemap.xml`{.markup--code .markup--p-code}**\
These are public signals about what the site does and doesn't want
crawled---better to check them before proceeding.

**Follow the law & authorization**\
Just because something is visible on the page doesn't mean it's yours to
explore. If you're doing bug bounty, always follow the program's scope.
If it's client work, get written permission.

**Avoid production risks**\
Don't overwhelm servers with repeated requests. Passive extraction is
safe, but subsequent probing might not be.

**Redact sensitive content responsibly**\
Some hidden paths might refer to staging or admin panels. Handle such
information with caution and don't leak them publicly without consent.

### Advanced Use Cases {#059f .graf .graf--h3 .graf-after--p name="059f"}

### Internal Pentest / Gray Box {#897d .graf .graf--h3 .graf-after--h3 name="897d"}

When you have partial credentials, run this on authenticated pages to
uncover internal assets: `/admin/dashboard`{.markup--code
.markup--p-code}, `/api/export`{.markup--code .markup--p-code},
`/maintenance`{.markup--code .markup--p-code}.

### Single Page Application (SPA) RECON {#234e .graf .graf--h3 .graf-after--p name="234e"}

SPAs often rely on JS-routed endpoints --- like
`/dashboard/settings`{.markup--code .markup--p-code} and
`/dashboard/profile`{.markup--code .markup--p-code}. Traditional
scanners won't see these. Passive DOM SCRAPING does!

Use DevTools after the SPA fully loads to capture all internal routes.

### Mobile Web Apps {#33fa .graf .graf--h3 .graf-after--p name="33fa"}

Same logic applies. Open URL in desktop browser, run the snippet, grab
endpoints for mobile-specific pages --- e.g., payment flows or profile
pages.

### Putting It All Together: Full Case Study {#917c .graf .graf--h3 .graf-after--p name="917c"}

Let's do a short walkthrough in a fictional scenario "AcmeCorp
e-commerce".

1.  [You access [`https://shop.acmecorp.example`{.markup--code
    .markup--li-code}](https://shop.acmecorp.example.){.markup--anchor
    .markup--li-anchor data-href="https://shop.acmecorp.example."
    rel="noopener"
    target="_blank"}[.](https://shop.acmecorp.example.){.markup--anchor
    .markup--li-anchor data-href="https://shop.acmecorp.example."
    rel="noopener" target="_blank"}]{#c714}
2.  [Run Snippet #2 → download `shop.acmecorp.example.txt`{.markup--code
    .markup--li-code}.]{#246b}
3.  [Inspect the file, see paths:]{#0bed}

- [`/ /products /products/awesome-widget /cart /checkout /user/profile /hidden-admin`{.markup--code
  .markup--li-code}]{#72cc}

1.  [The `/hidden-admin`{.markup--code .markup--li-code} path stands
    out---likely an admin panel.]{#8e93}
2.  [Write a simple script to probe `/hidden-admin`{.markup--code
    .markup--li-code} with HTTP HEAD or GET, determine access:]{#345b}

- [`for p in $(cat shop.acmecorp.example.txt); do curl -s -o /dev/null -w "%{http_code} $p\n" https://shop.acmecorp.example"$p"; done`{.markup--code
  .markup--li-code}]{#142c}

You find it returns 200, you're in. Now you're authorized and ready for
the deeper pentest.

### Conclusion {#1390 .graf .graf--h3 .graf-after--p name="1390"}

What you've learned today isn't just a neat trick --- it's a powerful
mindset. Passive endpoint RECON is stealthy, efficient, and surprisingly
potent. With just plain JavaScript in DevTools, you can unravel a site's
structure, seed your reconnaissance campaigns, and supercharge your
pentesting pipeline --- all without deploying heavy external tools or
generating suspicious traffic.

Remember, being ethical and scrupulous in applying these methods is just
as important as the technique itself. Use it only on authorized targets
and within well-defined scopes. With great power comes great
responsibility.

Enjoy hacking --- *ethically*!

### Promote and Collaborate on Cybersecurity Insights {#1912 .graf .graf--h3 .graf-after--p name="1912"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#15e9 .graf .graf--h3 .graf-after--p name="15e9"}

[Vijay
Gupta](https://www.youtube.com%2F@www.youtube.com/@bevijaygupta){.markup--anchor
.markup--p-anchor
data-href="https://www.youtube.com%2F@www.youtube.com/@bevijaygupta"
rel="noopener ugc nofollow noopener" target="_blank"} is a cybersecurity
enthusiast with several years of experience in cyber security, [cyber
crime forensics
investigation](https://play.google.com/store/books/series?id=_vUpHAAAABDW6M){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/series?id=_vUpHAAAABDW6M"
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
.h-card} on [June 9, 2025](https://medium.com/p/b20584fab44a).

[Canonical
link](https://medium.com/@bevijaygupta/passive-recon-with-devtools-extract-url-paths-b20584fab44a){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
