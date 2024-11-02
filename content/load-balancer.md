---
date: 2022-11-26
updated: 2024-10-08
type: concept
---

Load balancers are used to distribute incoming client requests across servers or databases while ensuring that requests do not go to unhealthy servers, thereby avoiding single points of failure. They can handle tasks like encrypting requests or reducing the load on servers. Load balancers also maintain session persistence by routing users to the correct servers.

It is common to deploy multiple load balancers in either **active-active** or **active-passive** setups, similar to database replication. Traffic can be routed using methods like round-robin or through different layers:

- **Layer 4** looks at transport layer data (e.g., IP addresses, header ports, and packet contents).
- **Layer 7** focuses on application layer data and can handle more specific routing, such as directing video traffic to video-hosting servers or user billing traffic to secure servers. While Layer 4 is less resource-intensive, Layer 7 offers more flexibility.

However, load balancers can introduce bottlenecks and, if a single one is used, create a single point of failure.
