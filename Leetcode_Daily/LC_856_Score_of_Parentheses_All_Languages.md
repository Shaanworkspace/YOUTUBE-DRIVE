# LeetCode 856 - Score of Parentheses

**Problem Link:** https://leetcode.com/problems/score-of-parentheses/

**Companies:** Bloomberg, Meta, Amazon, Google, TikTok

**Approach:** Stack storing running scores (single pass). Push 0 on `(`, on `)` pop top as inner score, compute `max(2 * top, 1)`, pop previous total, push their sum.

**Complexity:** Time O(n) | Space O(n)

---

## Java

```java
class Solution {
    public int scoreOfParentheses(String s) {


        Stack<Integer> stack = new Stack<>();
        stack.push(0);


        for (char ch : s.toCharArray()) {


            if (ch == '(') {


                stack.push(0);


            } else {


                int top = stack.pop();


                int A = Math.max(2 * top, 1);


                int B = stack.pop();


                stack.push(A + B);
            }
        }


        return stack.pop();
    }
}
```

---

## Python

```python
class Solution:
    def scoreOfParentheses(self, s: str) -> int:
        stack = [0]

        for ch in s:
            if ch == '(':
                stack.append(0)
            else:
                top = stack.pop()
                a = max(2 * top, 1)
                b = stack.pop()
                stack.append(a + b)

        return stack.pop()
```

---

## C++

```cpp
class Solution {
public:
    int scoreOfParentheses(string s) {
        stack<int> st;
        st.push(0);

        for (char ch : s) {
            if (ch == '(') {
                st.push(0);
            } else {
                int top = st.top(); st.pop();
                int A = max(2 * top, 1);
                int B = st.top(); st.pop();
                st.push(A + B);
            }
        }

        return st.top();
    }
};
```

---

## C

```c
int scoreOfParentheses(char* s) {
    int stack[60];
    int top = -1;
    stack[++top] = 0;

    for (int i = 0; s[i] != '\0'; i++) {
        if (s[i] == '(') {
            stack[++top] = 0;
        } else {
            int t = stack[top--];
            int A = (2 * t > 1) ? 2 * t : 1;
            int B = stack[top--];
            stack[++top] = A + B;
        }
    }

    return stack[top];
}
```
