---
title: "rate limiter design"
date: 2022-12-08
updated: 2024-03-25
---

## my solution

### functional requirements

- Prevent DDOS attacks.
- Given a request, determine if the specific request should be throttled, and either let it through or deny it.

### non-functional requirements

- Available.
	- If the service is not available, we just have to let requests through, meaning that we’ll be open to DDOS attacks and other issues.
- Low latency.
	- Because this will sit in front of every service, it needs to be low latency to not slow down operations and user requests.
- Scalable.
	- Should scale along with rest of the application as requests start to increase.

### api design

- `shouldAllowRequest(request)`

### high level design

- how do we identify users?
	- unique identifier such as ip address or user ids.
- what logic do we actually use to rate limit?
	- tokens in a bucket.
		- have tokens regenerate for each user per time unit *(up to a maximum number of tokens)*.
		- each time a request comes in, use a token if it’s available.
			- drop the request if there’s no tokens available currently.
	- maximum number of requests in a time window.
		- can be bad if a lot of requests come at the beginning of the window, because no requests will be allowed for the rest of the window.
- components.
	- rule engine to specify tunable parameters.
	- high throughput cache to store all the data of each user’s requests.
	- logging service.
		- nosql database.

### scaling

- Considerations:
	- How to share rate limiting state between distributed rate limiting nodes?
		- Nodes could talk to each other.
			- Host discovery. When new nodes are added or removed, how do the other nodes know about it? Could use gossip protocol.
		- Centralized master node that faciliates.
		- Distributed cache that all the nodes read/write from.

## positive feedback

## critique

## references
