# Designing Data-Intensive Applications

Short questionarie based on the book by Martin Kleppmann.

## Chapter 1. Reliable, Scalable, and Maintainable Applications

### 1. Differences between data-intensive and compute-intensive.
Compute-intensive demands computation work where most of their execution time is devoted to computational requirements
whereas data-intensive is a class of applications that use data paralell aproach to process large volumes of data (with size of tera or petabytes).

### 2. What are the caracteristics that make a system reliable? Mention an example of a not reliable system.
The reliability of a systems comes when it performs its intended functionality satisfactorily even under specific environmental and operating conditions. An example of the lack of system reliability lays in the failure either human, software or hardware made. For instance, a human mistake in the software that can create a series of cascading failures in a important component within the system.

### 3. Why rather to measure the performance of the system with percentiles than with mean?
Percentiles can more exactly measure the reachability in certain application. If you use the 99th percentile (p99) you can get the amount of users that reach that levels. In that way, you can fix anything needed. If you only use the mean, that gives you the average in your users and does not really tell you much information to fix anything.

### 4. What does make a system elastic? Give an example.
If a system is elastic, it means that it is able to add computing resources when detecting a load increase; for short, a system that is able to adapt to load changes. A clear example of it might be seen in cloud computing (AWS, Azure, Google Cloud), where you can choose what to pay according with your needs.

### 5. Therefore... What is the difference between scalability and elasticity?
Scalability gives you the ability to increase or decrease your resources (manually), and elasticity lets those operations happen automatically according to configured rules.

### 6. Does a one-size-fits-all scalable architecture exist? Why?
There is no generic architecture due to the problems with the volume of reads, writes and store, as same as the complexity of the data, the response time requirements, the access patterns, and more. Overall, the architecture of systems that operate at large scale is usually specific to the application to perform.

### 7. If you are working on the coding part of the development of a system for certain company, and you are part of the first version of the prototype, which maintainability design principle(s) you have to fulfill to avoid difficulties that you collegues might face?
Operability and simplicity. The former, to make it easy for operations teams to keep the system running smoothly, and the latter to make it easy for new engineers to understand the system, by removing as much complexity as possible from the system, avoiding a cascade of unnecessary failures.

## Chapter 2. Data Models and Query Languages

### 1. What was the original purpose of Relational Databases?
Their roots lie in dusiness data processing in the 1960s and '70s, mainly used for transaction processing and batch processing.

### 2. Is NoSQL a technology for databases?
No. It refers more to a "semantic field" that hold those technologies that are not stored as relational databases way.

### 3. What is a impedance mismatch related with databases?
This term was introduces by electronics. Every electric circuit has a certain impedance on its I/O (resistance to alternating current). Therefore, an impedande mismatch can lead to signal reflection and other troubles.

For databases, then, it refers to an specific state commonly use to critic SQL data model: if data is stored in relational tables, an akward translation layer is requires between the objects in the application code and the database model.

### 4. What is database normalization?
It is the process of structure a relational database in a serio of normal forms. The latter with the purpose od reducing data redundancy and to improve its data integrity.

### 5. What is database denormalization?
Optimization technique which add redundant data to one or more tables. It is important to highight that is not the opposite of normalization. I'ts just a technique that goes after normalization.

### 6. What id CODASYL?
Conference on Data Systems Languages (CODASYL) is a comitee in charged of standarize and implement the network model by several different database vendors. It is also known as the CODASYL model, which, basically, is a generalization of the hierarchical model.

### 7. How is structured the hierarchical model?
It follows a tree structure where every record has exactly one parent. What difference the hierarchical model from the network model is that a record in the latter can have multiple parents.

### 8. How a CODASYL query works?
By moving a cursor through the database by iterating over lists of records and following access paths. If a record had multiple parents, the application code had to keep track of all the various relationships. It is compared to navigation around an n-dimensional data space.

### 9. Which are the two types of query language?
When the relational model was introduced, it included a new way of querying data:
* declarative query language in SQL

In a declarative query language you just specify the pattern of the data you want, but not how to achieve that goal.

* IBM's Information Management System (IMS) and CODASYL queried the database
using imperative code.

Weheras an imperative language tells the computer to perform certain operations in a certain order.

