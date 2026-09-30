# LeetCode 1111 - Maximum Nesting Depth of Two Valid Parentheses Strings

**Problem Link:** https://leetcode.com/problems/maximum-nesting-depth-of-two-valid-parentheses-strings

**Companies:** Google, Bloomreach, Amazon

**Approach:** Greedy depth tracking with modulo 2 assignment.
Track running depth: on `(` increment depth first, then save `depth % 2`;
on `)` save `depth % 2` first, then decrement. This splits parentheses
alternately by depth level so neither group exceeds half the max depth.

**Time:** O(n) | **Space:** O(1) extra (excluding answer array)

---

## Java

```java
class Solution {
    public int[] maxDepthAfterSplit(String seq) {

        int[] answer = new int[seq.length()];
        int depth = 0;

        for (int i = 0; i < seq.length(); i++) {

            if (seq.charAt(i) == '(') {

                depth++;
                answer[i] = depth % 2;

            } else {

                answer[i] = depth % 2;
                depth--;
            }
        }

        return answer;
    }
}
```

---

## Python

```python
class Solution:
    def maxDepthAfterSplit(self, seq: str) -> list[int]:
        answer = [0] * len(seq)
        depth = 0

        for i, ch in enumerate(seq):
            if ch == '(':
                depth += 1
                answer[i] = depth % 2
            else:
                answer[i] = depth % 2
                depth -= 1

        return answer
```

---

## C++

```cpp
class Solution {
public:
    vector<int> maxDepthAfterSplit(string seq) {
        vector<int> answer(seq.size());
        int depth = 0;

        for (int i = 0; i < (int)seq.size(); i++) {
            if (seq[i] == '(') {
                depth++;
                answer[i] = depth % 2;
            } else {
                answer[i] = depth % 2;
                depth--;
            }
        }

        return answer;
    }
};
```

---

## C

```c
int* maxDepthAfterSplit(char* seq, int* returnSize) {
    int n = strlen(seq);
    int* answer = (int*)malloc(n * sizeof(int));
    int depth = 0;

    for (int i = 0; i < n; i++) {
        if (seq[i] == '(') {
            depth++;
            answer[i] = depth % 2;
        } else {
            answer[i] = depth % 2;
            depth--;
        }
    }

    *returnSize = n;
    return answer;
}
```
