---
type: moc
aliases: []
title: "system design moc"
date: 2022-11-26
updated: 2024-09-13
---

## book and course notes

- [[designing-data-intensive-applications]] - A very comprehensive and in-depth look at all aspects of creating a large-scale distributed system.
- [[system-design-primer]] - A higher-level overview of system design concepts from a Github guide.
- [[system-design-interview-an-insiders-guide-by-alex-yu]] - A lightweight overview of system design concepts, more focused on practical interview topics.
- [[cs75-scalability-lecture]] - An intro lecture to scalability.

## tech blogs

- [[tech-blog-readings]] - A collection of tech blogs that I’ve read and highlighted/taken notes on.

## interviews

![[Pasted image 20240515215150.png]]

![Steps to take during a system design interview](https://github.com/ashishps1/awesome-system-design-resources/raw/main/diagrams/interview-template.png)

1. Gather functional requirements through suggestions and questions. Who is the customer, use cases, etc.
2. If applicable, discuss system restraints. What is out-of-scope?
3. Do back-of-envelope estimations when they’re necessary to inform a decision.
	- This includes estimating request throughput, data storage.
4. Think about high-level API requirements to guide your thoughts. What HTTP requests will a user realistically need to hit?
5. Sketch out a high-level system design, that can cover the main non-functional components, making sure to justify decisions and only add details when necessary!
6. Think about a couple database tables that are relevant to the solution; pick a database technology at this time.
7. Before talking about scaling, perfect the design for a single user, making sure all the functional requirements are achieved.
8. Talk about scaling. Discuss non-functional requirements and trade-offs when making decisions.
	- Find bottlenecks and SPoF’s.
9. Walk through your design like it’s code. Address failure scenarios if there is time.

**Meta tips:**

- Start with a naive solution, then go through functional, non-functional requirements to find where the solution breaks down.
	- Iterate over your system design diagram!
	- Only add/change things when it’s necessary!
- Tips for defining non-functional requirements.
	- Think about scalability, availability/consistency, and performance, and maybe durability if data persistence is required.
		- **Scalability:** Think about DAU, storage requirements, read/write ratio, requests/second.
		- **Availability/Consistency**: Tradeoffs, eventual/causal/strong consistency.
		- **Durability**: Can we afford to lose data/writes.
- Treat interviewer as a coworker with which you are working with.
	- Provide maximum number of positive data points!
- Call it out when you unsure about something!
- Use function call syntax (`myFunction(params)`) for API level design instead of HTTP requests.

See [[system-design-interview-questions]] for my journey in practicing these questions and giving myself feedback.

## insider tips

- As a mid-level candidate, it might be good to let the interviewer drive instead of trying to fill all the dead air… this way, it’s more natural and you’re less likely to dig yourself into a hole.
- Call out when you don’t know something.
- Tips for dealing with cold versus warm interviewers:
	- say stuff like “correct me if I'm wrong, but I think we can do this.”
- Don’t go into stuff like “how many 9s” if it won’t influence your answer.
- Assess, provide opinion thoughts, then solicit feedback!! Don’t just write a design from rote memory.
- Functional requirements mostly stem from _data access patterns._

## formation course notes

- Stay on track!
	- Don’t dig yourself into a rabbit hole - clarify requirements, and repeat them back. Ask if you’re missing anything before continuing.
	- Don’t try to prove seniority!
		- e.g. Don’t bring up hot shards when it isn’t relevant…
	- Instead of jumping to a solution, first identify what the problems/bottlenecks are!!
- Communication.
	- Don’t get stuck in requirements gathering.
		- Ask about functionality! User journey, what does the product do.
	- Write as you go!!
	- If a decision is worth stating, then it’s worth defending/showing your work!
		- When making decisions, walk through your thought process before making a decision!
- Thinking like an engineer.
	- Start from requirements.
	- Foresee edge cases/non-happy path!
- Driving the conversation.
	- Use “let’s”.
	- Identify the hardest problem.
	- Don’t ask for too much permission!

## references

- https://www.teamblind.com/post/My-Approach-to-System-Design-V4SJARdx
- https://interviewing.io/guides/system-design-interview/part-two#part-2-introduction
