::: {}
# Behind the Code: Building eLocationTrackerBot --- A Telegram Bot for Location Tracking {#behind-the-code-building-elocationtrackerbot-a-telegram-bot-for-location-tracking .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction
:::

::::::: {.section .e-content field="body"}
:::::: {#fe21 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### **Behind the Code: Building eLocationTrackerBot --- A Telegram Bot for Location Tracking** {#d459 .graf .graf--h3 .graf--leading .graf--title name="d459"}

<figure id="bc02" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*P38rebE3A7o3ATb7"
class="graf-image" data-image-id="0*P38rebE3A7o3ATb7" data-width="1140"
data-height="694" data-is-featured="true" />
</figure>

**Introduction**

In an age where digital footprints are becoming larger and more
traceable, developing tools for cybersecurity research and awareness is
more important than ever. As a cybersecurity enthusiast and developer, I
recently built my first Telegram bot named **"eLocationTrackerBot"**.
The purpose of this bot is simple yet powerful: to identify the location
of a person through multiple vectors like IP addresses, phone numbers,
email headers, and even cleverly engineered image URLs.

This blog aims to document the complete development process of
eLocationTrackerBot, its use-cases, ethical boundaries, features,
limitations, and most importantly, how it works. Whether you're a fellow
developer looking to build a similar bot, a cybersecurity learner
exploring digital forensics, or someone curious about the technology
behind location tracking, this detailed breakdown is for you.

### 1. What is eLocationTrackerBot? {#9e0f .graf .graf--h3 .graf-after--p name="9e0f"}

eLocationTrackerBot is a custom Telegram bot designed to collect
geolocation-related data using the following four techniques:

- [**IP Tracking**: Extracts geolocation data from IP addresses.]{#dcb2}
- [**Phone Number Analysis**: Uses number lookup to determine
  location.]{#5502}
- [**Email Header Parsing**: Extracts IP and location from email
  metadata.]{#a487}
- [**Image-based IP Logging**: A social engineering technique that
  embeds tracking URLs into images.]{#b844}

This bot is aimed at ethical use only --- for cybersecurity awareness,
red teaming exercises, or educational purposes.

### 2. Understanding the Use Cases {#8127 .graf .graf--h3 .graf-after--p name="8127"}

- [**Digital Forensics**: Assists in tracing attackers or suspicious
  activities through IP or email headers.]{#3579}
- [**Phishing Awareness**: Demonstrates how social engineering through
  image links can be dangerous.]{#ff02}
- [**Cybersecurity Training**: Used in ethical hacking and penetration
  testing workshops.]{#52eb}
- [**Incident Response**: Helps teams identify approximate locations of
  attackers.]{#c1f2}

### 3. Tools and Technologies Used {#d080 .graf .graf--h3 .graf-after--li name="d080"}

- [**Python**: Core programming language.]{#4523}
- [**python-telegram-bot**: For creating the Telegram bot.]{#2fe7}
- [**ipwhois, ip2geotools, or ipapi**: For IP geolocation.]{#9a0f}
- [**Numverify API / Truecaller API (Unofficial)**: For phone number
  analysis.]{#da80}
- [**Email Parser Libraries**: To parse and extract email header
  data.]{#6194}
- [**Webhook + Flask**: To serve tracking image URLs.]{#7742}
- [**Ngrok / VPS Hosting**: To make your local server publicly
  accessible.]{#b7c3}

### 4. Architecture Overview {#106d .graf .graf--h3 .graf-after--li name="106d"}

1.  [**User sends a command** to the bot.]{#1060}
2.  [**Bot processes the input**, whether it's an IP, phone number, or
    email header.]{#28dc}
3.  [**Performs external API lookups** and returns the geolocation
    data.]{#c2dc}
4.  [For image tracking:]{#d4c6}

- [A unique tracking URL is generated.]{#cc3c}
- [When the victim opens the image, it logs their IP and
  timestamp.]{#f53b}

### 5. Core Features and Functionalities {#2af4 .graf .graf--h3 .graf-after--li name="2af4"}

- [`/start`{.markup--code .markup--li-code} - Starts the bot.]{#d94d}
- [`/ip <IP Address>`{.markup--code .markup--li-code} - Tracks and
  locates the IP.]{#97db}
- [`/phone <Phone Number>`{.markup--code .markup--li-code} - Returns
  geolocation info.]{#5b6e}
- [`/email <Raw Email Header>`{.markup--code .markup--li-code} - Parses
  and returns IP info.]{#62f4}
- [`/image`{.markup--code .markup--li-code} - Generates a tracking URL
  image.]{#13d9}
- [**Logging** --- All activities are logged for the developer.]{#b9bc}

### 6. Step-by-Step Development Breakdown {#df5e .graf .graf--h3 .graf-after--li name="df5e"}

#### Step 1: Bot Setup {#37d5 .graf .graf--h4 .graf-after--h3 name="37d5"}

Register your bot with BotFather on Telegram. Get your API key.

``` {#cd2f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters
updater = Updater('YOUR_BOT_TOKEN', use_context=True)
dp = updater.dispatcher
```

#### Step 2: IP Tracking Function {#3fcd .graf .graf--h4 .graf-after--pre name="3fcd"}

``` {#3434 .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
def ip_lookup(update, context):
    ip = context.args[0]
    # Use ipwhois or ipapi
    data = requests.get(f"http://ip-api.com/json/{ip}").json()
    result = f"City: {data['city']}, Country: {data['country']}, ISP: {data['isp']}"
    update.message.reply_text(result)
```

#### Step 3: Phone Number Lookup {#a4eb .graf .graf--h4 .graf-after--pre name="a4eb"}

``` {#5768 .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
def phone_lookup(update, context):
    phone = context.args[0]
    # Use Numverify or similar API
    data = requests.get(f"https://api.numverify.com/lookup?number={phone}&access_key=YOUR_KEY").json()
    update.message.reply_text(f"Location: {data['location']}, Carrier: {data['carrier']}")
```

#### Step 4: Email Header Parser {#64d8 .graf .graf--h4 .graf-after--pre name="64d8"}

``` {#1f3e .graf .graf--pre .graf-after--h4 .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
from email.parser import Parser
```

``` {#4163 .graf .graf--pre .graf-after--pre}
def parse_email(update, context):
    raw_header = ' '.join(context.args)
    email = Parser().parsestr(raw_header)
    ip_lines = [line for line in raw_header.splitlines() if 'Received:' in line]
    update.message.reply_text("\n".join(ip_lines))
```

#### Step 5: Image Tracking Module {#0266 .graf .graf--h4 .graf-after--pre name="0266"}

- [Generate a unique URL for every tracking image.]{#c0ed}
- [Set up a Flask server to listen and log IP info.]{#fd9a}

``` {#f8fa .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
from flask import Flask, request, send_file
import time, logging
```

``` {#f140 .graf .graf--pre .graf-after--pre}
app = Flask(__name__)
```

``` {#bc33 .graf .graf--pre .graf-after--pre}
@app.route('/track/<user_id>.png')
def track(user_id):
    ip = request.remote_addr
    with open('log.txt', 'a') as f:
        f.write(f"User: {user_id} IP: {ip} Time: {time.ctime()}\n")
    return send_file("tracker.png", mimetype='image/png')
```

- [Provide this URL to the bot user so they can send it to
  others.]{#e2ba}

### 7. Handling Image-based Tracking {#130e .graf .graf--h3 .graf-after--li name="130e"}

This is the most sensitive and powerful feature of the bot. When users
send the tracking image to someone (victim or attacker), the backend
server logs the IP address the moment the image is loaded.

**Caution:** This must only be used for educational or lawful
cybersecurity purposes.

### 8. Ethical Considerations and Legal Boundaries {#c1e1 .graf .graf--h3 .graf-after--p name="c1e1"}

The tool should never be used for illegal surveillance, stalking, or
harassment. eLocationTrackerBot is designed with the intent of spreading
cybersecurity awareness and should be deployed in controlled
environments.

- [Always get consent before testing on individuals.]{#9a98}
- [Make sure you comply with GDPR and other data laws.]{#30a3}
- [Use disclaimers and restrict usage via bot messages.]{#f1bd}

### 9. Deployment and Hosting {#fef9 .graf .graf--h3 .graf-after--li name="fef9"}

- [For development: Use **Ngrok** to tunnel localhost.]{#9812}
- [For production: Host the Flask server on a VPS or cloud (like AWS,
  Heroku).]{#a2ac}
- [Set up a secure reverse proxy (e.g., Nginx with HTTPS).]{#fa98}
- [Monitor logs and bot usage to prevent misuse.]{#d195}

### 10. Challenges and Solutions {#b1d2 .graf .graf--h3 .graf-after--li name="b1d2"}

- [**Telegram rate limits**: Optimize API calls and cache
  results.]{#60fc}
- [**IP logging abuse**: Restrict who can generate tracking
  URLs.]{#2c58}
- [**False positives in email headers**: Implement smart
  filters.]{#2352}
- [**Phone number lookups blocked by region**: Use multiple fallback
  APIs.]{#d3f9}

### 11. Future Improvements {#f509 .graf .graf--h3 .graf-after--li name="f509"}

- [Add GUI frontend for non-technical users.]{#cf70}
- [Store logs in a database like SQLite or MongoDB.]{#96f0}
- [Add reverse image search integration.]{#a0cb}
- [Enable batch processing for bulk IPs or emails.]{#0753}
- [Add user authentication and admin dashboard.]{#89db}

### 12. Conclusion {#0fa1 .graf .graf--h3 .graf-after--li name="0fa1"}

eLocationTrackerBot was not just a technical project --- it was a
journey into the world of geolocation, digital forensics, and ethical
hacking. While powerful, tools like this come with a heavy
responsibility. As developers, we must ensure our work contributes to
making the internet safer and more aware.

If you're thinking of building a similar tool, remember: the line
between ethical hacking and malicious behavior is defined by **intent
and consent**. Keep learning, stay ethical, and use technology for good.

**Disclaimer**: This tool and blog are intended for educational and
ethical purposes only. The author does not condone or encourage illegal
tracking or surveillance of individuals.

### Promote and Collaborate on Cybersecurity Insights {#e210 .graf .graf--h3 .graf-after--p name="e210"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#570a .graf .graf--h3 .graf-after--p name="570a"}

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
.h-card} on [May 19, 2025](https://medium.com/p/93e252db0648).

[Canonical
link](https://medium.com/@bevijaygupta/behind-the-code-building-elocationtrackerbot-a-telegram-bot-for-location-tracking-93e252db0648){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
