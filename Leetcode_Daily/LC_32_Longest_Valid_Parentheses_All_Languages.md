# LeetCode 32 - Longest Valid Parentheses

**Problem Link:** https://leetcode.com/problems/longest-valid-parentheses/description

**Companies:** Amazon, Meta, Bloomberg, Google, Microsoft

**Approach:** Stack with index tracking (Optimal — Best Approach)
Time: O(n) | Space: O(n)

Push -1 as base. Push index on '('. On ')', pop, then if empty push current index as new base, else update answer with i minus stack top.

---

## Java

```java
class Solution {
    public int longestValidParentheses(String s) {
        Stack<Integer> st = new Stack<>();
        st.push(-1);
        int ans = 0;


        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') st.push(i);
            else {
                st.pop();
                if (st.isEmpty()) st.push(i);
                else ans = Math.max(ans, i - st.peek());
            }
        }
        return ans;
    }
}
```

---

## Python

```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        st = [-1]
        ans = 0
        for i, ch in enumerate(s):
            if ch == '(':
                st.append(i)
            else:
                st.pop()
                if not st:
                    st.append(i)
                else:
                    ans = max(ans, i - st[-1])
        return ans
```

---

## C++

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        vector<int> st;
        st.push_back(-1);
        int ans = 0;
        for (int i = 0; i < (int)s.size(); i++) {
            if (s[i] == '(') st.push_back(i);
            else {
                st.pop_back();
                if (st.empty()) st.push_back(i);
                else ans = max(ans, i - st.back());
            }
        }
        return ans;
    }
};
```

---

## C

```c
int longestValidParentheses(char* s) {
    int n = strlen(s);
    int* st = (int*)malloc((n + 1) * sizeof(int));
    int top = 0;
    st[top++] = -1;
    int ans = 0;
    for (int i = 0; i < n; i++) {
        if (s[i] == '(') st[top++] = i;
        else {
            top--;
            if (top == 0) st[top++] = i;
            else {
                int len = i - st[top - 1];
                if (len > ans) ans = len;
            }
        }
    }
    free(st);
    return ans;
}
```
