---
type: leetcode
title: 271. encode and decode strings
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/encode-and-decode-strings/
date: 2023-01-03
updated: 2024-06-02
---

Design an algorithm to encode **a list of strings** to **a string**. The encoded string is then sent over the network and is decoded back to the original list of strings.

Machine 1 (sender) has the function:

```
string encode(vector<string> strs) {
  // ... your code
  return encoded_string;
}
```

Machine 2 (receiver) has the function:

```
vector<string> decode(string s) {
  //... your code
  return strs;
}
```

So Machine 1 does:

```
string encoded_string = encode(strs);
```

and Machine 2 does:

```
vector<string> strs2 = decode(encoded_string);
```

`strs2` in Machine 2 should be the same as `strs` in Machine 1.

Implement the `encode` and `decode` methods.

You are not allowed to solve the problem using any serialize methods (such as `eval`).

## solutions

### non-ascii delimiter

```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        return "\U0001f600".join(strs)
        

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        return s.split("\U0001f600") 
```

- i just used the smile emoji lol.

### chunked transfer encoding

![fig](https://leetcode.com/problems/encode-and-decode-strings/solutions/328340/Figures/271/encodin.png)
- for each string, compute its length, and append a four character number in front of it in the encoded string.
- fairly easy and straightforward to decode this.
