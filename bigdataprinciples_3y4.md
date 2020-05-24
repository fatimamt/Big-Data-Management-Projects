This is the continuation of the Questions & Answers taken from the book Big Data Priciples and Best Practices of Scalable Realtime Data Sytems.

For this file, the information is taken from chapters 3 and 4.

**DISCLAIMER**

Some of the questions and answers are complemented with trusted online resoucers which will be at the end of this file.

# Chapter 3. Data model for Big Data: Illustration
## 1. Why the JSON format is so important? Mention an use. Does it have any disadvantage?
The JSON format is an easy one to get started due to the structure that it follows.

Example:
> books = {
>
>	"Title": "Big Data: Principles and best practices of scalable realtime data systems",
>
>	"Author": \["Nathan Marz", "James Warren"],
>
>	"Genre": \["Academic", "Data Science", "Big Data"]
>
>}

Nonetheless, this JSON format may not be the most recommended for use by a team of developers, due to the ease of data corruption, issue hard to debug.
## 2. Characteristcs of serialization frameworks
Serialization helps us to transfer complex data structures by converting these structures into sequences of bytes that can be sent through a stream.

Therefore, serialization frameworks are na easy approach to making an enforceable schema due to the generation of a code for whatever language you wish to use for reading, writing, and validation objects that match your schema.
It is a general-purpose programming language that translates itself into whatever language it is targeting.
## 3. Disadvantages of serialization frameworks
Even though serialization frameworks are useful, they present some limations when achieving a fully rigourus schema. This strategy only check that all required fields are indeed on the schema and with the expected type. Therefore, they are unable to check richer properties which will not match with your data and a problem in your system will be noticeable.
## 4. How does the book recommend to think about a schema?
As a function in a code which takes a parameter (a piece of data), and returns if the information is valid or not.
## 5. Some examples of tools that use serialization frameworks recommended by the book.
* Apache Thrift
* Protocol Buffers
* Avro
# Chapter 4. Data storage on the batch layer.
## 1. Requirements for data storage for the master dataset in the batch layer
To know how the data will be written and read in large amounts. Both, implemented in the batch layer of the Lambda Architecture.
* **Write:** 
	* To be efficient to append new data
 	* To be easy to scale the storage as your dataset grows
* **Read:**
	* The batch storage must support pararell processing to handle large amounts of data in a scalable manner due to the computing functions on the master dataset.
* **Both:** 
	* To make it less expensive or minimized costs, but decompressing your data to suit your specific needs
	* To enforce the inmutability of your master dataset.
## 2. 
## 3.
## 4.
## 5.
## 6. 

# References
* Marz, N., & Warren, J. (2015). Big data: principles and best practices of scalable real-time data systems. Shelter Island: Manning.
* [JSON Format](https://www.json.org/)
* [JSON Syntax](https://www.w3schools.com/js/js_json_syntax.asp)
* [Serialization](http://www.jtech.ua.es/j2ee/publico/lja-2012-13/sesion05-apuntes.html)
