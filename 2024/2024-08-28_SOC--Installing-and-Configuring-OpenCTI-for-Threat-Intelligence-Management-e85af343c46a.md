---
title: "SOC  Installing and Configuring OpenCTI for Threat Intelligence Management e85af343c46a"
platform: Medium
original_file: 2024-08-28_SOC--Installing-and-Configuring-OpenCTI-for-Threat-Intelligence-Management-e85af343c46a.md
---

# SOC  Installing and Configuring OpenCTI for Threat Intelligence Management e85af343c46a

::: {}
# SOC: Installing and Configuring OpenCTI for Threat Intelligence Management {#soc-installing-and-configuring-opencti-for-threat-intelligence-management .p-name}
:::

::: {.section .p-summary field="subtitle"}
Introduction
:::

::::::: {.section .e-content field="body"}
:::::: {#ffc2 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### SOC: Installing and Configuring OpenCTI for Threat Intelligence Management {#f8d6 .graf .graf--h3 .graf--leading .graf--title name="f8d6"}

<figure id="e7d7" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*euOtglcSssbvbLYqSFkMUQ.png"
class="graf-image" data-image-id="1*euOtglcSssbvbLYqSFkMUQ.png"
data-width="2240" data-height="1260" data-is-featured="true" />
</figure>

### Introduction {#dc79 .graf .graf--h3 .graf-after--figure name="dc79"}

In the realm of cybersecurity, the ability to effectively manage,
analyze, and share threat intelligence is critical. A Security
Operations Center (SOC) often relies on various tools to collect and
process this intelligence. OpenCTI (Open Cyber Threat Intelligence) is
one such tool that has gained significant traction in recent years. It's
an open-source platform designed to manage cyber threat intelligence
(CTI) data and help security teams better understand and respond to
threats.

This blog will guide you through the complete process of installing and
configuring OpenCTI in a SOC environment. We will cover everything from
the basic concepts of OpenCTI, its features, the installation process,
and how to integrate it into your existing SOC infrastructure. Along the
way, we'll provide code snippets and configuration tips to ensure a
smooth setup.

### Understanding OpenCTI {#e4f7 .graf .graf--h3 .graf-after--p name="e4f7"}

OpenCTI is an open-source platform designed to manage cyber threat
intelligence data. It provides a comprehensive interface for analyzing,
visualizing, and sharing threat intelligence in a collaborative
environment. Built on modern web technologies, OpenCTI is highly
flexible and can integrate with various other security tools and
platforms.

#### Key Features of OpenCTI {#6056 .graf .graf--h4 .graf-after--p name="6056"}

1.  [**Data Ingestion and Normalization**: OpenCTI supports the
    ingestion of threat intelligence data from multiple sources,
    normalizing and enriching the data to provide a unified
    view.]{#35c6}
2.  [**Threat Actor Tracking**: The platform allows you to track and
    analyze threat actors, their tactics, techniques, and procedures
    (TTPs), and the indicators of compromise (IOCs) associated with
    them.]{#f3e8}
3.  [**Visualization**: OpenCTI offers powerful visualization tools that
    help in understanding the relationships between different entities,
    such as threat actors, vulnerabilities, and incidents.]{#b69c}
4.  [**Collaboration**: The platform facilitates collaboration among
    security teams, enabling the sharing of intelligence and insights
    across different departments and organizations.]{#ed7f}
5.  [**API and Integration**: OpenCTI comes with a robust API, making it
    easy to integrate with other security tools, such as SIEMs (Security
    Information and Event Management), SOAR (Security Orchestration,
    Automation, and Response) platforms, and more.]{#e1b9}

### Prerequisites for Installing OpenCTI {#3568 .graf .graf--h3 .graf-after--li name="3568"}

Before we begin with the installation, there are a few prerequisites
that need to be met:

**Operating System**: OpenCTI is typically installed on a Linux-based
system. Ubuntu 20.04 LTS is recommended, but other distributions like
CentOS or Debian can also be used.

**Hardware Requirements**:

- [**CPU**: 4 cores (8 cores recommended for production).]{#5880}
- [**RAM**: 16 GB (32 GB recommended for production).]{#61a7}
- [**Storage**: 100 GB (depending on the data volume).]{#63c3}

**Dependencies**:

- [Docker and Docker Compose.]{#b9e3}
- [Node.js and npm.]{#c27d}
- [Python 3.x.]{#7f03}
- [Redis.]{#888b}
- [Elasticsearch.]{#6349}
- [RabbitMQ.]{#bfc7}
- [PostgreSQL.]{#8138}

**Network Configuration**: Ensure that the system has a stable internet
connection, and the necessary ports (typically 3000 for the web
interface) are open.

### Step-by-Step Guide to Installing OpenCTI {#65a8 .graf .graf--h3 .graf-after--p name="65a8"}

Let's move forward with the installation process. We'll be using Docker
and Docker Compose to set up OpenCTI and its dependencies.

#### 1. Installing Docker and Docker Compose {#422d .graf .graf--h4 .graf-after--p name="422d"}

First, install Docker and Docker Compose on your system:

``` {#83f2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
# Update the package index
sudo apt-get update
```

``` {#f7e6 .graf .graf--pre .graf-after--pre}
# Install Docker
sudo apt-get install -y docker.io
```

``` {#782a .graf .graf--pre .graf-after--pre}
# Enable Docker service to start on boot
sudo systemctl enable docker
```

``` {#2ab7 .graf .graf--pre .graf-after--pre}
# Start Docker service
sudo systemctl start docker
```

``` {#4618 .graf .graf--pre .graf-after--pre}
# Verify Docker installation
docker --version
```

``` {#ec00 .graf .graf--pre .graf-after--pre}
# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

``` {#52a6 .graf .graf--pre .graf-after--pre}
# Apply executable permissions to the binary
sudo chmod +x /usr/local/bin/docker-compose
```

``` {#8f60 .graf .graf--pre .graf-after--pre}
# Verify Docker Compose installation
docker-compose --version
```

#### 2. Cloning the OpenCTI Repository {#7647 .graf .graf--h4 .graf-after--pre name="7647"}

Next, clone the OpenCTI GitHub repository:

``` {#973f .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
# Install Git if not already installed
sudo apt-get install -y git
```

``` {#62c2 .graf .graf--pre .graf-after--pre}
# Clone the OpenCTI repository
git clone https://github.com/OpenCTI-Platform/docker.git opencti
```

``` {#70d8 .graf .graf--pre .graf-after--pre}
# Navigate to the cloned directory
cd opencti
```

#### 3. Configuring Environment Variables {#d341 .graf .graf--h4 .graf-after--pre name="d341"}

Before running the Docker containers, you need to configure the
environment variables for OpenCTI. Create a `.env`{.markup--code
.markup--p-code} file in the OpenCTI directory with the following
content:

``` {#79e2 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
# OpenCTI
OPENCTI_ADMIN_EMAIL=admin@example.com
OPENCTI_ADMIN_PASSWORD=YourSecurePassword
OPENCTI_PORT=8080
# Database
OPENCTI_DATABASE_HOSTNAME=opencti-postgres
OPENCTI_DATABASE_PORT=5432
OPENCTI_DATABASE_USERNAME=opencti
OPENCTI_DATABASE_PASSWORD=YourSecurePassword
OPENCTI_DATABASE_NAME=opencti
# Elasticsearch
OPENCTI_ELASTICSEARCH_URL=http://opencti-elasticsearch:9200
# RabbitMQ
OPENCTI_RABBITMQ_HOSTNAME=opencti-rabbitmq
OPENCTI_RABBITMQ_PORT=5672
OPENCTI_RABBITMQ_USERNAME=opencti
OPENCTI_RABBITMQ_PASSWORD=YourSecurePassword
# Redis
OPENCTI_REDIS_HOSTNAME=opencti-redis
OPENCTI_REDIS_PORT=6379
```

Replace `admin@example.com`{.markup--code .markup--p-code} and
`YourSecurePassword`{.markup--code .markup--p-code} with your desired
admin email and secure password.

#### 4. Deploying OpenCTI with Docker Compose {#36ca .graf .graf--h4 .graf-after--p name="36ca"}

Now that the environment variables are configured, you can deploy
OpenCTI using Docker Compose:

``` {#7ea8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="graphql"}
# Launch the OpenCTI stack
sudo docker-compose up -d
```

Docker Compose will pull the necessary images and start the OpenCTI
containers, including PostgreSQL, Elasticsearch, Redis, RabbitMQ, and
the OpenCTI server.

#### 5. Verifying the Installation {#025e .graf .graf--h4 .graf-after--p name="025e"}

Once the containers are up and running, verify the installation by
accessing the OpenCTI web interface:

``` {#c7b6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
http://<your-server-ip>:8080
```

Log in using the admin credentials you specified in
the `.env`{.markup--code .markup--p-code} file. If everything is set up
correctly, you should see the OpenCTI dashboard.

### Configuring OpenCTI for SOC Operations {#f42d .graf .graf--h3 .graf-after--p name="f42d"}

After installing OpenCTI, the next step is to configure it to suit your
SOC's requirements. Here are some key configurations and integrations
that can enhance OpenCTI's capabilities:

#### 1. Data Sources and Connectors {#c0b1 .graf .graf--h4 .graf-after--p name="c0b1"}

OpenCTI supports a variety of data sources through connectors, which
allow you to import threat intelligence from external feeds, platforms,
and databases. Some popular connectors include:

- [**MISP Connector**: Integrates with MISP (Malware Information Sharing
  Platform) to pull threat intelligence data.]{#af21}
- [**VirusTotal Connector**: Pulls data from VirusTotal, a popular
  malware analysis service.]{#3238}
- [**AlienVault OTX Connector**: Integrates with the AlienVault Open
  Threat Exchange (OTX).]{#ce2e}

To configure a connector, navigate to the "Connectors" section in the
OpenCTI dashboard and follow the on-screen instructions. You may need to
configure API keys and other authentication details depending on the
connector.

#### 2. User Management and Access Control {#75fe .graf .graf--h4 .graf-after--p name="75fe"}

In a SOC, different team members may require different levels of access
to the OpenCTI platform. You can manage users and roles from the
"Administration" section of OpenCTI:

- [**Create Users**: Add new users with unique usernames and
  passwords.]{#4dfe}
- [**Assign Roles**: Define roles with specific permissions (e.g.,
  read-only, analyst, admin) and assign them to users.]{#556e}
- [**Two-Factor Authentication (2FA)**: Enable 2FA for enhanced
  security.]{#46cb}

#### 3. Creating and Managing Workspaces {#a73d .graf .graf--h4 .graf-after--li name="a73d"}

Workspaces in OpenCTI allow you to organize your threat intelligence
data into projects or investigations. Each workspace can contain
entities such as reports, incidents, observables, and relationships.
Here's how to create a workspace:

1.  [**Navigate to Workspaces**: Go to the "Workspaces" section from the
    main menu.]{#6476}
2.  [**Create a New Workspace**: Click on the "+" icon and fill in the
    required details (name, description, tags, etc.).]{#2230}
3.  [**Add Entities**: Start adding entities like threat actors,
    incidents, and IOCs to your workspace. You can link entities to show
    relationships.]{#85c1}

#### 4. Integrating with SIEM and SOAR Platforms {#264e .graf .graf--h4 .graf-after--li name="264e"}

To fully leverage OpenCTI within your SOC, you can integrate it with
your SIEM (e.g., Splunk, QRadar) and SOAR (e.g., TheHive, Cortex)
platforms. This integration allows automated ingestion of threat
intelligence data and seamless response to incidents.

For example, to integrate OpenCTI with Splunk:

1.  [**Install the OpenCTI Add-On for Splunk**: This can be done from
    Splunkbase or by manually downloading the add-on.]{#3f01}
2.  [**Configure API Access**: Set up API access in OpenCTI and
    configure the Splunk add-on with the API key and URL.]{#ba4c}
3.  [**Create Searches and Alerts**: Use the imported threat
    intelligence data to create searches, dashboards, and alerts in
    Splunk.]{#1a4d}

#### 5. Automation and Workflow Management {#2d66 .graf .graf--h4 .graf-after--li name="2d66"}

OpenCTI can be integrated with automation tools to streamline SOC
operations. You can use tools like Cortex, Ansible, or custom scripts to
automate tasks such as:

- [**Enriching IOCs**: Automatically enrich indicators of compromise
  with data from external sources.]{#d7e7}
- [**Incident Response**: Trigger automated responses (e.g., blocking
  IPs, disabling user accounts) based on threat intelligence.]{#8357}
- [**Reporting**: Generate automated reports for stakeholders.]{#bb70}

### Maintaining and Scaling OpenCTI {#e7bf .graf .graf--h3 .graf-after--li name="e7bf"}

Once OpenCTI is up and running, it's essential to maintain and scale the
platform as your SOC grows.

#### 1. Regular Backups {#beac .graf .graf--h4 .graf-after--p name="beac"}

Ensure that regular backups are taken for the OpenCTI database and
configuration files. You can use tools like `pg_dump`{.markup--code
.markup--p-code} for PostgreSQL and `rsync`{.markup--code
.markup--p-code} for file backups.

Example backup command for PostgreSQL:

``` {#b05a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
pg_dump -U opencti -h localhost -d opencti > /path/to/backup/opencti_backup.sql
```

#### 2. Monitoring and Logging {#baaa .graf .graf--h4 .graf-after--pre name="baaa"}

Monitor the health and performance of OpenCTI using tools like
Prometheus and Grafana. You should also configure logging for the
OpenCTI application and its components (Elasticsearch, RabbitMQ, etc.)
using tools like the ELK stack (Elasticsearch, Logstash, Kibana).

#### 3. Scaling {#46f6 .graf .graf--h4 .graf-after--p name="46f6"}

As the amount of data grows, you may need to scale the components of
OpenCTI:

- [**Horizontal Scaling**: Deploy additional nodes for Elasticsearch and
  PostgreSQL.]{#33a4}
- [**Vertical Scaling**: Increase the resources (CPU, RAM) allocated to
  the Docker containers.]{#c35d}
- [**Load Balancing**: Implement load balancers to distribute traffic
  across multiple OpenCTI instances.]{#b8d7}

### Conclusion {#108a .graf .graf--h3 .graf-after--li name="108a"}

OpenCTI is a powerful and flexible platform that can significantly
enhance your SOC's threat intelligence capabilities. By following the
steps outlined in this guide, you can successfully install, configure,
and integrate OpenCTI into your existing security infrastructure.
Whether you're tracking threat actors, managing incidents, or
collaborating with other security teams, OpenCTI provides the tools you
need to stay ahead of cyber threats.

As your SOC evolves, continue to explore the features and integrations
that OpenCTI offers. Regular updates and community contributions ensure
that OpenCTI remains a cutting-edge tool in the ever-changing landscape
of cybersecurity.

By mastering OpenCTI, your SOC will be better equipped to protect your
organization from the ever-growing number of cyber threats.

### Promote and Collaborate on Cybersecurity Insights {#ad40 .graf .graf--h3 .graf-after--p name="ad40"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#b0f0 .graf .graf--h3 .graf-after--p name="b0f0"}

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
.h-card} on [August 28, 2024](https://medium.com/p/e85af343c46a).

[Canonical
link](https://medium.com/@bevijaygupta/soc-installing-and-configuring-opencti-for-threat-intelligence-management-e85af343c46a){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
