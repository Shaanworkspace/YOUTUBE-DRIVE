# LeetCode 921 - Minimum Add to Make Parentheses Valid

**Problem Link:** https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/

**Approach:** Stack + Unmatched Closing Counter
- Push every `(` onto the stack.
- On `)`: pop if stack has `(`, else count one needed `(`.
- Answer = needOpen + stack.size() (leftover opens need closings).
- Time: O(n) | Space: O(n) stack (can be optimized to O(1) with a counter).

---

## Java

```java
class Solution {
    public int minAddToMakeValid(String s) {
        Stack<Character> stack = new Stack<>();
        int needOpen = 0;

        for (char currentBracket : s.toCharArray()) {
            if (currentBracket == '(') {
                stack.push(currentBracket);
            } else {
                if (!stack.isEmpty()) {
                    stack.pop();
                } else {
                    needOpen++;
                }
            }
        }

        return needOpen + stack.size();
    }
}
```

---

## Python

```python
class Solution:
    def minAddToMakeValid(self, s: str) -> int:
        stack = []
        need_open = 0

        for ch in s:
            if ch == '(':
                stack.append(ch)
            else:
                if stack:
                    stack.pop()
                else:
                    need_open += 1

        return need_open + len(stack)
```

---

## C++

```cpp
class Solution {
public:
    int minAddToMakeValid(string s) {
        stack<char> st;
        int needOpen = 0;

        for (char currentBracket : s) {
            if (currentBracket == '(') {
                st.push(currentBracket);
            } else {
                if (!st.empty()) {
                    st.pop();
                } else {
                    needOpen++;
                }
            }
        }

        return needOpen + (int)st.size();
    }
};
```

---

## C

```c
int minAddToMakeValid(char* s) {
    int top = -1;
    int needOpen = 0;

    for (int i = 0; s[i] != '\0'; i++) {
        if (s[i] == '(') {
            top++;
        } else {
            if (top >= 0) {
                top--;
            } else {
                needOpen++;
            }
        }
    }

    return needOpen + (top + 1);
}
```