### 10. Mention some examples of data that can be modeled as a graph (Graph-Like Data Models).
When dealing with a many-to-many relationship, relational model cannot handle complexity, so it become more natural to start modeling the data as a graph. A graph consists of two kinds of objects: **_vertices_** (nodes/entities) and **_edges_** (relationship/arcs).
* Social graphs

|Vertices|  Edges      |
|--------|-------------|
| People |Who knows who|

* Web Graph

|Vertices  |  Edges      |
|----------|-------------|
|Web Pages |HTML links   |

* Road or rail networks

|Vertices  |  Edges               |
|----------|----------------------|
| Junctions|Roads or railway lines|

## Chapter 3. Storage and Retrieval

### 1. What are indexes? Mention an advantage and a disadvantage of indexes.
An index in an _additional_ structure that is derived form the primary data to identify your information. To mention and advantage and a disadvantage, well-chosen indexes speed up read queries, but every index slows down writes. 

### 2. What is a hash index?
A hash index consists of a collection of buckets organized in an array. A hash function maps index keys to correspoding buckets in the hash index.

### 3. Mention some of the reasons for append-only design to be considered a good design idea.
* Merging old segments avoids the problem of data files getting fragmented over time
* Concurrency and crash recovery are much simpler if fragment files are appen-only or immutable. 
* Appending and segment merging are sequential write  operations, which are gererally faster than random writes, especially on magnetic spinning-disk hard drives.

### 4. What is an SSTtable?
It is file fulfilled with key-value string pairs. This file must be sorted by key in order to be considered an SSTable (Sorted String Table).

### 5. Mention some advantages of the SStables over log segments with hash indexes
* Merging segments is simple and efficient, even if the files are bigger than the available memory.
* In order to find a particular key in the file, you no longer need to keep an index of all the keys in memory. 
* Since read requests need to scan over several key-valye pairs in the requested range anyway, it is possible to group those records into a block and compress it before writting in to disk. Each entry of the sparse in-memory index then points at the start of a compressed block. Besides saving disk space, compression also reduces the I/O bandwidth use. 

### 6. What is a B-tree?
A B-tree is a self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions, and deletions in logarithmic time.

### 7. What does "transaction processing" means?
Transaction processing just means allowing clients to make low-latency read and writes as opposed to _batch processing_ jobs, which only run periodically.

### 8. What is a data warehouse?
A data warehouse is a seperate dabatase that analysts can query to their hearts' content, without affecting Online Transaction Processing (OLTP). The data warehouse contains a read-only copy of the data in all the various OLTP systems in the company. 

### 9. What's the philosophy behind _column-oriended storage_?
The idea behind column-oriented storage is simple: Don't store all the values from one row together, but store all the values from each column together instead.

## Chapter 4. Encoding and Evolution

### 1. Let's say I made a change in my schema and, eventually, in my code; nevertheless, the user hasn't upgrade in his decive the newer version of my code so both version of it are coexisting in the same system. What characteristics does my code need to have for a good performance? 
* Backward Compatibility: Newer code can read data that was written by older code
* Forward Compatibility: Older code can read data that was written by newer code

### 2. Mention two of the most typical representations for programs to work with data
* Data structures: In memory, data is kept in objects, structs, lists, arrays, hast tables, trees, and so on. These data structures are optimized for efficient access and manipulations by the CPU. This is usually done using pointers. 
* Files/sequence of bytes: When you want to write data to a file or send it over the network, you have to encode it as some kind of self-contained sequence of bytes. Since a pointer wouldn't make sense to any other process, this sequence-of-bytes representation looks quite different from the data structures that are normally used in memory.

### 3. In a realistic and general scenario, is it advisable to use your language's built-in encoding for your data? why? 
No. It's generally a bad idea to use it for anything other than very transient purposes.

Even though they usually have plenty of advantages, they also have deep disadvantages like the fact that the encoding is often tied to a particular programming language, and reading the data in another language is very difficult. Another disadvantage is the fact that versioning data is an afterthought in these libraries: as they are intended for a quick and easy encoding of data, they often neglect the inconvenient problems of forward and backward compatibility

### 4. If I want to remove or add a field in my schema, what do I need to take into consderation related to the compatibility of my system?
Removing a field is just like adding a field, with backward and forward compatibility concerns reversed. That means you can only remove a field that is optional, and you can never use the same tag number again. 

