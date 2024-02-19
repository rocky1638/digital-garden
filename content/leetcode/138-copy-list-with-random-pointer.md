---
created_at: 2023-01-07
type: leetcode
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/copy-list-with-random-pointer/
---

# 138. Copy List With Random Pointer

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return _the head of the copied linked list_.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val`: an integer representing `Node.val`
- `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will **only** be given the `head` of the original linked list.

```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head: return None

        cur = head
        prev = None
        h = {}

        # create copies of all the nodes
        while cur:
            # create copy and save in hashmap
            copy = Node(cur.val)
            h[id(cur)] = copy

            # set next pointer of previous node
            if prev:
                h[id(prev)].next = copy
            
            # increment index and cur pointer
            prev = cur
            cur = cur.next
        
        cur = head
        while cur:
            # set random pointer on copied nodes
            # based on old nodes
            if cur.random:
                h[id(cur)].random = h[id(cur.random)]
            cur = cur.next
        
        return h[id(head)]
```

- we keep a hash table that maps the old nodes to the new nodes.
- use the `id()` function to key by the memory addresses of the old nodes.

```dataview
table without id file.inlinks as Backlinks
where file.name = this.file.name
```

## Related.

## References.

Categories:: [[linked-list]], [[hashmap]]
