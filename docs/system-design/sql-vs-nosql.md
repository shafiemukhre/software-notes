---
sidebar_position: 20
---

# SQL vs NoSQL

## SQL Databases

**When to Use:**

- When you need strong ACID (Atomicity, Consistency, Isolation, Durability) compliance for transactions.
- For applications requiring complex queries and reports.
- When dealing with a structured data model with clear schemas.
- For applications where data integrity and relations (e.g., foreign keys) are crucial.

**Pros:**

- **Structured Data**: SQL databases are ideal for structured data and provide a powerful schema to enforce data integrity and relationships.
- **Complex Queries**: They excel at handling complex queries and transactions, thanks to their powerful query language.
- **ACID Compliance**: Ensures reliable transactions, which is critical for applications like banking systems where data integrity is paramount.

**Cons:**

- **Scalability**: Traditional SQL databases can struggle with horizontal scaling and handling very large volumes of data across distributed systems.
- **Schema Rigidity**: Any changes to the data structure require schema modifications, which can be cumbersome and slow to implement in large databases.

**Examples of Software/Applications for SQL:**

- **E-commerce Platforms** (e.g., Magento, WooCommerce): These require complex transactions, inventory management, and user data relationships.
- **Banking and Financial Applications**: Where transaction integrity (ACID properties) is critical.
- **Enterprise Applications**: That need complex queries, extensive reporting, and data analytics.

## NoSQL Databases

**When to Use:**

- For applications requiring high scalability and performance with large volumes of data.
- When the data model is flexible or frequently changing.
- For projects that require rapid development and iterations.
- In cases where the application demands efficient storage and retrieval of large amounts of unstructured or semi-structured data.

**Pros:**

- **Scalability**: NoSQL databases are designed for horizontal scaling, making them suitable for handling very large volumes of data across distributed systems.
- **Flexibility**: They allow you to store unstructured, semi-structured, or structured data with flexible schemas.
- **High Performance**: Optimized for specific data models and

**Cons**

- **Lack of Standardization**: Unlike SQL databases, which have a standardized query language (SQL), NoSQL databases often use different query languages and models. This lack of standardization can result in a steeper learning curve and difficulties in transitioning or integrating systems.
- **Consistency Models**: Many NoSQL databases employ eventual consistency rather than strict ACID compliance, which might not be suitable for applications requiring immediate consistency. This could lead to challenges in transactions that need to be precisely coordinated.
- **Transaction Support**: While some NoSQL databases have introduced support for transactions, they typically do not offer the same level of support as SQL databases. This can be a limiting factor for applications requiring complex transactions.
- **Data Integrity and Relationships**: NoSQL databases generally do not enforce data integrity and relationships as rigorously as SQL databases. This means the application code often has to manage these aspects, potentially leading to more complexity and room for errors.
- **Maturity and Ecosystem**: Although NoSQL databases have been around for a while, their ecosystems, tools, and third-party support might not be as mature or extensive as those available for SQL databases.

**Examples of Software/Applications for NoSQL**

Given their characteristics, NoSQL databases are well-suited for several types of applications:

- **Social Media Platforms**: Applications like Twitter or Instagram that handle vast amounts of unstructured or semi-structured data (e.g., posts, comments, likes) can benefit from the schema flexibility of document-based NoSQL databases like MongoDB.
- **Real-Time Big Data Analytics**: Platforms that process and analyze large streams of real-time data, such as log analysis tools or recommendation engines, often use NoSQL databases like Cassandra or HBase for their ability to scale horizontally and handle high volumes of writes and reads efficiently.
- **Content Management Systems (CMS)**: Systems that manage dynamic content, which can vary greatly in structure, such as blogs or news websites, can leverage NoSQL databases for their schema flexibility. Examples include using MongoDB or Couchbase.
- **E-Commerce Platforms**: For personalization and session data, where the data model can change rapidly as new features are added, NoSQL databases like Redis (for session management) or DynamoDB (for user preferences) are often used.
- **IoT Applications**: Internet of Things (IoT) applications, which collect sensor data from a multitude of devices, can use NoSQL databases like Cassandra or TimescaleDB (a time-series SQL database with NoSQL features) to efficiently store and query time-stamped data.
- **Mobile Apps**: Mobile applications that require syncing data across devices, such as note-taking apps or to-do list apps, often use NoSQL databases for their ability to handle unstructured data and offer offline synchronization capabilities.

## ACID vs BASE

### ACID

ACID is a set of properties of relational database transactions.

- **Atomicity** - Each transaction is all or nothing
- **Consistency** - Any tranaction will bring the database from one valid state to another
- **Isolation** - Excuting transactions concurrently has the same results as if the transactions were executed serially
- **Durability** - Once a transaction has been committed, it will remain so

There are many techniques to scale a relational database: master-slave replication, master-master replication, federation, sharding, denormalization, and SQL tuning.

### BASE

NoSQL is a collection of data items represented in a key-value store, document-store, wide column store, or a graph database. Data is denormalized, and joins are generally done in the application code. Most NoSQL stores lack true ACID transactions and favor eventual consistency.

**BASE** is often used to describe the properties of NoSQL databases. In comparison with the CAP Theorem, BASE chooses availability over consistency.

Basically available - the system guarantees availability.
Soft state - the state of the system may change over time, even without input.
Eventual consistency - the system will become consistent over a period of time, given that the system doesn't receive input during that period.
In addition to choosing between SQL or NoSQL, it is helpful to understand which type of NoSQL database best fits your use case(s). We'll review key-value stores, document-stores, wide column stores, and graph databases in the next section.
