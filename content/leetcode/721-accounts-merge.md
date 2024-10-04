---
type: leetcode
title: 721. accounts merge
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/accounts-merge/
date: 2022-11-21
updated: 2024-09-16
---

Given a list of `accounts` where each element `accounts[i]` is a list of strings, where the first element `accounts[i][0]` is a name, and the rest of the elements are **emails** representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some common email to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails **in sorted order**. The accounts themselves can be returned in **any order**.

## solutions

### bfs and seen set

```python
class Solution:
    def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
        # keep track of name associated to each email
        email_to_name = defaultdict()
        
        # set up graph
        graph = defaultdict(list)
        for account in accounts:
            name = account[0]
            
            for i in range(1, len(account)):
                email = account[i]
                email_to_name[email] = name
                if (i+1) < len(account):
                    next_email = account[i+1]
                    graph[email].append(next_email)
                    graph[next_email].append(email)
             

        seen = set()
        ans = []
                    
        def bfs(node):
            ret = []
            q = deque([node])
            while q:
                cur = q.popleft()
                ret.append(cur)
                for neighbor in graph[cur]:
                    if neighbor not in seen:
                        seen.add(neighbor)
                        q.append(neighbor)
            return ret
        
        while len(seen) < len(email_to_name.keys()):
            for email in email_to_name.keys():
                if email not in seen:
                    seen.add(email)
                    emails = bfs(email)
                    ans.append([email_to_name[emails[0]]]+sorted(emails))
        return ans
```

- we create a [[graph]] of all the emails that are related to each other.
- all the emails that belong to a single person will be connected and disjoint from all the other emails.
- we can bfs from an email to find all the other emails for a person.
	- keep a `seen` set so we don’t look at the same email twice.

### union-find

```python
class UnionFind:
    def __init__(self, nodes):
        self.parent = {}
        self.size = {}
        for node in nodes:
            self.parent[node] = node
            self.size[node] = 1
        
    def find(self, x):
        if x != self.parent[x]:
            self.parent[x] = self.find(self.parent[x]) # Path compression
        return self.parent[x]
    
    def union(self, u, v):
        pu, pv = self.find(u), self.find(v)
        if pu == pv: return False  # Return False if u and v are already union
        if self.size[pu] > self.size[pv]: # Union by larger size
            self.size[pu] += self.size[pv]
            self.parent[pv] = pu
        else:
            self.size[pv] += self.size[pu]
            self.parent[pu] = pv
        return True

class Solution:
    def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
        # keep track of name associated to each email
        email_to_name = collections.defaultdict()
        
        # set up graph
        graph = collections.defaultdict(list)
        for account in accounts:
            name = account[0]

            # so all accounts show up in graph
            if len(account) == 2:
                graph[account[1]] = []
                email_to_name[account[1]] = name
            
            else:
                for i in range(1, len(account)):
                    email = account[i]
                    email_to_name[email] = name
                    if (i+1) < len(account):
                        next_email = account[i+1]
                        graph[email].append(next_email)
                        graph[next_email].append(email)
        
        # create union find, and union all edges
        uf = UnionFind(list(graph.keys()))
        for key in graph:
            for neighbor in graph[key]:
                uf.union(key, neighbor)

        # find every node again to make sure parents are compressed fully
        for key in graph:
            uf.find(key)
        
        # now we should have our connected components.
        # just manipulate to the output format.
        collected = collections.defaultdict(list)
        for key in uf.parent:
            parent = uf.parent[key]
            child = key
            collected[parent].append(child)
        ans = []
        for key in collected:
            ans.append([email_to_name[key]] + sorted(collected[key]))

        return ans
```

- we use a union-find technique to create sets that contain all the nodes that are connected.
- then, we just collect them into the output format.

Categories:: [[bfs]], [[dfs]], [[union-find]]
