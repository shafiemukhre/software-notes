---
sidebar_position: 30
draft: "true"
---
# Design a rate limiter

## Step by step

### Step 1

**What is a rate limiter**?

A rate limiter is used to control the rate of traffic sent by a client or a service. For examples:
- A user can create no more than 2 posts per second.
- You can only create a maximum of 10 accounts per day from the same IP address.

Benefits of using an API rate limiter:
- Protect from DoS (Denial of Service) attacks. (note: rate limiter can't protect against DDoS - Distributed DoS)
- Reduce cost.
- Prevent servers from being overloaded.

**Questions to ask**

- Client-side or server-side API rate limiter? —> server-side API rate limiter.
- Does the rate limiter throttle API requests based on IP or other properties [*side note: what are the other properties?*]? —> The rate limiter should be flexible enough to support different sets of throttle rules.
- Will this work in a distributed environment? —> yes
- 