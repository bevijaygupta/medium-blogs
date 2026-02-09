::: {}
# Proxy Tool For HTTP/HTTPS Traffic Capture {#proxy-tool-for-httphttps-traffic-capture .p-name}
:::

::: {.section .p-summary field="subtitle"}
Proxy Tool For HTTP/HTTPS Traffic Capture
:::

::::::: {.section .e-content field="body"}
:::::: {#e32f .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Proxy Tool For HTTP/HTTPS Traffic Capture {#4fa9 .graf .graf--h3 .graf--leading .graf--title name="4fa9"}

<figure id="9331" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*l3iCoU1THKOyNoNo.png"
class="graf-image" data-image-id="0*l3iCoU1THKOyNoNo.png"
data-width="640" data-height="157" />
</figure>

### Proxy Tool For HTTP/HTTPS Traffic Capture {#bc33 .graf .graf--h3 .graf-after--figure name="bc33"}

### From Binary {#e8e2 .graf .graf--h3 .graf-after--h3 name="e8e2"}

The installation is easy. You can download the pre-built binaries for
your platform from the
[Releases](https://github.com/projectdiscovery/proxify/releases/){.markup--anchor
.markup--p-anchor
data-href="https://github.com/projectdiscovery/proxify/releases/"
rel="noopener ugc nofollow noopener" target="_blank"} page. Extract them
using tar, move it to your `$PATH`{.markup--code .markup--p-code}and
you're ready to go.

``` {#53bb .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
tar -xvf proxify-linux-amd64.tarmv proxify-linux-amd64 /usr/local/bin/proxifyproxify -version
```

**proxify** requires **go1.14+** to install successfully. Run the
following command to get the repo --

### From Source {#7dae .graf .graf--h3 .graf-after--p name="7dae"}

``` {#1908 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
GO111MODULE=on go get -v github.com/projectdiscovery/proxify/cmd/proxify
```

### From Github {#eaf2 .graf .graf--h3 .graf-after--pre name="eaf2"}

``` {#f579 .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
git clone https://github.com/projectdiscovery/proxify.git; cd proxify/cmd/proxify; go build; cp proxify /usr/local/bin; proxify -version
```

### Usage {#5a23 .graf .graf--h3 .graf-after--pre name="5a23"}

``` {#614b .graf .graf--pre .graf-after--h3 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
proxify -h
```

This will display help for the tool. Here are all the switches it
supports.

FlagDescriptionExampleaddrListen HTTP IP and Portproxify -addr
127.0.0.1:8080configConfig data pathproxify -config
certscert-cache-sizeNumber of certificates to cacheproxify
-cert-cache-size 1024dns-addrListen DNS IP and Portproxify -dns-addr
'127.0.0.1:80'dns-mappingDNS A mappingproxify -dns-mapping
test.com:80dns-resolverListen DNS IP and Portproxify -dns-resolver
'127.0.0.1:5353'http-proxyUpstream HTTP Proxyproxify -http-proxy
hxxp://127.0.0.1:8080no-colorNo Color in outputproxify
-no-coloroutputOutput Folderproxify -output logsrequest-dslRequest
Filter DSLproxify -request-dsl
"contains(request,'admim')"request-match-replace-dslRequest
Match-Replace DSLproxify -request-match-replace-dsl
"replace(request,'false','true')"response-dslResponse Filter DSLproxify
-response-dsl "contains(response,
md5('test'))"response-match-replace-dslResponse Match-Replace DSLproxify
-response-match-replace-dsl "regex(response, '\^authentication
failed\$', 'authentication ok')"silentSilent outputproxify
-silentsocks5-proxyUpstream socks5 proxyproxify -socks5-proxy
socks5://proxy-ip:portvVerbose outputproxify -vversionCurrent
versionproxify -version

### Use Upstream proxy {#6486 .graf .graf--h3 .graf-after--p name="6486"}

Open a local proxy on port 8081 and forward the traffic to burp on port
8080

``` {#f4d6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
proxify -addr ":8081" -http-proxy http://127.0.0.1:8080
```

Open a local proxy on port 8080 and forward the traffic to the TOR
network

``` {#f086 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
proxify -socks5-proxy socks5://127.0.0.1:9050
```

### Dump all the HTTP/HTTPS traffic {#1075 .graf .graf--h3 .graf-after--pre name="1075"}

