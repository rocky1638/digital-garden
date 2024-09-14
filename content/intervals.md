---
type: concept
title: intervals
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-08-28
---

## how to determine if two intervals intersect

Say we have two intervals $I_1$ and $I_2$ such that $I_1 = [s_1, e_1]$ and $I_2 = [s_2, e_2]$.

It’s hard to enumerate all of the intersection conditions, but only two conditions satisfy the non-overlap conditions, which are the two cases where the two intervals are disjoint.

$$
(e_1 < s_2) \lor (e_2 < s_1)
$$

We can simply negate this logical statement to find a simplified expression for intersection.

$$
\begin{align}
&=\lnot((e_1 < s_2) \lor (e_2 < s_1)) \\
&=\lnot(e_1 < s_2) \land \lnot(e_2 < s_1) \tag*{By DeMorgan's Law} \\
&=(e_1 \ge s_2) \land (e_2 \ge s_1) \\
\end{align}
$$
