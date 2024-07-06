---
type: system-design-question
title: design reddit
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-02-24
---

## requirements

### functional

- Create posts
- Upvote/downvote posts
- Fetch feeds
	- Hot, Top, New

### non-functional

- Low latency retrieving queries.
- Availability over strong consistency for almost all of the operations.
- High read/write ratio.
- Unique read patterns (long tail).

## deep dives

- How to deal with imbalanced read/write patterns (celebrity problem).
- Considering upvotes (writes) on popular/new posts.
- How to organize data stores to avoid scatter-gather, good partition keys/indices.
- Fanout? Does it make sense?

