# LeetCode 20 - Valid Parentheses

**Problem Link:** https://leetcode.com/problems/valid-parentheses/description

**Companies:** Google, Amazon, Microsoft, Meta, Bloomberg, Apple

---

## Approach 1: Stack — Push Open, Match Close (Classic)

Push every opening bracket. On a closing bracket, fail if the stack is empty or the top is not the matching opener. Valid only if the stack is empty at the end.
Time: O(n) | Space: O(n)

## Approach 2: 1 Line Trick — Repeated Pair Replace (No Stack)

Repeatedly delete every "()", "{}" and "[]" pair until none remain. If the string collapses to empty, every bracket matched in the correct nested order.
Time: O(n^2) worst case | Space: O(n) | Passes: simplest interview trick, zero extra data structure

---

## Java

```java
import java.util.Stack;

class Solution {
    public boolean isValid(String s) {


        Stack<Character> stack = new Stack<>();


        for (char ch : s.toCharArray()) {


            // Opening bracket
            if (ch == '(' || ch == '{' || ch == '[') {
                stack.push(ch);
            }


            // Closing bracket
            else {


                if (stack.isEmpty()) {
                    return false;
                }


                char top = stack.pop();


                if (ch == ')' && top != '(') {
                    return false;
                }


                if (ch == '}' && top != '{') {
                    return false;
                }


                if (ch == ']' && top != '[') {
                    return false;
                }
            }
        }


        return stack.isEmpty();
    }
}
```

```java
// Approach 2: 1 Line Trick — Repeated Pair Replace (No Stack)
class Solution {
    public boolean isValid(String s) {
        while (s.contains("()") || s.contains("{}") || s.contains("[]")) {
            s = s.replace("()", "").replace("{}", "").replace("[]", "");
        }
        return s.isEmpty();
    }
}
```

---

## Python

```python
# Approach 1: Stack — Push Open, Match Close
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        pairs = {')': '(', '}': '{', ']': '['}
        for ch in s:
            if ch in '({[':
                stack.append(ch)
            else:
                if not stack or stack.pop() != pairs[ch]:
                    return False
        return not stack

# Approach 2: 1 Line Trick — Repeated Pair Replace (No Stack)
class Solution:
    def isValid(self, s: str) -> bool:
        while '()' in s or '{}' in s or '[]' in s:
            s = s.replace('()', '').replace('{}', '').replace('[]', '')
        return s == ''
```

---

## C++

```cpp
// Approach 1: Stack — Push Open, Match Close
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for (char ch : s) {
            if (ch == '(' || ch == '{' || ch == '[') {
                st.push(ch);
            } else {
                if (st.empty()) return false;
                char top = st.top(); st.pop();
                if (ch == ')' && top != '(') return false;
                if (ch == '}' && top != '{') return false;
                if (ch == ']' && top != '[') return false;
            }
        }
        return st.empty();
    }
};

// Approach 2: 1 Line Trick — Repeated Pair Replace (No Stack)
class Solution {
public:
    bool isValid(string s) {
        while (s.find("()") != string::npos ||
               s.find("{}") != string::npos ||
               s.find("[]") != string::npos) {
            size_t p;
            while ((p = s.find("()")) != string::npos) s.erase(p, 2);
            while ((p = s.find("{}")) != string::npos) s.erase(p, 2);
            while ((p = s.find("[]")) != string::npos) s.erase(p, 2);
        }
        return s.empty();
    }
};
```

---

## C

```c
// Approach 1: Stack — Push Open, Match Close
bool isValid(char* s) {
    int n = strlen(s);
    char* st = (char*)malloc(n + 1);
    int top = -1;
    for (int i = 0; s[i]; i++) {
        char ch = s[i];
        if (ch == '(' || ch == '{' || ch == '[') {
            st[++top] = ch;
        } else {
            if (top < 0) { free(st); return false; }
            char t = st[top--];
            if (ch == ')' && t != '(') { free(st); return false; }
            if (ch == '}' && t != '{') { free(st); return false; }
            if (ch == ']' && t != '[') { free(st); return false; }
        }
    }
    bool ans = (top == -1);
    free(st);
    return ans;
}

// Approach 2: 1 Line Trick — Repeated Pair Replace (No Stack)
bool isValid(char* s) {
    int n = strlen(s);
    char* buf = (char*)malloc(n + 1);
    strcpy(buf, s);
    int len = n, changed = 1;
    while (changed) {
        changed = 0;
        int w = 0;
        for (int i = 0; i < len; i++) {
            if (i + 1 < len &&
                ((buf[i] == '(' && buf[i+1] == ')') ||
                 (buf[i] == '{' && buf[i+1] == '}') ||
                 (buf[i] == '[' && buf[i+1] == ']'))) {
                i++;
                changed = 1;
            } else {
                buf[w++] = buf[i];
            }
        }
        len = w;
        buf[len] = '\0';
    }
    bool ans = (len == 0);
    free(buf);
    return ans;
}
```
