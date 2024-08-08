---
type: article
title: stripe interview
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-15
updated: 2024-07-17
---

# recruiter call notes

## apple pay STAR blurb

Situation: Our application faced high drop-off rates on the payments page due to limited payment options. We needed to integrate a new third-party payment provider to introduce Apple Pay and pave the way for future payment methods.

Task: As the backend engineer, I was responsible for integrating the new payment service, ensuring data integrity and durability, and refactoring existing code to more easily accommodate multiple payment methods.

Action: I collaborated on a two-month project with a senior engineer and cross-functional teams including design, business, and product. My role involved:

1. Developing backend integrations with the new payment API
2. Implementing robust error handling and data durability measures*
	- This was important as because the the payment flow consisted of multiple network calls, we needed to consider how to gracefully handle/fail if any stage of the multi-step process failed.
	- Making sure to commit on the DB at key points (creating a pending transaction, marking the transaction as success/fail), to allow for auditing and reconciliation.
3. Refactoring controller code for polymorphic support of multiple payment methods
4. Coordinating regular integration calls with the provider to overcome documentation challenges
5. Maintaining clear communication with stakeholders throughout the project

Result: We successfully launched a bug-free integration, resulting in:

1. A 20% relative decrease in payment page drop-off rates
2. Apple Pay capturing 35% of all payments within a week of launch
3. A scalable foundation for future payment method integrations

This project exemplifies Stripe's values of being “macro-optimistic”, when we pushed through all of the documentation challenges, believing that we would get it done in the end.

# debugging interview

Stripe and Retool both have a debugging interview — Stripe asks it in the onsite, while Retool uses it as a first-round interview. I ended up receiving offers from both of these companies, so I wanted to share how my experience for these debugging interviews went.

## how the interview usually starts

After exchanging pleasantries, your interviewer will ask you to clone a repo on Github (or they’ll send you the code via email). Don’t worry if your Github is acting up and the good ol’ `git clone` isn’t working— you can just download a ZIP of the repository directly and open it within your editor. The interviewer won’t care— this is a debugging interview, not a “how do I fix my Git” interview, so just do what’s fastest.

There will usually be a README which has instructions, which contains instructions on how to run a test that’s — surprise! — failing.

The Stripe interview involved fixing a single bug, while Retool presented multiple. Stripe used code from a popular open-source library, and Retool provided a custom codebase, relatively smaller in size.

## how to approach this interview

## study the failing test

Read the prompt carefully. Run the test, make sure it is indeed failing. Quickly confirm with the interviewer that you’re looking at the right test.

There’s no way you’ll be able to read through all the code in the repository during the hour you have to debug. Be efficient with your time. Start reading the code containing the failing test, and figure out what the test is trying to do. At a high level, you’re trying to answer these questions:

- What does this function expect the value to be? Why?
- What is the current value? Why?

## Locate the problematic function.

Make sure it’s the right function. Add a print statement or a debugger to be _absolutely sure_ that you are looking at the right spot. Function names are not always unique (e.g. same function name within different modules) — but if you have a decent code editor that lets you right click into a function and jump to the definition, you’re golden. I still recommend the print/debugger to be very sure you’re in the right spot.

## Study the function

Read the function carefully. Say out loud what each line of code is doing. Annotate the code — you don’t have that much time to reread these functions, so I suggest using comments to cache the work you’re doing here. If your interview is friendly, they might correct your statements in real-time. I find it helpful to write a one or two sentence summary of what the function does at the top — though it wouldn’t be overkill to add annotations every few lines in the function.

Repeat as needed as you move from function to function.

## Find code that looks suspicious.

This often comes with experience. For example, there might be an issue with slicing a list in Python; the code might’ve treated the ending index as inclusive of the element. Or, there’s an off-by-one in a for loop somewhere. Or, the list is being mutated but not saved, or the list wasn’t supposed to be mutated but was.

Start by saying a few theories — then validate. I used Python’s pdb to walk through each line of the function to confirm what the values of each variable were and if they were what I expected them to be.

## Repeat until you find the bug.

A well-designed bug squash interview won’t be straightforward — you’ll likely need to go through multiple layers of code, following functions from one to the next. There might be multiple issues with the code, or it may be costly to invalidate theories about which part of the code is wrong.

## Fix the bug.

Write code that solves the bug, but is also easy to understand. Consider whether your edits affect the runtime of the code or mutate the returned output in some other undesired way, and clarify with the interviewer if your suggestion on how to fix the bug is acceptable.

## Tips for Success

## Verbalize your thought process.

Let me repeat that again. **Verbalize your thought process**. Is there a worse way to spend this interview than to just sit in silence and try random theories in your head? What do you think the interviewer is going to write for interview feedback? If you at least tell the interviewer your theories on where the issues are, they have some gauge on what and how you’re thinking about the problem. I’m fairly certain my explanations of what I was doing and why I was doing it was what got me a passing mark in the Stripe debugging round — I could find the bug, and I knew why the code wasn’t working, but I wasn’t sure how to fix it (it involved a bit more specific knowledge that I didn’t have at the time).

## Know how to use the debugger.

If you’re going into a Python debugging interview and you’ve never used pdb before, you’re at a significant disadvantage. Figure out the debugging tools for your language of choice and learn how to use them effectively.

## Keep track of time.

If you’ve made near 0 progress in the first 20 minutes, I’d recommend asking for a hint. If your interviewer has mercy, they’ll give you one — and hopefully it’s enough for you to unblock yourself and make more progress in the rest of the interview.

## Annotate the code.

It’s like leaving breadcrumbs for yourself as you navigate this foreign, confusing land. Save yourself some mental cycles and cache the work you’ve done already via code comments (or even write out what the code is doing on a separate file if you really need to).

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Thanks for reading and best of luck on your interviews!

---

```
There's a screening round to determine whether you will proceed to the onsite interviews or not. And once you get past that, you move onto the on-site ones.

For the screening round, you get a series of coding problem, where one builds on top of the previous one. You're supposed to just figure out how to get the output given a long prompt, and they'll also share some tests to check for themselves that what you wrote is correct. They care about speed and correctness. They don't care about complexity (no big O) nor any fancy algorithm nor data structure - this is actually the theme throughout the entire process.

For the on-site interviews, there's debugging, integration, problem solving (basically same as the screening round), system design, and a call with whoever would be hiring you.

For debugging, they give you an giant open source library with failed unit tests, your job is to figure out what's wrong and fix those tests.

For integration, there are a few steps you follow to put together a working app.

For system design, they simplify part of Stripe and ask how you would design it. This was a LOT simpler than the FAANG ones I've done.
```
