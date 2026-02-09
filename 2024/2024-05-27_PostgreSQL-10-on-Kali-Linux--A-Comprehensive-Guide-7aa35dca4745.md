---
title: "PostgreSQL 10 on Kali Linux  A Comprehensive Guide 7aa35dca4745"
platform: Medium
original_file: 2024-05-27_PostgreSQL-10-on-Kali-Linux--A-Comprehensive-Guide-7aa35dca4745.md
---

# PostgreSQL 10 on Kali Linux  A Comprehensive Guide 7aa35dca4745

::: {}
# PostgreSQL 10 on Kali Linux: A Comprehensive Guide {#postgresql-10-on-kali-linux-a-comprehensive-guide .p-name}
:::

::: {.section .p-summary field="subtitle"}
Kali Linux, the renowned operating system for penetration testing and
security auditing, is equipped with a vast array of tools. However...
:::

::::::: {.section .e-content field="body"}
:::::: {#f51d .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### PostgreSQL 10 on Kali Linux: A Comprehensive Guide {#7e37 .graf .graf--h3 .graf--leading .graf--title name="7e37"}

<figure id="87c1" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*PvKRhjlDBB538EDKVEy2xA.jpeg"
class="graf-image" data-image-id="1*PvKRhjlDBB538EDKVEy2xA.jpeg"
data-width="685" data-height="376" />
</figure>

Kali Linux, the renowned operating system for penetration testing and
security auditing, is equipped with a vast array of tools. However, for
those looking to leverage robust database solutions within this powerful
platform, PostgreSQL 10 offers an optimal choice. PostgreSQL, often
referred to as Postgres, is a powerful, open-source relational database
system that emphasizes extensibility and SQL compliance. This blog will
delve into the installation, configuration, and usage of PostgreSQL 10
on Kali Linux, covering essential aspects to provide a comprehensive
understanding.

### Understanding PostgreSQL 10 {#c60a .graf .graf--h3 .graf-after--p name="c60a"}

### Overview of PostgreSQL {#163d .graf .graf--h3 .graf-after--h3 name="163d"}

PostgreSQL is an advanced, enterprise-class open-source relational
database management system (RDBMS). Known for its performance,
reliability, and feature set, PostgreSQL supports a wide variety of
applications, from simple web applications to large-scale data
warehousing and analytics. Key features of PostgreSQL include:

- [ACID Compliance: Ensures reliable transactions and data
  integrity.]{#ca38}
- [Advanced Data Types: Supports JSON, XML, and array data
  types.]{#4d50}
- [Extensibility: Users can define custom data types, functions, and
  operators.]{#382c}
- [Concurrency: Implements Multi-Version Concurrency Control (MVCC) for
  handling multiple simultaneous transactions.]{#9877}

### PostgreSQL 10 Enhancements {#fec8 .graf .graf--h3 .graf-after--li name="fec8"}

PostgreSQL 10 introduced several significant features and enhancements
that improve performance, scalability, and usability:

- [Logical Replication: More flexible replication for specific tables or
  entire databases.]{#c3cd}
- [Declarative Table Partitioning: Simplifies table partitioning and
  management.]{#fd2c}
- [Quorum Commit for Synchronous Replication: Enhances data durability
  and availability.]{#b4a0}
- [Improved Parallel Query: Enhances performance for large-scale
  queries.]{#9d62}
- [Scram-SHA-256 Authentication: Offers stronger password hashing
  mechanisms for security.]{#a0b3}

### Installing PostgreSQL 10 on Kali Linux {#b73f .graf .graf--h3 .graf-after--li name="b73f"}

### Prerequisites {#991c .graf .graf--h3 .graf-after--h3 name="991c"}

Before installing PostgreSQL, ensure your system is updated and has the
necessary tools installed. Open a terminal and execute the following
commands:

``` {#65e5 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
bash
```

``` {#daa2 .graf .graf--pre .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
sudo apt update
sudo apt upgrade -y
```

### Installation Process {#3043 .graf .graf--h3 .graf-after--pre name="3043"}

1.  [Add PostgreSQL APT Repository: PostgreSQL provides an APT
    repository to ensure you can install and update PostgreSQL packages
    easily.]{#c0f8}

- [bash]{#3c90}
- [`echo "deb http://apt.postgresql.org/pub/repos/apt/ kali-rolling-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list`{.markup--code
  .markup--li-code}]{#0e56}

1.  [Import the Repository Signing Key:]{#bcce}

- [bash]{#31c6}
- [`wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -`{.markup--code
  .markup--li-code}]{#b4d2}

1.  [Update the Package List:]{#2de6}

- [bash]{#2c03}
- [`sudo apt update`{.markup--code .markup--li-code}]{#3e4d}

1.  [Install PostgreSQL 10:]{#12b5}

- [bash]{#43fa}
- [`sudo apt install postgresql-10 -y`{.markup--code
  .markup--li-code}]{#e588}

### Verifying the Installation {#5d48 .graf .graf--h3 .graf-after--li name="5d48"}

Once the installation is complete, verify that PostgreSQL is installed
and running:

``` {#4d4a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
bash
```

``` {#f877 .graf .graf--pre .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
sudo systemctl status postgresql
```

You should see an active (running) status indicating that the PostgreSQL
service is up and running.

### Configuring PostgreSQL 10 {#e3d6 .graf .graf--h3 .graf-after--p name="e3d6"}

### Basic Configuration {#8992 .graf .graf--h3 .graf-after--h3 name="8992"}

PostgreSQL's configuration files are located in the
`/etc/postgresql/10/main/`{.markup--code .markup--p-code} directory. The
primary files include:

- [postgresql.conf: Main configuration file for PostgreSQL
  settings.]{#69f0}
- [pg_hba.conf: Configures client authentication.]{#fb67}

1.  [Editing postgresql.conf:]{#913f}
2.  [Open the configuration file:]{#03dd}

- [bash]{#5eaf}
- [`sudo nano /etc/postgresql/10/main/postgresql.conf`{.markup--code
  .markup--li-code}]{#ab4c}

1.  [Common settings to adjust include `listen_addresses`{.markup--code
    .markup--li-code} and `port`{.markup--code
    .markup--li-code}:]{#8f0d}

- [conf]{#19f5}
- [`listen_addresses = '*' port = 5432`{.markup--code
  .markup--li-code}]{#1864}

1.  [These settings ensure PostgreSQL listens on all network interfaces
    on the default port 5432.]{#716f}
2.  [Editing pg_hba.conf:]{#632c}
3.  [Open the client authentication configuration file:]{#feb9}

- [bash]{#d692}
- [`sudo nano /etc/postgresql/10/main/pg_hba.conf`{.markup--code
  .markup--li-code}]{#5a68}

1.  [Add or modify the following lines to allow local connections and
    connections from specific IP ranges:]{#17b9}

- [conf]{#3940}
- [`# Allow local connections local all all peer # Allow connections from specific IP range host all all 192.168.1.0/24 md5`{.markup--code
  .markup--li-code}]{#d28f}

### Starting and Enabling PostgreSQL {#4c37 .graf .graf--h3 .graf-after--li name="4c37"}

Ensure that PostgreSQL starts automatically on boot:

``` {#a5a0 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
bash
```

``` {#332e .graf .graf--pre .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
sudo systemctl enable postgresql
```

Restart the PostgreSQL service to apply the changes:

``` {#c47b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
bash
```

``` {#cded .graf .graf--pre .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
sudo systemctl restart postgresql
```

### Using PostgreSQL 10 {#f0b9 .graf .graf--h3 .graf-after--pre name="f0b9"}

### Accessing PostgreSQL {#3d8e .graf .graf--h3 .graf-after--h3 name="3d8e"}

PostgreSQL includes a command-line tool, `psql`{.markup--code
.markup--p-code}, which allows you to interact with the database server.

1.  [Switch to the PostgreSQL User:]{#54c9}

- [bash]{#0e95}
- [`sudo -i -u postgres`{.markup--code .markup--li-code}]{#6c0c}

1.  [Access the PostgreSQL Shell:]{#62f7}

- [bash]{#55f0}
- [`psql`{.markup--code .markup--li-code}]{#3c9e}

1.  [You should see a prompt like this:]{#0abf}

- [plaintext]{#727f}
- [`postgres=#`{.markup--code .markup--li-code}]{#53a6}

### Creating a Database and User {#73dc .graf .graf--h3 .graf-after--li name="73dc"}

1.  [Create a New Database:]{#84e1}

- [sql]{#13d9}
- [`CREATE DATABASE mydatabase;`{.markup--code .markup--li-code}]{#31f4}

1.  [Create a New User:]{#0fc4}

- [sql]{#dc89}
- [`CREATE USER myuser WITH PASSWORD 'mypassword';`{.markup--code
  .markup--li-code}]{#3685}

1.  [Grant Privileges to the User:]{#010c}

- [sql]{#2746}
- [`GRANT ALL PRIVILEGES ON DATABASE mydatabase TO myuser;`{.markup--code
  .markup--li-code}]{#c049}

### Basic SQL Commands {#39d5 .graf .graf--h3 .graf-after--li name="39d5"}

Here are some basic SQL commands to help you get started with
PostgreSQL:

1.  [List Databases:]{#d633}

- [sql]{#e383}
- [`\l`{.markup--code .markup--li-code}]{#f0de}

1.  [Connect to a Database:]{#eb50}

- [sql]{#9cbc}
- [`\c mydatabase`{.markup--code .markup--li-code}]{#51c0}

1.  [Create a Table:]{#5437}

- [sql]{#c936}
- [`CREATE TABLE employees ( id SERIAL PRIMARY KEY, name VARCHAR(100), position VARCHAR(100), salary NUMERIC );`{.markup--code
  .markup--li-code}]{#725b}

1.  [Insert Data into a Table:]{#833f}

- [sql]{#cfe4}
- [`INSERT INTO employees (name, position, salary) VALUES ('John Doe', 'Software Engineer', 75000);`{.markup--code
  .markup--li-code}]{#acce}

1.  [Query Data:]{#770b}

- [sql]{#252e}
- [`SELECT * FROM employees;`{.markup--code .markup--li-code}]{#79b2}

1.  [Update Data:]{#8928}

- [sql]{#0544}
- [`UPDATE employees SET salary = 80000 WHERE name = 'John Doe';`{.markup--code
  .markup--li-code}]{#ae92}

1.  [Delete Data:]{#9b02}

- [sql]{#476f}
- [`DELETE FROM employees WHERE name = 'John Doe';`{.markup--code
  .markup--li-code}]{#e700}

### Advanced PostgreSQL Features {#c324 .graf .graf--h3 .graf-after--li name="c324"}

### Logical Replication {#08a4 .graf .graf--h3 .graf-after--h3 name="08a4"}

Logical replication allows fine-grained replication control by enabling
replication of individual tables or entire databases. To set up logical
replication:

1.  [Configure the Publisher:]{#706a}
2.  [Edit `postgresql.conf`{.markup--code .markup--li-code} on the
    publisher node:]{#2e36}

- [conf]{#0a45}
- [`wal_level = logical max_replication_slots = 4 max_wal_senders = 4`{.markup--code
  .markup--li-code}]{#84a4}

1.  [Restart the PostgreSQL service:]{#c4ce}

- [bash]{#8451}
- [`sudo systemctl restart postgresql`{.markup--code
  .markup--li-code}]{#7d25}

1.  [Create a replication slot and a publication:]{#2d56}

- [sql]{#3650}
- [`CREATE PUBLICATION mypublication FOR TABLE employees;`{.markup--code
  .markup--li-code}]{#675a}

1.  [Configure the Subscriber:]{#84da}
2.  [On the subscriber node, create a subscription:]{#6afd}

- [sql]{#5080}
- [`CREATE SUBSCRIPTION mysubscription CONNECTION 'host=publisher_ip dbname=mydatabase user=myuser password=mypassword' PUBLICATION mypublication;`{.markup--code
  .markup--li-code}]{#2636}

### Declarative Table Partitioning {#176b .graf .graf--h3 .graf-after--li name="176b"}

PostgreSQL 10 introduced declarative table partitioning, simplifying the
management of large tables by dividing them into smaller, more
manageable pieces.

1.  [Create a Partitioned Table:]{#7ce2}

- [sql]{#3c08}
- [`CREATE TABLE sales ( id SERIAL PRIMARY KEY, sale_date DATE, amount NUMERIC ) PARTITION BY RANGE (sale_date);`{.markup--code
  .markup--li-code}]{#cd37}

1.  [Create Partitions:]{#5a34}

- [sql]{#ba2d}
- [`CREATE TABLE sales_2021 PARTITION OF sales FOR VALUES FROM ('2021-01-01') TO ('2022-01-01'); CREATE TABLE sales_2022 PARTITION OF sales FOR VALUES FROM ('2022-01-01') TO ('2023-01-01');`{.markup--code
  .markup--li-code}]{#959f}

### Scram-SHA-256 Authentication {#349b .graf .graf--h3 .graf-after--li name="349b"}

To enhance security, PostgreSQL 10 supports Scram-SHA-256
authentication. Configure it by editing `pg_hba.conf`{.markup--code
.markup--p-code}:

``` {#2ad7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
conf
```

``` {#46d3 .graf .graf--pre .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
# Use Scram-SHA-256 authentication
host    all             all             0.0.0.0/0               scram-sha-256
```

Change the user's password to use the new authentication method:

``` {#112b .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
sql
```

``` {#eaf6 .graf .graf--pre .graf-after--pre .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
ALTER USER myuser WITH PASSWORD 'newpassword';
```

### Integrating PostgreSQL with Other Tools {#f79c .graf .graf--h3 .graf-after--pre name="f79c"}

### Using pgAdmin {#e4f7 .graf .graf--h3 .graf-after--h3 name="e4f7"}

pgAdmin is a popular graphical tool for managing PostgreSQL databases.
To install and use pgAdmin on Kali Linux:

1.  [Install pgAdmin:]{#23e2}

- [bash]{#c9f1}
- [`sudo apt install pgadmin4`{.markup--code .markup--li-code}]{#2000}

1.  [Configure pgAdmin:]{#92b5}
2.  [Launch pgAdmin and configure the connection to your PostgreSQL
    server using the credentials set up earlier.]{#d5f6}

### Using Python with psycopg2 {#e2c0 .graf .graf--h3 .graf-after--li name="e2c0"}

Python's `psycopg2`{.markup--code .markup--p-code} library is a
PostgreSQL adapter that allows Python applications to interact with
PostgreSQL databases.

1.  [Install psycopg2:]{#71bd}

- [bash]{#466e}
- [`sudo apt install python3-psycopg2`{.markup--code
  .markup--li-code}]{#7e1a}

1.  [Sample Python Script:]{#efed}

- [python]{#ab67}
- [`import psycopg2 # Connect to PostgreSQL database conn = psycopg2.connect( dbname="mydatabase", user="myuser", password="mypassword", host="localhost" ) # Create a cursor object cur = conn.cursor() # Execute a query cur.execute("SELECT * FROM employees") # Fetch and display results rows = cur.fetchall() for row in rows: print(row) # Close the cursor and connection cur.close() conn.close()`{.markup--code
  .markup--li-code}]{#b5b3}

### Best Practices for PostgreSQL on Kali Linux {#3b13 .graf .graf--h3 .graf-after--li name="3b13"}

1.  [**Regular Backups:** Use `pg_dump`{.markup--code .markup--li-code}
    or `pg_basebackup`{.markup--code .markup--li-code} to perform
    regular backups of your databases to prevent data loss.]{#961c}
2.  [**Monitoring:** Implement monitoring tools like
    `pg_stat_statements`{.markup--code .markup--li-code} and
    `pgAdmin`{.markup--code .markup--li-code} to track database
    performance and identify bottlenecks.]{#6792}
3.  [**Security:** Regularly update PostgreSQL and use strong passwords
    and encryption to secure your databases.]{#6bcd}
4.  [**Maintenance:** Perform routine maintenance tasks such as
    vacuuming and analyzing tables to optimize performance.]{#828e}
5.  [**Documentation:** Keep thorough documentation of your database
    schemas, configurations, and procedures to ensure smooth operations
    and facilitate troubleshooting.]{#42e0}

### Conclusion {#1ed0 .graf .graf--h3 .graf-after--li name="1ed0"}

PostgreSQL 10 on Kali Linux offers a powerful and versatile platform for
database management, combining the strengths of a robust operating
system with an advanced RDBMS. By following the steps outlined in this
guide, you can effectively install, configure, and utilize PostgreSQL 10
to manage your data securely and efficiently.

Whether you're leveraging PostgreSQL for web applications, data
analysis, or security testing, its extensive feature set and scalability
make it a valuable asset. Embrace the capabilities of PostgreSQL 10 on
Kali Linux, and harness its power to meet your data management needs.

### About the Author: {#8829 .graf .graf--h3 .graf-after--p name="8829"}

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

If you've found my content valuable and wish to support me directly, you
can also consider tipping me on my [PayPal
account](https://www.paypal.me/bevijaygupta){.markup--anchor
.markup--p-anchor data-href="https://www.paypal.me/bevijaygupta"
rel="noopener ugc nofollow noopener" target="_blank"}. Your
contributions go a long way in helping me sustain my blogging efforts
and continue creating content that resonates with you. Every tip is
deeply appreciated and fuels my passion for writing. Thank you for
considering supporting me on this journey through your generosity and
encouragement.
:::
::::
::::::
:::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [May 27, 2024](https://medium.com/p/7aa35dca4745).

[Canonical
link](https://medium.com/@bevijaygupta/postgresql-10-on-kali-linux-a-comprehensive-guide-7aa35dca4745){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
