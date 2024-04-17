---
type: <% tp.file.cursor() %>
title: <% tp.file.cursor() %>
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-03-27
---

## my solution

### functional requirements

Brainstorming:

- Users can upload images to their account and view them.
- Users can view other users’ pictures.
- Users can follow other users.
- Users can scroll through a feed of people they’re following.
	- Users can see suggested posts based on their browsing/viewing history.
- Users can like posts.
- Users can comment on posts.
	- Users can reply to comments.

Let’s focus on:

- Users can upload images.
- Users can follow other users.
- Users can view a feed.

### estimating scale

- 2 billion users.
- Storage.
	- 20 photos per user.
	- Photos persist indefinitely.
	- 500KB per photo.
	- 2B * 20 * 500KB = 2B * 1MB = 2M * 1GB = 2000 * 1TB = 2PB
- Requests.
	- Upload image, download images, following each other, viewing a feed.
	- 200M DAU.
	- Many more reads then writes.
	- 2B feed reads per day.

### non-functional requirements

- Low latency.
	- Users shouldn’t have to wait very long to see images/feeds.
- High availability.
	- Any downtime is lots of lost ad money.
- Eventual consistency.
	- When a user uploads an image, it’s ok if someone doesn’t get that image in their feed if they refresh 1 second later. Maybe it’s in their feed ~1 minute later.
- Durable.
	- Users uploaded photos should not disappear.

### api design

- `uploadImage(image, metadata)`
- `getFeed(userId)`
- `follow(user1, user2)`

### design

![[design-instagram-initial.png|Design without scale.]]

![[design-instagram-final-design.png]]

## positive feedback

## critique

- Consider separating out read and write service.
- Consider adding message queue for asynchronous image upload/processing for throughput.
- 

## references

- [Design Instagram](https://www.youtube.com/watch?v=VJpfO6KdyWE)
