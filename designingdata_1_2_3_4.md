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
