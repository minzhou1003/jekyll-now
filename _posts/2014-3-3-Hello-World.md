---
layout: post
title: Google File System Summary
---

This paper is motivated by the rapidly growing demands of Google's data processing needs. Specifically, Google needed a better file system to meet their application workloads and technological environment.
The main design idea of GFS is based on the following assumptions (or problems): high component failure rates, huge files, files are write-once and mutated by appending new file, large streaming reads and high sustained throughput favored over low latency.
The GFS's architecture, which is the solution to above problems, it consists of a single master and multiple chunksevers. In their design, files are stored as chunks with a fixed size (64MB) which makes the streaming much easier across the 64MB segment. To ensure the reliability, they replicate each chunk across at least 3 chunkservers. Also, all the metadata is kept on a single master machine, which is a simple centralized management. Besides, there is no data caching on the user side due to the large size of data. Finally, they made the interface to be familiar but also customized the API by adding two operations which are atomic record append and snapshot.
This weakness of this architecture is that it has a single point of failure and a scalability bottleneck because of the single master. To solve this problem, GFS created shadow masters to minimize the master involvement, which means the major job of the master is to store the global metadata. Another way is storing all table in memory to keep the master's scalability high. Additionally, master has an operation log to recover quickly and ensure consistent data
In conclusion, GFS strongly demonstrates how to handle large-scale processing workloads on commodity hardware.