### 5. Imagine that I created a system a couple of years ago for a samll project; nonetheless, it grew so fast that one of my field that is currently a 32-bit variable datatype can no longer hold the information that needs to be stored in that field. How can I solve this issue and what problems could I face by solving it? 
One solution can be changing the datatype of the field from a 32-bit integer into a 64-bit integer. New code can easily read data written by old code, because the parser can fill in any missing bits with zeros. However, if old code reads data written by new code, the old code is still using a 32-bit variable to hold the value. If the decoded 64-bit value won't fit in the 32 bits, it will be truncated. 

### 6. What are the most used standardized data encodings and what is the developers' perspective on them?
JSON, XML and CSV are the most common ones; they are widely known, widely supported, and almost as widely disliked. XML is often criticized for being too verbose and unnecessarily complicated. JSON's popularity is mainly due to its built-in support in web browsers and simplicity relative to XML. CSV is another popular language-independent format, albeit less powerful. 

### 7. What is the biggest problem of CSV related to its schema?
CSV does not have any schema, so it is up to the application to define the meaning of each row and column. If an application change adds a new row or column, you have to handle that change manually. 

### 8. What is Apache Avro? Why kind of schemas does it have?  
Apache Avro is another binary encoding format that is interestingly different from Protocol Buffers and Apache Thrift. It was started in 2009 as a result of Thrift not being a good fit for Hadoop's use cases.

It has two schema languages: One intended for human editing, and one that is more easily machine-readable. 

### 9. Speaking about Avro, what is it known as "the writer's schema"? What about "the reader's schema"?
When an application wants to encode some data, it encodes the data using whatever version of the schema it knows about. That's the "writer's schema".

When an application wants to decode some data, it is expecting the data to be in some schema, which is known as "the reader's schema". That is the schema that application code is relying on.

### 10. How does compatibility work on Avro?
With Avro, forward compatibility means that you can have a new version of the schema as writer and an old version of the schema as reader. Conversely, backward compatibility means that you can have a new version of the schema as reader and an old version as writer. 

### 11. Let's say that I'm working with Avro and I have a data field called "Name". For me, that field is optional, so it is completely fine if it has values or not... How can I tell Avro that it can have null values? is that procedure the same for every programming language? 
In some programming languages "null" is an accetable default variable for a field, this is: If you've declared a field as "string", if you don't write a value in that field it will automatically be read as "null".

This is not the case for Avro. You must specify all of the valid datatypes for a field or otherwise will crash. In this example you must declare that field to be a string AND a null one.

## Chapter 5. Replication

### 1. Replication is the action of keeping a cop of the same data on multiple connected machines in a network. But why is it highly recomended?
Replication gives the opportunity to keep data geographically close to the users, getting as a result the reduction of latency. Another advantage is that you give the system the capacity to continue working even if some of its parts have failed, hence, increasing the availabity. And finally, to scale out the number of machines that can serve read queries, therefore, increasing read throughput.

### 2. What is the problem that comes with replication?
Despite being a simple goal, it turns out to be a tricky problem, because it requires carefully tinking about concurrency and about all the things that can go wrong, with all the consequences. For intance, to deal with unavailable nodes and network interruptions.

### 3. Mention the three main approaches to replication described on the book.
* **Single-leader replication:** Clients send all writes to a single note, which sends a steam of data cange events to the other replicas (followers). Read can be performed on any replica, but reads from followers may be stale.
* **Multi-leader replication:** Clients send each write to one of the several leader nodes, any of which can accept writes. The leaders send streams of data change events to each other and to any follower nodes.
* **Leaderless replication:** CLients send each write to several nodes, and read from several nodes in parallel in order ro detect and correct nodes with stale data.

### 4. Which is an advantage of the single-leader replication?
Single-leader replication is fairly easy to understand and there is no conflicy resolution to worry about.

### 5. What is it to read-after-write consistency?
It is a consistency model that helps to the developer to decide how an application shoul behave under a replication lag which causes strange effects. Basically, it refers to the users who should always see data that they submitted themselves.

### 6. Why concurrency issues are inherent to multi-leader and leaderless replication methods?
Because they allow multiple writes to happen concurrently, conflicts may occur.

### 7.

### 8.

### 9.

### 10.
