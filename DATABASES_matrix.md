# DATABASES INFORMATION

## Relational

### What is a relational database?

According to [Oracle]( https://www.oracle.com/database/what-is-a-relational-database/), a Relational Database stores data and provides its access to points related to one another. On the other hand, [Amazon]( https://aws.amazon.com/es/relational-database/) defines it a recompilation of data with a predefined relationship between them. Whereas [IBM]( https://www.ibm.com/cloud/learn/relational-databases) explains it too, as a way to organize data into tables that can be related according to the data in common. Overall, a relational database is used to store data in tables to have a better understanding of the information they contain; therefore, it uses a structure where the access to data in relation is allowed. 

A relational database management system (RDBMS) is a computer program that employs the relational data model, which was designed to solve multiple arbitrary data structures that a single database system would cause.

- Table – set of values.

- Record (row) – a piece of data

- Field (column) – an item in a record.

To interact with a RDBMS is commonly used the Structured Query Language (SQL) which allows both to input and to retrieve data with a straightforward structure, reason why it become a standard language for database queries.

### Advantages

Relational Databases consist on a schema based on ACID properties (atomicity, consistency, isolation and durability), which provides warranty of validation even if errors, power failures, etc. are presented. This characteristic, therefore, operate altogether to give transactions throughout a well-documented and widely supported SQL syntax.

The model of a relational database is structured, helps or facilitates to do complex queries, including sub-queries and joins. The latter gives a meaningful benefit for the information due to the ease to understand the relationships between data and tables.

Furthermore, the SQL approach, allows you the opportunity to make your database flexible. Plus, the elimination of data redundancy is a characteristic of relational databases that pull up their normalization, which avoid such redundancy in the data.

### Disadvantages

A common limitation of relational databases is their null scalability, specifically horizontal scaling or scaling out. That shows difficulties when adding a new resource instead of increasing the capacity of the current resource. And the main reason why it is a complicated procedure to do, is because of the consistency in which the design of a relational model is based on.

Finally, the limitation that the data is currently demanding, has to do with the amount of information the digital sector is storing. A relational database was designed to manage structured data, which means that the data is organized in a predetermined way that allows the information to be easily sortable and searchable. Thus, developers start to look for other alternatives, giving birth, as a consequence, to NoSQL databases.



## Time-series

### What is a time series database?

A TSBD is a database that has been optimized for time-stamped or time series of data. To simply put it, they are measurements or events that are tracked, monitored, down sampled, and aggregated over time, examples of this could be server metrics, application performance monitoring, network data, sensor data, events, clicks, trades in a market, and many other types of analytics data.

Time series may be called profiles, curves traces or trends. Early TSBD were designed to measure values from sensory equipment.

![img](https://raw.githubusercontent.com/oswaldochan/5_MassiveData/master/images_random/databases_matrix_img1.png)

Time series databases are the fastest growing segment of the database industry over the past year, meaning that there is a wider community support like python. 

Scaling: Time series can be based on relational or no SQL, it handles scaled by introducing efficiencies that are only possible when you use time. Resulting in performance improvement, higher ingest rates, faster queries at scale and better data compression.

It has smooth, continuous, highly concurrent and high trough put data writing. There are more writes than reads, 95% of the operation on time series are writes. Recent data is generated in real time, no existing data is updated except on manual revision.

## Ledger Database

### First of all, what is a ledger?

**Ledgers** are typically used to record a history of economic and financial activity in an organization. Many organizations build applications with ledger-like functionality because they want to maintain an accurate history of their applications' data, for example, tracking the history of credits and debits in banking transactions, verifying the data lineage of an insurance claim, or tracing movement of an item in a supply chain network. *Ledger applications are often implemented using custom audit tables or audit trails created in relational databases*. However, building audit functionality with relational databases is time-consuming and prone to human error. It requires custom development, and since relational databases are not inherently immutable, any unintended changes to the data are hard to track and verify. Alternatively, *blockchain frameworks, such as Hyperledger Fabric and Ethereum, can also be used as a ledger*. However, this adds complexity as you need to set-up an entire blockchain network with multiple nodes, manage its infrastructure, and require the nodes to validate each transaction before it can be added to the ledger.

### What is _Quantum Ledger Database (QLDB)_?

> Amazon QLDB is a new class of database that eliminates the need to engage in the complex development effort of building your own ledger-like applications. With QLDB, your data’s change history is immutable – it cannot be altered or deleted – and using cryptography, you can easily verify that there have been no unintended modifications to your application’s data

**AWS Quantum Ledger Database (QLDB) is the first, and currently only, commercially available ledger database.**

### What are its characteristics?

> - **Immutable and Transparent**:  Amazon QLDB uses a journal that tracks each application data change and maintains a complete and sequenced history of changes over time. Data on the journal cannot be deleted or modified.
> - **Cryptographically Verifiable**:  QLDB uses a cryptographic hash function (SHA-256) to generate a secure output file of your data’s change history, known as a digest. The digest acts as a proof of your data’s change history, allowing you to look back and validate the integrity of your data changes.
> - **Performant and Highly Scalable**: Amazon QLDB is highly scalable and can execute 2 – 3X as many transactions than ledgers in common blockchain frameworks. QLDB has a centralized design, allowing its transactions to execute without the need for multi-party consensus.
> - **Serverless**:  You create a ledger, define your tables, and QLDB automatically scales to support the demands of your application
> - **Easy to Use**: QLDB supports PartiQL - a new, open source, SQL-compatible query language designed to easily work with all data types and structures.
> - **Highly Available**: Amazon QLDB is designed for high availability, replicating multiple copies of data within an Availability Zone (AZ) as well as across 3 AZs in an AWS region, without any additional cost or setup
> - **Streaming Capability**: Amazon QLDB can stream data directly to Amazon Kinesis Data Streams, which allows you to react quickly to new events and to easily develop event-driven workflows and perform real-time and historical data analysis.

![99Product-Page-Diagram_AWS-Quantum](https://raw.githubusercontent.com/oswaldochan/5_MassiveData/master/images_random/databases_matrix_img2.png)



# MATRIX

|                                                              | **Relational Database**                                      | **Time-series Database**                                     | **Ledger Database**                                          |                                                              |                                                              |                                                         |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------- | ------------------------------------------------------------ |
| **MariaDB**                                                  | **Amazon Aurora**                                            | **IBM Db2 on Cloud**                                         | **InfluxDB**                                                 |                                                              | **Prometheus**                                               | **Blockchain**                                          | **QLDB**                                                     |
| **Applications**                                             | Same applications as  MySQL                                  | - Enterprise  - SaaS  - Web  - Mobile Gaming                 | Designed to keep business running 24x7                       | Realtime analytics                                           | Open-source TimeSeries DBMS and monitoring system            | Asset management  Insurance  Payments  Smart appliances | Finance  Manufacturing  Insurance  HR                        |
| **Capabilities**                                             | Drop-in replacement.  Free and open-source software          | +5x faster than  MySQL.  High performance and Scalability.  Built for the cloud (AWS).  Migration support. | Artificial Intelligence.  Independent scaling of CPU.  Rolling Security Updates. | high throughput ingest, compression and real-time  querying. | a multi-dimensional data model with time series data  identified by metric name and key/value pairs. | It is extremely secure, anonymous, decentralized        | Performant, faster than blockchain, Amazon ecosystem    Serverless |
| **Limitations**                                              | Size and space limits of underlying storage and  operating system are reached long before MariaDB's internal limits are  reached | Not available for old MySQL versions.                        | Specific restrictions in column-organized tables  according to the database configurations and environment. | Not set up and go.  Little to no documentation.              | Numeric only                                                 | Uses excessive energy, slow process and harder to scale | It is Amazon proprietary, no open source.                    |
| **Atomicity**  **Consistency**  **Isolation**  **Durability (ACID)** | YES                                                          | YES  Recovers from  physical storage failures (less than 30sec) | YES                                                          | yes                                                          | No                                                           | -                                                       | -                                                            |
| **Data integrity**                                           | Support by  System-versioned tables to allow data analysis.  | Almost instantaneous crash recovery.                         | Check constraints and referential constraints on  data       | No foreign  keys, data integrity checks are not needed       | No checks.                                                   | -                                                       | -                                                            |
| **Transactions**                                             | YES                                                          | YES                                                          | YES                                                          | yes                                                          | yes                                                          | yes                                                     | yes                                                          |
| **Stored procedures**                                        | Standard storage engines and more with MariaDB  Source and Binary packages. | Storage System that auto-scales up to 64TB per  database instance. | Allows you to monitor the connection and storage  usage.     | Writes data  from API to disk.                               | local storage subsystem, organizes data in chunks of  constant size (1024 bytes payload) | Decentralized                                           | Centralized                                                  |
| **Backup**                                                   | YES                                                          | Managed by Amazon RDS which automates time consuming  tasks like backups. | Online and offline backups.                                  | Offline and  online backups.                                 | local                                                        | yes                                                     | yes                                                          |



# REFERENCES

https://www.oracle.com/database/what-is-a-relational-database/

https://aws.amazon.com/es/relational-database/

https://www.ibm.com/cloud/learn/relational-databases

https://dev.to/lmolivera/everything-you-need-to-know-about-relational-databases-3ejl

https://www.codecademy.com/articles/what-is-rdbms-sql

https://www.digitalocean.com/community/tutorials/a-comparison-of-nosql-database-management-systems-and-models

https://www.accionlabs.com/blog/nosqldatabase?rq=matrix

https://aws.amazon.com/rds/aurora/

https://aws.amazon.com/qldb/?nc1=h_ls

https://github.com/MariaDB/server

https://mariadb.com/kb/en/mariadb-vs-mysql-features/

https://www.ibm.com/cloud/db2-on-cloud/

https://blockgeeks.com/guides/blockchain-applications/

https://ivan.mw/2019-11-24/what-is-a-ledger-database

https://www.influxdata.com/time-series-database/

https://blog.timescale.com/blog/what-the-heck-is-time-series-data-and-why-do-i-need-a-time-series-database-dcf3b1b18563/

https://technology.amis.nl/2019/01/31/influxdb-for-time-series-data/

https://prometheus.io/docs/prometheus/latest/storage/