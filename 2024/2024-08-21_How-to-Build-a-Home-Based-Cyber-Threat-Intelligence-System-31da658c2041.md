---
title: "How to Build a Home Based Cyber Threat Intelligence System 31da658c2041"
platform: Medium
original_file: 2024-08-21_How-to-Build-a-Home-Based-Cyber-Threat-Intelligence-System-31da658c2041.md
---

# How to Build a Home Based Cyber Threat Intelligence System 31da658c2041

::: {}
# How to Build a Home-Based Cyber Threat Intelligence System {#how-to-build-a-home-based-cyber-threat-intelligence-system .p-name}
:::

::: {.section .p-summary field="subtitle"}
What is Threat Intelligence?
:::

::::::: {.section .e-content field="body"}
:::::: {#1936 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### How to Build a Home-Based Cyber Threat Intelligence System {#85de .graf .graf--h3 .graf--leading .graf--title name="85de"}

### What is Threat Intelligence? {#d93e .graf .graf--h3 .graf-after--h3 name="d93e"}

> ***Threat intelligence involves analysing evidence-based information
> about cyber attacks, enabling cyber security experts to identify
> issues contextually and create targeted solutions for the detected
> problems.***

> *Rooted in data, similar to open source intelligence (OSINT), threat
> intelligence provides context --- like who is attacking you, what
> their motivation and capabilities are, and what indicators of
> compromise (IOCs) in your systems to look for --- that helps you make
> informed decisions about your security.*

> ***---*** [***Recorded
> Future***](https://www.recordedfuture.com/threat-intelligence){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://www.recordedfuture.com/threat-intelligence"
> rel="noopener ugc nofollow noopener" target="_blank"}

It is important to note that within the topic of Cyber Threat
Intelligence (CTI), there are several important subtopics to understand;
Indicators of compromise and Advanced Persistent Threats and Traffic
Light Protocol are three key areas to study in relation to CTI.

### Indicators of Compromise (IOCs) {#c3ce .graf .graf--h3 .graf-after--p name="c3ce"}

Indicators of compromise refer to data which can indicate that an
organization may have been compromised by external actor. They are used
by security teams to enrich logs in the SIEM so that, for example, if a
new domain is marked as as malicious by a threat intelligence provider,
and activity is detected between an organization an the domain, the
security team should be alerted and conduct an investigation.

Types of IOC data include:

- [IP Addresses]{#aee7}
- [Domain names]{#d3ea}
- [Malicious file names]{#da8c}
- [File Hashes]{#733d}
- [URLs]{#291e}

### Advanced Persistent Threats (APTs) {#8c4e .graf .graf--h3 .graf-after--li name="8c4e"}

> *An advanced persistent threat (APT) is a sophisticated, sustained
> cyberattack in which an intruder establishes an undetected presence in
> a network in order to steal sensitive data over a prolonged period of
> time. An APT attack is carefully planned and designed to infiltrate a
> specific organization, evade existing security measures and fly under
> the radar.*

> ***---***
> [***Crowdstrike***](https://www.crowdstrike.com/cybersecurity-101/advanced-persistent-threat-apt/){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://www.crowdstrike.com/cybersecurity-101/advanced-persistent-threat-apt/"
> rel="noopener ugc nofollow noopener" target="_blank"}

APTs are tracked in several ways by different organizations. MITRE
tracks APTs using a numbering system, whereas Crowdstrike refers to them
by a name, typically associated with the country of origin. For example,
MITRE refers to Russia's General Staff Main Intelligence Directorate
(GRU) as **APT28**, whereas Crowdstrike refers to them as **Fancy
Bear.**

- [Crowdstrike:
  [https://www.crowdstrike.com/adversaries/](https://www.crowdstrike.com/adversaries/){.markup--anchor
  .markup--li-anchor
  data-href="https://www.crowdstrike.com/adversaries/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#38ba}
- [MITRE:
  [https://attack.mitre.org/groups/](https://attack.mitre.org/groups/){.markup--anchor
  .markup--li-anchor data-href="https://attack.mitre.org/groups/"
  rel="noopener ugc nofollow noopener" target="_blank"}]{#665b}

### Traffic Light Protocol {#2981 .graf .graf--h3 .graf-after--li name="2981"}

> *The Traffic Light Protocol (TLP) was created in order to facilitate
> greater sharing of information. TLP is a set of designations used to
> ensure that sensitive information is shared with the appropriate
> audience. It employs four colors to indicate expected sharing
> boundaries to be applied by the recipient(s)*

> *---* [***Cyber Security Infrastructure Security
> Agency***](https://www.cisa.gov/news-events/news/traffic-light-protocol-tlp-definitions-and-usage){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://www.cisa.gov/news-events/news/traffic-light-protocol-tlp-definitions-and-usage"
> rel="noopener ugc nofollow noopener" target="_blank"}

- [**TLP: RED --- **Not for disclosure, restricted to participants
  only.]{#c86a}
- [**TLP: Amber+Strict --- **Limited disclosure, restricted to
  participants' organization.]{#6c26}
- [**TLP: Amber --- **Limited disclosure, restricted to participants'
  organization and its clients (see Terminology Definitions).]{#3ba6}
- [**TLP: Green --- **Limited disclosure, restricted to the
  community.]{#9fec}
- [**TLP: Clear --- **Disclosure is not limited.]{#8cf9}

### What is OpenCTI? {#8fa6 .graf .graf--h3 .graf-after--li name="8fa6"}

> *OpenCTI is an open source platform allowing organizations to manage
> their cyber threat intelligence knowledge and observables. It has been
> created in order to structure, store, organize and visualize technical
> and non-technical information about cyber threats.*

> *The structuration of the data is performed using a knowledge schema
> based on the* [*STIX2
> standards*](https://oasis-open.github.io/cti-documentation/){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://oasis-open.github.io/cti-documentation/"
> rel="noopener ugc nofollow noopener" target="_blank"}*. It has been
> designed as a modern web application including a* [*GraphQL
> API*](https://graphql.org/){.markup--anchor .markup--blockquote-anchor
> data-href="https://graphql.org/" rel="noopener ugc nofollow noopener"
> target="_blank"} *and an UX oriented frontend. Also, OpenCTI can be
> integrated with other tools and applications such as*
> [*MISP*](https://github.com/MISP/MISP){.markup--anchor
> .markup--blockquote-anchor data-href="https://github.com/MISP/MISP"
> rel="noopener ugc nofollow noopener" target="_blank"}*,*
> [*TheHive*](https://github.com/TheHive-Project/TheHive){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://github.com/TheHive-Project/TheHive"
> rel="noopener ugc nofollow noopener" target="_blank"}*,* [*MITRE
> ATT&CK*](https://github.com/mitre/cti){.markup--anchor
> .markup--blockquote-anchor data-href="https://github.com/mitre/cti"
> rel="noopener ugc nofollow noopener" target="_blank"}*, etc.*

> *---*
> [***OpenCTI***](https://github.com/OpenCTI-Platform/opencti){.markup--anchor
> .markup--blockquote-anchor
> data-href="https://github.com/OpenCTI-Platform/opencti"
> rel="noopener ugc nofollow noopener" target="_blank"}

OpenCTI is free to setup and run, consuming threat intelligence from
open source and propriety threat feeds. It is ideal for using for a home
lab on docker, although you can deploy to an organization (recommended
to use Kubernetes). Once you start pulling data from threat feeds, you
can very quickly get access to IOCs, threat reports, attack techniques,
and more. The platform will automatically correlate similar threat
intelligence so you can correlate multiple threat feeds to single
entities.

<figure id="0448" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*DWM8W_AMg9PKl_xA.png"
class="graf-image" data-image-id="0*DWM8W_AMg9PKl_xA.png"
data-width="1125" data-height="590" data-is-featured="true" />
</figure>

### Setup and Install OpenCTI {#c4f4 .graf .graf--h3 .graf-after--figure name="c4f4"}

For people who are less experienced installing and running docker, I
suggest using [Docker
Desktop](https://docs.docker.com/desktop/install/windows-install/){.markup--anchor
.markup--p-anchor
data-href="https://docs.docker.com/desktop/install/windows-install/"
rel="noopener ugc nofollow noopener" target="_blank"}, then installing
Portainer. Portainer provides a web interface and makes it very easy to
work with the docker daemon, which should make deploying OpenCTI much
easier.

### Install Portainer --- Full install guide [here](https://docs.portainer.io/start/install-ce/server/docker/wsl){.markup--anchor .markup--h3-anchor data-href="https://docs.portainer.io/start/install-ce/server/docker/wsl" rel="noopener ugc nofollow noopener" target="_blank"} {#28cb .graf .graf--h3 .graf-after--p name="28cb"}

1.  [Create Docker volume]{#0003}

``` {#a86a .graf .graf--pre .graf-after--li .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
docker volume create portainer_data
```

<figure id="14d5" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/0*fcqLf9MhsE4eoxAV.png"
class="graf-image" data-image-id="0*fcqLf9MhsE4eoxAV.png"
data-width="788" data-height="257" />
</figure>

2\. Run Portainer

``` {#1023 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="javascript"}
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

3\. You will see the following once it has completed pulling the image.

<figure id="60c6" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*QDeNCuGC_fJRbqcS.png"
class="graf-image" data-image-id="0*QDeNCuGC_fJRbqcS.png"
data-width="738" data-height="325" />
</figure>

4\. The Portainer container is now running and available to connect

<figure id="c34b" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*YnJFAKrcukAfLz98.png"
class="graf-image" data-image-id="0*YnJFAKrcukAfLz98.png"
data-width="788" data-height="259" />
</figure>

### Setup Portainer {#64b3 .graf .graf--h3 .graf-after--figure name="64b3"}

1\. Connect to the new container using the following URL:
[https://localhost:9443](https://localhost:9443/){.markup--anchor
.markup--p-anchor data-href="https://localhost:9443/"
rel="noopener ugc nofollow" target="_blank"}. Replace
`localhost`{.markup--code .markup--p-code} with the relevant IP address
or FQDN if needed, and adjust the port if you changed it earlier.

2\. Create a password for the admin user.

<figure id="3fc2" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*bcDj2UWgtbJT3E9g.png"
class="graf-image" data-image-id="0*bcDj2UWgtbJT3E9g.png"
data-width="788" data-height="456" />
</figure>

3\. Click Get Started.

<figure id="c04a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*3bAhT3Xwljc7Ho3A.png"
class="graf-image" data-image-id="0*3bAhT3Xwljc7Ho3A.png"
data-width="788" data-height="541" />
</figure>

4\. Click **Live Connect**

<figure id="abfb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*MddjwDNg3s81Q4PF.png"
class="graf-image" data-image-id="0*MddjwDNg3s81Q4PF.png"
data-width="788" data-height="240" />
</figure>

Take some time to explore the dashboard and familiarise yourself with
the configuration.

### Setup OpenCTI --- Create Portainer Stack (Docker Compose) {#8662 .graf .graf--h3 .graf-after--p name="8662"}

1\. Click On Stacks and create stack. Enter the name **opencti**

<figure id="fc20" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*88pUK1b7zn_2PqUx.png"
class="graf-image" data-image-id="0*88pUK1b7zn_2PqUx.png"
data-width="1125" data-height="810" />
</figure>

2\. Below is an example docker compose file which cane be used for the
Stack. Copy and paste to the Web Editor Window.

``` {#254b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
version: '3'
services:
  redis:
    image: redis:7.2.5
    restart: always
    volumes:
      - redisdata:/data
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.13.4
    volumes:
      - esdata:/usr/share/elasticsearch/data
    environment:
      # Comment-out the line below for a cluster of multiple nodes
      - discovery.type=single-node
      # Uncomment the line below below for a cluster of multiple nodes
      # - cluster.name=docker-cluster
      - xpack.ml.enabled=false
      - xpack.security.enabled=false
      - thread_pool.search.queue_size=5000
      - logger.org.elasticsearch.discovery="ERROR"
      - "ES_JAVA_OPTS=-Xms${ELASTIC_MEMORY_SIZE} -Xmx${ELASTIC_MEMORY_SIZE}"
    restart: always
    ulimits:
      memlock:
        soft: -1
        hard: -1
      nofile:
        soft: 65536
        hard: 65536
  minio:
    image: minio/minio:RELEASE.2024-05-28T17-19-04Z # Use "minio/minio:RELEASE.2024-05-28T17-19-04Z-cpuv1" to troubleshoot compatibility issues with CPU
    volumes:
      - s3data:/data
    ports:
      - "9000:9000"
    environment:
      MINIO_ROOT_USER: ${MINIO_ROOT_USER}
      MINIO_ROOT_PASSWORD: ${MINIO_ROOT_PASSWORD}    
    command: server /data
    restart: always
  rabbitmq:
    image: rabbitmq:3.13-management
    environment:
      - RABBITMQ_DEFAULT_USER=${RABBITMQ_DEFAULT_USER}
      - RABBITMQ_DEFAULT_PASS=${RABBITMQ_DEFAULT_PASS}
      - RABBITMQ_NODENAME=rabbit01@localhost
    volumes:
      - amqpdata:/var/lib/rabbitmq
    restart: always
  opencti:
    image: opencti/platform:6.2.11
    environment:
      - NODE_OPTIONS=--max-old-space-size=8096
      - APP__PORT=8080
      - APP__BASE_URL=${OPENCTI_BASE_URL}
      - APP__ADMIN__EMAIL=${OPENCTI_ADMIN_EMAIL}
      - APP__ADMIN__PASSWORD=${OPENCTI_ADMIN_PASSWORD}
      - APP__ADMIN__TOKEN=${OPENCTI_ADMIN_TOKEN}
      - APP__APP_LOGS__LOGS_LEVEL=error
      - REDIS__HOSTNAME=redis
      - REDIS__PORT=6379
      - ELASTICSEARCH__URL=http://elasticsearch:9200
      - MINIO__ENDPOINT=minio
      - MINIO__PORT=9000
      - MINIO__USE_SSL=false
      - MINIO__ACCESS_KEY=${MINIO_ROOT_USER}
      - MINIO__SECRET_KEY=${MINIO_ROOT_PASSWORD}
      - RABBITMQ__HOSTNAME=rabbitmq
      - RABBITMQ__PORT=5672
      - RABBITMQ__PORT_MANAGEMENT=15672
      - RABBITMQ__MANAGEMENT_SSL=false
      - RABBITMQ__USERNAME=${RABBITMQ_DEFAULT_USER}
      - RABBITMQ__PASSWORD=${RABBITMQ_DEFAULT_PASS}
      - SMTP__HOSTNAME=${SMTP_HOSTNAME}
      - SMTP__PORT=25
      - PROVIDERS__LOCAL__STRATEGY=LocalStrategy
    ports:
      - "8080:8080"
    depends_on:
      - redis
      - elasticsearch
      - minio
      - rabbitmq
    restart: always
  worker:
    image: opencti/worker:6.2.11
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - WORKER_LOG_LEVEL=info
    depends_on:
      - opencti
    deploy:
      mode: replicated
      replicas: 3
    restart: always
  connector-export-file-stix:
    image: opencti/connector-export-file-stix:6.2.11
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - CONNECTOR_ID=${CONNECTOR_EXPORT_FILE_STIX_ID} # Valid UUIDv4
      - CONNECTOR_TYPE=INTERNAL_EXPORT_FILE
      - CONNECTOR_NAME=ExportFileStix2
      - CONNECTOR_SCOPE=application/json
      - CONNECTOR_LOG_LEVEL=info
    restart: always
    depends_on:
      - opencti
  connector-export-file-csv:
    image: opencti/connector-export-file-csv:6.2.11
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - CONNECTOR_ID=${CONNECTOR_EXPORT_FILE_CSV_ID} # Valid UUIDv4
      - CONNECTOR_TYPE=INTERNAL_EXPORT_FILE
      - CONNECTOR_NAME=ExportFileCsv
      - CONNECTOR_SCOPE=text/csv
      - CONNECTOR_LOG_LEVEL=info
    restart: always
    depends_on:
      - opencti
  connector-export-file-txt:
    image: opencti/connector-export-file-txt:6.2.11
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - CONNECTOR_ID=${CONNECTOR_EXPORT_FILE_TXT_ID} # Valid UUIDv4
      - CONNECTOR_TYPE=INTERNAL_EXPORT_FILE
      - CONNECTOR_NAME=ExportFileTxt
      - CONNECTOR_SCOPE=text/plain
      - CONNECTOR_LOG_LEVEL=info
    restart: always
    depends_on:
      - opencti
  connector-import-file-stix:
    image: opencti/connector-import-file-stix:6.2.11
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - CONNECTOR_ID=${CONNECTOR_IMPORT_FILE_STIX_ID} # Valid UUIDv4
      - CONNECTOR_TYPE=INTERNAL_IMPORT_FILE
      - CONNECTOR_NAME=ImportFileStix
      - CONNECTOR_VALIDATE_BEFORE_IMPORT=true # Validate any bundle before import
      - CONNECTOR_SCOPE=application/json,text/xml
      - CONNECTOR_AUTO=true # Enable/disable auto-import of file
      - CONNECTOR_LOG_LEVEL=info
    restart: always
    depends_on:
      - opencti
  connector-import-document:
    image: opencti/connector-import-document:6.2.11
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - CONNECTOR_ID=${CONNECTOR_IMPORT_DOCUMENT_ID} # Valid UUIDv4
      - CONNECTOR_TYPE=INTERNAL_IMPORT_FILE
      - CONNECTOR_NAME=ImportDocument
      - CONNECTOR_VALIDATE_BEFORE_IMPORT=true # Validate any bundle before import
      - CONNECTOR_SCOPE=application/pdf,text/plain,text/html
      - CONNECTOR_AUTO=true # Enable/disable auto-import of file
      - CONNECTOR_ONLY_CONTEXTUAL=false # Only extract data related to an entity (a report, a threat actor, etc.)
      - CONNECTOR_CONFIDENCE_LEVEL=15 # From 0 (Unknown) to 100 (Fully trusted)
      - CONNECTOR_LOG_LEVEL=info
      - IMPORT_DOCUMENT_CREATE_INDICATOR=true
    restart: always
    depends_on:
      - opencti
  connector-analysis:
    image: opencti/connector-import-document:6.2.11
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - CONNECTOR_ID=${CONNECTOR_ANALYSIS_ID} # Valid UUIDv4
      - CONNECTOR_TYPE=INTERNAL_ANALYSIS
      - CONNECTOR_NAME=ImportDocumentAnalysis
      - CONNECTOR_VALIDATE_BEFORE_IMPORT=false # Validate any bundle before import
      - CONNECTOR_SCOPE=application/pdf,text/plain,text/html
      - CONNECTOR_AUTO=true # Enable/disable auto-import of file
      - CONNECTOR_ONLY_CONTEXTUAL=false # Only extract data related to an entity (a report, a threat actor, etc.)
      - CONNECTOR_CONFIDENCE_LEVEL=15 # From 0 (Unknown) to 100 (Fully trusted)
      - CONNECTOR_LOG_LEVEL=info
    restart: always
    depends_on:
      - opencti
```

``` {#9ad3 .graf .graf--pre .graf-after--pre}
volumes:
  esdata:
  s3data:
  redisdata:
  amqpdata:
```

3\. Click on Environment Variables. Click Advanced Mode. Copy and paste
the variables into the window:

<figure id="3012" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*EfI3taGQ_sYybzcb.png"
class="graf-image" data-image-id="0*EfI3taGQ_sYybzcb.png"
data-width="788" data-height="416" />
</figure>

``` {#ec8f .graf .graf--pre .graf-after--figure .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ini"}
OPENCTI_ADMIN_EMAIL=admin@opencti.io
OPENCTI_ADMIN_PASSWORD=changeme
OPENCTI_ADMIN_TOKEN=47a3dbe5-5675-4acb-807e-e08d2173d9f7
OPENCTI_BASE_URL=http://localhost:8080
MINIO_ROOT_USER=opencti
MINIO_ROOT_PASSWORD=changeme
RABBITMQ_DEFAULT_USER=opencti
RABBITMQ_DEFAULT_PASS=changeme
CONNECTOR_EXPORT_FILE_STIX_ID=dd817c8b-abae-460a-9ebc-97b1551e70e6
CONNECTOR_EXPORT_FILE_CSV_ID=7ba187fb-fde8-4063-92b5-c3da34060dd7
CONNECTOR_EXPORT_FILE_TXT_ID=ca715d9c-bd64-4351-91db-33a8d728a58b
CONNECTOR_IMPORT_FILE_STIX_ID=72327164-0b35-482b-b5d6-a5a3f76b845f
CONNECTOR_IMPORT_DOCUMENT_ID=c3970f8a-ce4b-4497-a381-20b7256f56f0
CONNECTOR_ANALYSIS_ID=4dffd77c-ec11-4abe-bca7-fd997f79fa36
SMTP_HOSTNAME=localhost
ELASTIC_MEMORY_SIZE=4G
OPENCTI_URL=http://opencti:8080
```

4\. Make sure to change the passwords in the environment variables file
from **changeme** to something more secure**.** Click **Deploy Stack.**
This will take some time as it will need to download additional docker
images. Once complete you should see the stack deployed in the
notification bell.

<figure id="0add" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*n-Oh3XReF3VYQQ1O.png"
class="graf-image" data-image-id="0*n-Oh3XReF3VYQQ1O.png"
data-width="623" data-height="328" />
</figure>

If you see any errors, you can examine the logs of each container and
see if there are any connectivity issues.

### Access & Start Using OpenCTI {#9548 .graf .graf--h3 .graf-after--p name="9548"}

1\. Access the URL
[http://localhost:8080/](http://localhost:8080/){.markup--anchor
.markup--p-anchor data-href="http://localhost:8080/"
rel="noopener ugc nofollow" target="_blank"} using these credentials to
login:

- [Username: admin@opencti.io]{#84fe}
- [Password: **You set this earlier in the environment
  variables**]{#a849}

<figure id="55f3" class="graf graf--figure graf-after--li">
<img
src="https://cdn-images-1.medium.com/max/800/0*sIKLc9CWGuXsRmTL.png"
class="graf-image" data-image-id="0*sIKLc9CWGuXsRmTL.png"
data-width="788" data-height="372" />
</figure>

**At this stage you won't see much happening as we haven't added any
threat feeds just yet.**

2\. Lets add one threat feed from CISA, for known Exploited
Vulnerabilities. This is referred to as "The KEV List".

Go back to the stacks editor. Paste the following code towards the
bottom of the window. Ensure it is pasted above the **Volumes** section.

``` {#82a4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="ruby"}
connector-cisa-known-exploited-vulnerabilities:
    image: opencti/connector-cisa-known-exploited-vulnerabilities:latest
    environment:
      - OPENCTI_URL=${OPENCTI_URL}
      - OPENCTI_TOKEN=${OPENCTI_ADMIN_TOKEN}
      - CONNECTOR_ID=dc788080-859b-49d7-8946-0ec346725204
      - CONNECTOR_TYPE=EXTERNAL_IMPORT
      - "CONNECTOR_NAME=CISA Known Exploited Vulnerabilities"
      - CONNECTOR_SCOPE=cisa
      - CONNECTOR_CONFIDENCE_LEVEL=100 # From 0 (Unknown) to 100 (Fully trusted)
      - CONNECTOR_UPDATE_EXISTING_DATA=false
      - CONNECTOR_RUN_AND_TERMINATE=false
      - CONNECTOR_LOG_LEVEL=info
      - CISA_CATALOG_URL=https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
      - CISA_CREATE_INFRASTRUCTURES=false
      - CISA_TLP=TLP:CLEAR
      - CISA_INTERVAL=2 # In days, must be strictly greater than 1
    restart: always
```

3\. It should look like this. (Note, indentation on Docker Compose is
important, so it may indicate that there is a formatting error. Ensure
it is correctly indented).

<figure id="3c80" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*VPHjUkiJdExkube6.png"
class="graf-image" data-image-id="0*VPHjUkiJdExkube6.png"
data-width="788" data-height="605" />
</figure>

4\. You will need to generate a Connector ID for any new connectors you
add. In my example, the ID is on **Line 191.**

This is required for every subsequent connector; you can generate new
IDs using the following site [UUID
Generator](https://www.uuidgenerator.net/version4){.markup--anchor
.markup--p-anchor data-href="https://www.uuidgenerator.net/version4"
rel="noopener ugc nofollow noopener" target="_blank"}.

5\. Click Update stack; it will download the new container image and
run. To confirm this, navigate to Arsenal, and then Vulnerabilities.

<figure id="b9b8" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*iGPf4G7YeypHC-k_.png"
class="graf-image" data-image-id="0*iGPf4G7YeypHC-k_.png"
data-width="1125" data-height="427" />
</figure>

6\. If you click on one of the vulnerabilities you will see the detail
which has been downloaded.

<figure id="179e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*R8p0K7k1fGetQCD3.png"
class="graf-image" data-image-id="0*R8p0K7k1fGetQCD3.png"
data-width="1125" data-height="542" />
</figure>

7\. For troubleshooting, you can click on **Data,** then **Ingestion.**
Click on **Connectors** to see the newly added **CISA Known Exploited
Vulnerabilities** connector. You can see the Worker statistics pane is
showing there is activity ongoing.

<figure id="8e26" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*n7fT8VKPuZF9aOtp.png"
class="graf-image" data-image-id="0*n7fT8VKPuZF9aOtp.png"
data-width="1125" data-height="449" />
</figure>

### OpenCTI Connectors {#5264 .graf .graf--h3 .graf-after--figure name="5264"}

You can add multiple connectors, to pull threat feeds from external
sources. The full list of available connectors can be found here on the
[OpenCTI
GitHub](https://github.com/OpenCTI-Platform/connectors){.markup--anchor
.markup--p-anchor
data-href="https://github.com/OpenCTI-Platform/connectors"
rel="noopener ugc nofollow noopener" target="_blank"}

Some of these connectors require an API token; whilst some are free to
use, please ensure you read the Terms and conditions for the appropriate
usage. For individuals, some threat intel services such as AlienVault
OTX will allow the consumption of their threat intel for free, but for
organizations, it requires a paid subscription. There is a ReadMe for
each connector, but for reference, the AlienVault OTX link can be found
[here](https://otx.alienvault.com/api){.markup--anchor .markup--p-anchor
data-href="https://otx.alienvault.com/api"
rel="noopener ugc nofollow noopener" target="_blank"}

I've added my configuration to my
[GitHub](https://github.com/andrewblooman/medium/tree/main/opencti_demo){.markup--anchor
.markup--p-anchor
data-href="https://github.com/andrewblooman/medium/tree/main/opencti_demo"
rel="noopener ugc nofollow noopener" target="_blank"}, which you are
free to download and use for yourself, but bear in mind that you will
need to generate the required API tokens.

Some of the Connectors I use for my home lab include:

- [Shodan]{#8b07}
- [AlienVault OTX]{#d39c}
- [Abuse IPDB]{#82cd}
- [URL Haus]{#8e17}

Once you've added multiple connectors, confirm the data is being
ingested by checking the Connectors page again. The data will be queued
and can take up to 24 hours to download and process.

<figure id="509e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*ba-RS0ibX-riPGLY.png"
class="graf-image" data-image-id="0*ba-RS0ibX-riPGLY.png"
data-width="1125" data-height="310" />
</figure>

Once its finished syncing, it should populate the dashboard like below.

<figure id="6e1d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*jejzrF0c7h9obW6f.png"
class="graf-image" data-image-id="0*jejzrF0c7h9obW6f.png"
data-width="1125" data-height="590" />
</figure>

### OpenCTI --- Indicators Of Compromise {#4e03 .graf .graf--h3 .graf-after--figure name="4e03"}

Navigate to the Indicators and Observables pages to see the various IOCs
which have been downloaded. These are searchable in the platform and can
help you find out who may behind an attack.

<figure id="880a" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*LfZL6QG1id-vIzC-.png"
class="graf-image" data-image-id="0*LfZL6QG1id-vIzC-.png"
data-width="1125" data-height="357" />
</figure>

### OpenCTI --- Attack Patterns {#045f .graf .graf--h3 .graf-after--figure name="045f"}

For any aspiring Red Teamers or Pen testers, check out the Attack
Patterns for guidance on how adversaries may attempt to breach different
systems, for example; OS credential dumping in Linux.

<figure id="a69d" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/0*V2OCSoihgD_2BzKI.png"
class="graf-image" data-image-id="0*V2OCSoihgD_2BzKI.png"
data-width="1125" data-height="438" />
</figure>

### Final Thoughts {#e00a .graf .graf--h3 .graf-after--figure name="e00a"}

OpenCTI is a great way to learn more about threat intelligence and is a
fun project which you can learn at home, but you could always deploy
within an Organization. OpenCTI integrates nicely with
[MISP](https://www.misp-project.org/){.markup--anchor .markup--p-anchor
data-href="https://www.misp-project.org/"
rel="noopener ugc nofollow noopener" target="_blank"}, which is another
popular source of open source threat intel.

Proprietary threat intel feeds from organisations such as Recorded
Future and ReliaQuest can be very expensive; so a great way to augment
your systems is to use aggregators like MISP and OpenCTI (Or build your
own!). This can furnish your SIEM and SOAR products with threat intel to
compliment the restricted information which you may pay for.

### Promote and Collaborate on Cybersecurity Insights {#a0c5 .graf .graf--h3 .graf-after--p name="a0c5"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#c940 .graf .graf--h3 .graf-after--p name="c940"}

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
.h-card} on [August 21, 2024](https://medium.com/p/31da658c2041).

[Canonical
link](https://medium.com/@bevijaygupta/how-to-build-a-home-based-cyber-threat-intelligence-system-31da658c2041){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
