---
draft: "true"
---
# Design a URL Shortener

## Skeleton Summary

Step 1: Requirements and BOE estimations

**Example Questions**

- What is the traffic volume, how many URLs are generated per day? (100 million)
- How long is the shortened URL? (as short as possible or 6 - 11)
- What characters are allowed in the shortened URL? (62 or 58 chars: A-Z, a-z, 0-9)
- Can the users create custom short links, create custom expiry dates, update short links, and delete short links? (assume yes to all)

Functional Requirements: Generate short URL, redirect short URL, custom short links, deletion, update, expiry date.

Non-functional requirements: Highly available system, horizontally scalable, low latency smooth experience, unpredictable short URL, and (optionally) readable/distinguishable short link.



Back-of-the-envelope estimation
- 10m URLs per day -> 10m  / 24 / 3600 = 116 write operation per second
- 1:100 write:read ratio -> 116 x 100 = 100k read operation per second
- 


| header 1 |     |
| -------- | --- |
| dsasa    |     |
