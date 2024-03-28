---
sidebar_position: 20
---

# Scale to Millions of Users

Summary

- Build redundancy at every tier (especially at the server tier and data tier)
- Cache data as much as you can
- Host static assets in CDN
- Scale your data tier by sharding
- Split tiers into individual services (microservices architecture)
- Support multiple data centers
- Monitor your system and use automation tools

Details

- A software has 3 parts: client tier, server tier, and data tier.
- Choose between SQL vs NoSQL database (either key-value, column, document, or graph).
- Horizontal scaling allows you to scale by adding more servers to your pool of resources.
- Problem: If many users access the web server simultaneously and it reaches the web server's load limit, users generally experience slower response or fail to connect to the server.
  - Solution: A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set. This prevents failover issues and improves the availability of the web tier.
- Problem: One database is not enough, it does not support failover and redundancy.
  - Solution: Database replication usually has a master/slave relationship between the original (master - only support write operation) and the copies (slaves - only support read operation).
- To improve load/response time.
  - Solution: add a cache layer (redis, memcached) and use CDN to host static contents.
- Change from stateful server architecture to stateless server architecture. Stateless server means the database stores the state instead of the web server.
- Use multiple data centers to serve different regions or internationally. Users are geoDNS-routed aka geo-routed, to the closest data center.
- To further scale the system, decouple different components of the system so they can be scaled independently. Message queue is a key strategy employed by many real-world distributed systems to solve this problem.
- Horizontal scaling (aka sharding) can also be used to scale the database.

## References

- Alex Xu's System Design Interview Chapter 1
- System design primer: [Design a system that scales to millions of users on AWS](https://github.com/donnemartin/system-design-primer/tree/master/solutions/system_design/scaling_aws#design-a-system-that-scales-to-millions-of-users-on-aws)
- Youtube: [System Design: Scale System From Zero To Million Users](https://www.youtube.com/watch?v=ejofP2VKu-4)
- [Neetcode: The only Cloud services you actually need to know](https://www.youtube.com/watch?v=gcfB8iIPtbY)
-
