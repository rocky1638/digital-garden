---
type: system-design-question
title: "design dropbox"
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-07
---

## my solution

## positive feedback

## critique

## references

- https://www.youtube.com/watch?v=4wIU4rTV-JU&list=PLjTveVh7FakJOoY6GPZGWHHl4shhDT8iV&index=3
	- Use chunking to allow for parallelized uploads, as well as more efficient versioning (we can avoid re-downloading chunks that haven’t changed).
	- If using multiple leaders to handle file uploads, use version vectors for conflict detection, which can also be helpful for conflict resolution.
	- Store permissions, (maps users to files).
	- Serve chunks from object storage with CDNs to reduce latency.
	- Users can subscribe to file updates through a stream like Kafka, which allows them to constantly receive streams of updates from files that other users (or their other devices) can edit.
