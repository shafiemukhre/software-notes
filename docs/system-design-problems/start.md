---
draft: "false"
sidebar_position: 10
---

# Start here

## Frameworks for system design interview

- Step 1: Understand the problem, establish design scope, list functional and non-functional requirements, and do back-of-the-envelope estimation (3 - 10 mins)
- Step 2: Propose a high-level design and get buy-in (10 - 15 mins)
- Step 3: Design deep dive (10 - 25 mins)
- Step 4: Wrap-up (3 - 5 mins)

## System Design Template

This template is originally from a discussion [post](https://leetcode.com/company/amazon/discuss/229177/My-System-Design-Template) on leetcode.

**1. Feature Expectation (5 mins)**

```
(1) Use cases
(2) Scenarios that will not be covered
(3) Who will use
(4) How many will use
(5) Usage patterns
```

**2. Estimations (5 mins)**

```
(1) Throughput (QPS for read and write queries)
(2) Latency expected from the system (for read and write queries)
(3) Read/Write ratio
(4) Traffic estimates
    - Write (QPS, Volume of data)
    - Read  (QPS, Volume of data)
(5) Storage estimates
(6) Memory estimates
    - If we are using a cache, what is the kind of data we want to store in cache
    - How much RAM and how many machines do we need for us to achieve this ?
    - Amount of data you want to store in disk/ssd
// 7 - 9 are essential estimation for distributed systems
(7) Key metrics to measure
    - For example, in the case of designing a search system, we will be interested to see how many keywords are resulting in blank search results. Here the ratio of search hits is important so we also need to know the number of search queries we are receiving per minute.
    - We can use tools like Graphana with Prometheus, AppDynamics, etc.
(8) System health monitoring
    - Measuring app index, the latency of microservices
    - We can use Newrelic, AppDynamics
(9) Log systems
    - We can use ELK(Elastic, Logstash, Kibana) or Logtail, etc.
```

**3. Design goals (5 mins)**

```
(1) Latency and Throughput requirements
(2) Consistency vs Availability  [Weak/strong/eventual => consistency | Failover/replication => availability]
```

**4. High level design (5 - 10 mins)**

```
(1) APIs for Read/Write scenarios for crucial components
(2) Database schema
(3) Basic algorithm
(4) High level design for Read/Write scenario
```

**5. Deep dive (15 - 20 mins)**

```
(1) Scaling the algorithm
(2) Scaling individual components:
    -> Availability, Consistency and Scale story for each component
    -> Consistency and availability patterns
(3) Think about the following components, how they would fit in and how it would help
    a) DNS
    b) CDN [Push vs Pull]
    c) Load Balancers [Active-Passive, Active-Active, Layer 4, Layer 7]
    d) Reverse Proxy
    e) Application layer scaling [Microservices, Service Discovery]
    f) DB [RDBMS, NoSQL]
        > RDBMS
            >> Master-slave, Master-master, Federation, Sharding, Denormalization, SQL Tuning
        > NoSQL
            >> Key-Value, Wide-Column, Graph, Document
                Fast-lookups:
                -------------
                >>> RAM  [Bounded size] => Redis, Memcached
                >>> AP [Unbounded size] => Cassandra, RIAK, Voldemort
                >>> CP [Unbounded size] => HBase, MongoDB, Couchbase, DynamoDB
    g) Caches
        > Client caching, CDN caching, Webserver caching, Database caching, Application caching, Cache @Query level, Cache @Object level
        > Caching patterns/policies:
            >> Cache aside
            >> Write through
            >> Write behind
            >> Refresh ahead
        > Eviction techniques:
            >> LRU
            >> LFU
            >> FIFO
    h) Asynchronism
        > Message queues
        > Task queues
        > Back pressure
    i) Communication
        > TCP
        > UDP
        > REST
        > RPC
```

**6. Justify (5 mins)**

```
(1) Throughput of each layer
(2) Latency caused between each layer
(3) Overall latency justification
```


## Tips

**Get started with this**

```
Notes:
- start typing here..

Functional requirements:
- 

Non-functional requirements:
- 

Estimations:
- 

```


## Resources

- [System design cheatsheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f) - by @vasanthk recommended by System Design Primer
- [System Design Blueprint: The Ultimate Guide](https://webcache.googleusercontent.com/search?q=cache:https://medium.com/bytebytego-system-design-alliance/system-design-blueprint-the-ultimate-guide-e27b914bf8f1)
- [System Design Interview Question Handbook – Concepts You Should Know](https://www.freecodecamp.org/news/systems-design-for-interviews/)


