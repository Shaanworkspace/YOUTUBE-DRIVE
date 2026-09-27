# LeetCode 1190 - Reverse Substrings Between Each Pair of Parentheses

**Problem Link:** https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/

**Companies:** Amazon, Meta, Microsoft, PayPal, Agoda, Oracle, Okta, Google, Bloomberg, Adobe, Flipkart

---

## Approach: Stack Simulation (Single Best Approach)

Traverse the string while maintaining a stack of previously built strings plus a
`current` string. On `(` push `current` and reset it. On `)` reverse `current`,
pop the previous string, and concatenate. Plain characters are appended to
`current`. Parentheses are naturally removed.

Time: O(n^2) worst case (nested reversals) | Space: O(n)

---

## Java

```java
class Solution {
    public String reverseParentheses(String s) {

        Stack<String> stack = new Stack<>();
        String current = "";

        for (char ch : s.toCharArray()) {

            if (ch == '(') {
                stack.push(current);
                current = "";
            }

            else if (ch == ')') {
                current = new StringBuilder(current).reverse().toString();

                String previous = stack.pop();
                current = previous + current;
            }

            else {
                current = current + ch;
            }
        }

        return current;
    }
}
```

---

## Python

```python
class Solution:
    def reverseParentheses(self, s: str) -> str:
        stack = []
        current = ""

        for ch in s:
            if ch == '(':
                stack.append(current)
                current = ""
            elif ch == ')':
                current = current[::-1]
                previous = stack.pop()
                current = previous + current
            else:
                current = current + ch

        return current
```

---

## C++

```cpp
class Solution {
public:
    string reverseParentheses(string s) {
        vector<string> stack;
        string current = "";

        for (char ch : s) {
            if (ch == '(') {
                stack.push_back(current);
                current = "";
            } else if (ch == ')') {
                reverse(current.begin(), current.end());
                string previous = stack.back();
                stack.pop_back();
                current = previous + current;
            } else {
                current = current + ch;
            }
        }

        return current;
    }
};
```

---

## C

```c
char* reverseParentheses(char* s) {
    int n = strlen(s);
    char** stack = (char**)malloc(sizeof(char*) * (n + 1));
    int top = -1;
    char* current = (char*)malloc(sizeof(char) * (n + 1));
    current[0] = '\0';
    int len = 0;

    for (int i = 0; s[i] != '\0'; i++) {
        if (s[i] == '(') {
            stack[++top] = current;
            current = (char*)malloc(sizeof(char) * (n + 1));
            current[0] = '\0';
            len = 0;
        } else if (s[i] == ')') {
            for (int l = 0, r = len - 1; l < r; l++, r--) {
                char t = current[l]; current[l] = current[r]; current[r] = t;
            }
            char* previous = stack[top--];
            int plen = strlen(previous);
            char* merged = (char*)malloc(sizeof(char) * (n + 1));
            strcpy(merged, previous);
            strcat(merged, current);
            free(previous);
            free(current);
            current = merged;
            len = plen + len;
        } else {
            current[len++] = s[i];
            current[len] = '\0';
        }
    }

    return current;
}
```
