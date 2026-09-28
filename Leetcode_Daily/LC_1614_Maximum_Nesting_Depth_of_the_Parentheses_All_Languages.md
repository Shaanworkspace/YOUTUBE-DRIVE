# LeetCode 1614 - Maximum Nesting Depth of the Parentheses

**Problem Link:** https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/description

**Companies:** Amazon, Google, Bloomberg, Intel, TCS

**Approach:** Single-pass counter — increment depth on '(', update maxDepth, decrement on ')'.
Time: O(n) | Space: O(1)

---

## Java

```java
class Solution {
    public int maxDepth(String s) {
        int depth = 0;
        int maxDepth = 0;

        for(char c : s.toCharArray()){
            if(c=='('){
                depth++;
                maxDepth = Math.max(depth,maxDepth);
            }
            if(c==')'){
                depth--;
            }
        }

        return maxDepth;
    }
}
```

---

## Python

```python
class Solution:
    def maxDepth(self, s: str) -> int:
        depth = 0
        max_depth = 0

        for c in s:
            if c == '(':
                depth += 1
                max_depth = max(max_depth, depth)
            if c == ')':
                depth -= 1

        return max_depth
```

---

## C++

```cpp
class Solution {
public:
    int maxDepth(string s) {
        int depth = 0;
        int maxDepth = 0;

        for (char c : s) {
            if (c == '(') {
                depth++;
                maxDepth = max(maxDepth, depth);
            }
            if (c == ')') {
                depth--;
            }
        }

        return maxDepth;
    }
};
```

---

## C

```c
int maxDepth(char* s) {
    int depth = 0;
    int maxDepth = 0;

    for (int i = 0; s[i] != '\0'; i++) {
        if (s[i] == '(') {
            depth++;
            if (depth > maxDepth) maxDepth = depth;
        }
        if (s[i] == ')') {
            depth--;
        }
    }

    return maxDepth;
}
```