Dump all the traffic into separate files with request followed by the
response, as default `proxify`{.markup--code .markup--p-code} listen to
`http://127.0.0.0:8080`{.markup--code .markup--p-code}. Custom address
and port can be defined using `addr`{.markup--code .markup--p-code}
flag.

As default, proxied request/resposed are stored in the
`logs`{.markup--code .markup--p-code} folder.

``` {#3f68 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
proxify -output db
```

### Hostname mapping with Local DNS resolver {#506f .graf .graf--h3 .graf-after--pre name="506f"}

Proxify supports embedding DNS resolver to map hostnames to specific
addresses and define an upstream dns server for any other domain name

start a local http proxy on port 8080 using an embedded dns server
listening on port 53 and resolving
[www.google.it](https://www.google.it/){.markup--anchor
.markup--p-anchor data-href="https://www.google.it/"
rel="noopener ugc nofollow noopener" target="_blank"} to 192.168.1.1,
all other fqdn are forwarded upstream to 1.1.1.1

``` {#4e5a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
proxify -dns-addr ":53" -dns-mapping "www.google.it:192.168.1.1" -dns-resolver "1.1.1.1:53"
```

This feature is used for example by the `replay`{.markup--code
.markup--p-code} utility to hijack the connections and simulate
responses. It may be useful during internal assessments with private DNS
servers. Using `*`{.markup--code .markup--p-code} as domain name matches
all dns requests.

### Match/Filter traffic with DSL language. {#7377 .graf .graf--h3 .graf-after--p name="7377"}

If the request or response match the filters the dump is tagged
with `.match.txt`{.markup--code .markup--p-code} suffix:

``` {#316e .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="scss"}
proxify -request-dsl "contains(request,'firefox')" -response-dsl "contains(response, md5('test'))"
```

### Match and Replace on the fly {#a331 .graf .graf--h3 .graf-after--pre name="a331"}

Proxify supports modifying Requests and Responses on the fly with DSL
language.

``` {#e4e3 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
proxify -request-match-replace-dsl "replace(request,'firefox','chrome')" -response-match-replace-dsl "regex(response, '^authentication failed$', 'authentication ok')"
```

### Replay all traffic into burp {#bf25 .graf .graf--h3 .graf-after--pre name="bf25"}

Replay all the dumped requests/responses into the destination URL
([http://127.0.0.1:8080](http://127.0.0.1:8080/){.markup--anchor
.markup--p-anchor data-href="http://127.0.0.1:8080/"
rel="noopener ugc nofollow noopener" target="_blank"}) if not specified.
For this to work, it's necessary to configure burp to use proxify as an
upstream proxy, as it will take care to hijack the DNS resolutions and
simulate the remote server with the dumped request. This allows having
in the burp history exactly all requests/responses as if they were
originally sent through it, allowing for example to perform a remote
interception on the cloud, and merge all results locally within burp.

``` {#6bd8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
replay -output "logs/"
```

### Installing SSL Certificate {#0ca4 .graf .graf--h3 .graf-after--pre name="0ca4"}

A certificate authority is generated for proxify which is stored in the
folder `~/.config/proxify/`{.markup--code .markup--p-code} as default,
manually can be specified by `-config`{.markup--code .markup--p-code}
flag. The generated certificate can be imported by visiting
[http://proxify/cacert.crt](http://proxify/cacert.crt){.markup--anchor
.markup--p-anchor data-href="http://proxify/cacert.crt"
rel="noopener ugc nofollow noopener" target="_blank"} in a browser
connected to proxify.

Installation steps for the Root Certificate are similar to other proxy
tools which include adding the cert to the system trusted root store.

### Applications of Proxify {#f7f4 .graf .graf--h3 .graf-after--p name="f7f4"}

Proxify can be used in multiple places. Here are some common example
where Proxify comes in handy:-

Storing all the burp proxy history logs locally. Store all your browse
history locally. Store all the response of while you fuzz as per you
config at run time.

### Promote and Collaborate on Cybersecurity Insights {#b980 .graf .graf--h3 .graf-after--p name="b980"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#1e12 .graf .graf--h3 .graf-after--p name="1e12"}

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
.h-card} on [July 14, 2024](https://medium.com/p/9b3895cf0913).

[Canonical
link](https://medium.com/@bevijaygupta/proxy-tool-for-http-https-traffic-capture-9b3895cf0913){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
