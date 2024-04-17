---
title: "design pastebin"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-03-26
---

## my solution

### clarifications

- Can users update values for data after they’ve created a share link?

### functional requirements

- User can enter text data into a web application.
- User can persist this text data when they visit the website again.
- User can share specific paste with others using a unique link.
	- How long are these links valid for?
- When a user accesses a link, they see the correct data.
- Stretch goals.
	- Users can lock a paste with a password.

### non-functional requirements

#### estimations

- What is the maximum/average length of text in a paste?
	- Maximum: 10MB per paste.
- How long does each paste persist before being deleted?
	- Persist pastes for 3 years.
- How many pastes are being created daily?
	- 10,000,000 pastes per day.
- How many reads per paste?
	- 50 reads per paste.
- Storage estimate: 10MB * 100,000/day * 365 * 3 = 10MB * 1000,000,000 = 10PB
- Request estimate: 10M + 500M requests per day = 500M/24/60/60 = 6000RPS.

#### requirements

- Durability.
	- Users paste should not disappear before they are supposed to.
- Availability.
	- When users access a paste, they should be able to.
- Scalable.
	- We want to be able to handle lots of data, like our estimates.

### design

![[design-pastebin.png]]

## positive feedback

- Forgot about caching, and hotspots/popular pastes.

## critique

- A little confused and didn’t make too clear of a distinction between generating keys using a hash vs. generating keys using an incrementing counter.

## references

- [Design Text Storage Service like Pastebin](https://www.youtube.com/watch?v=josjRSBqEBI)
