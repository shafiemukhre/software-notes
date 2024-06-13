## General
- Notes should have lots of bullet points, tables, diagrams, and examples.
- Add "tips" call-outs on how to memorize the section when you can.

## Frontend

- [] use storybook. see [this storybook example for react-spreadsheet](https://iddan.github.io/react-spreadsheet/storybook/?path=/story/spreadsheet--basic)
- [] check styleX
- [] write note for scss https://www.youtube.com/watch?v=kFA-ZJ9KTqs
- [ ] blender, react-three-fiber + react-three-rapier (the physics engine)
- [ ] write some notes on ARIA
	- https://www.youtube.com/watch?v=i7lU6v_RejM
	- https://developer.mozilla.org/en-US/docs/Web/Accessibility
	- https://web.dev/learn/accessibility
- [7 Ways to Implement Conditional Rendering in React Applications](https://www.digitalocean.com/community/tutorials/7-ways-to-implement-conditional-rendering-in-react-applications)


## Database modelling

- [✔] ~~Assume you have an existing databases. Can you add a json object into a column of your SQL database to store arbitrary key-value pairs? How the database looks like? Write an API endpoint to fetch all regions from the subscriptions table.~~

## System Design

- [] design in-memory KV store


## System Design Problems
Do overlap problems from System Design Interview book by Alex Xu and and [Grokking Modern System Design Interview (26 hours)](https://www.educative.io/courses/grokking-modern-system-design-interview-for-engineers-managers). Use [donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer) for reviewing system design basics. 

Steps: 1. Clarify/understand the problem + list function vs non-function requirement + BotE estimation -> 2. High-Level Design -> 3. Design dive deep -> Wrap up and review.

Advanced Design Problem
- [ ] Design a URL shortener - reviewed
- [ ] Design a web crawler - reviewed
- [ ] Design a news feed system
- [ ] Design Youtube
- [ ] Design Google Drive
- [ ] Design a chat system (maybe equivalent to WhatsApp)
- [ ] + Design Instagram (from primer)
- [ ] + Design Amazon's sales ranking by category feature (from Primer)
- [ ] + Design a system that scales to millions of users on AWS (from Primer)

Elementary design Problem
- [ ] Design a rate limiter
- [ ] Design consistent hashing
- [ ] Design a key-value store - compare with a key-value store for search engine (from Primer)
- [ ] Design a unique ID generator in a distributed system

? - Should do this as well, since these are from Alex Xu's book
- [ ] Design a notification system
- [ ] Design a search autocomplete system



15 problems :/ -> 5 on Saturday, 5 on Sunday, 5 on Monday
review 75 leetcode (5 mins for each question) on Saturday and 75 neetcode on Sunday.
2 mock interview on Saturday,
2 mock interview on Sunday
5 LP stories on Saturday
5 LP stories on Sunday
do a few low-level design problems on Monday - Wednesday.
Review Neetcode and do amazon tags problem Monday - Wednesday.

- Load balancer
	- active-active load balancer=
- different caching pattern: write-back cache
	- eviction policy, expiration policy, consistency requirements
- crdt - eventual consistency
- multileader/leaderless vs single leader?

Sources:
* [Arpit's System design Masterclass](https://www.youtube.com/watch?v=1r9bPisYaOQ&list=PLsdq-3Z1EPT36NJXTutvKcreetuHCr9a-)
* [AWS Learning Accelerator course](https://courses.beabetterdev.com/courses/aws-learning-accelerator) - seems like a good project to learn AWS serverless.


## Algorithm

- When creating a note, remember to do it like this: https://ryanzhang.info/ctci/topics/python.html and this https://ryanzhang.info/machine_learning/nlp.html, one-page note but long. The goal is to keep on adding new information but as time goes on, keep on rewriting and make sure only the most important notes are there. Expand and shrink it. 
* [ ] Create a note on this: [Leetcode Discuss: Edge cases to consider during problem solving](https://leetcode.com/discuss/general-discussion/988504/Edge-cases-to-consider-during-problem-solving)
- [ ] Learn enum for LLC object-oriented problems
- [ ] This hashing explanation is pretty good: https://www.youtube.com/watch?v=4YiQITXu_iM

- Some problems require TreeMap data structure which is available in Java. Python doesn't have this, bisect is what is normally being used. This is implementation of bisect: https://github.com/python/cpython/blob/3.9/Lib/bisect.py
- 

For quick revision, do all leetcode problems from these list to cover all possible algorithms
* Graph patterns: https://leetcode.com/discuss/general-discussion/971272/Python-Graph-Algorithms-One-Place-for-quick-revision
	* with explanation: https://leetcode.com/discuss/interview-question/4283222/Graph-(Beginners-to-Advanced)-All-Algorithms-Python
* DP patterns: [https://leetcode.com/discuss/general-discussion/972402/Python-template-for-DP-patterns-One-Place-for-quick-revision](https://leetcode.com/discuss/general-discussion/972402/Python-template-for-DP-patterns-One-Place-for-quick-revision) , https://leetcode.com/discuss/study-guide/4988261/dynamic-programming-patterns
* Tree: [https://leetcode.com/discuss/general-discussion/1019622/Python-template-Tree-questions-in-One-Place-for-quick-revision](https://leetcode.com/discuss/general-discussion/1019622/Python-template-Tree-questions-in-One-Place-for-quick-revision)  
* EDGE case: [https://leetcode.com/discuss/general-discussion/988504/Edge-cases-to-consider-during-problem-solving](https://leetcode.com/discuss/general-discussion/988504/Edge-cases-to-consider-during-problem-solving)
* Few Object Oriented Programming (low-level system design) problems.

DP
- [Must do Dynamic Programming Problems Category Wise](https://leetcode.com/company/amazon/discuss/4676022/Must-do-Dynamic-Programming-Problems-Category-Wise)
- [Solved all dynamic programming (dp) problems in 7 months](https://leetcode.com/discuss/general-discussion/1000929/solved-all-dynamic-programming-dp-problems-in-7-months)
- 

## Leadership Principle
- [Amazon LPs Compiled](https://leetcode.com/discuss/interview-experience/1149636/Amazon-LPs-Compiled)
- 