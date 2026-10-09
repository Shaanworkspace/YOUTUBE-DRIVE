# LeetCode 1541 - Minimum Insertions to Balance a Parentheses String

**Problem Link:** https://leetcode.com/problems/minimum-insertions-to-balance-a-parentheses-string/

**Companies:** Meta

**Approach:** Single-pass greedy with two counters (open, insertions). Each '(' needs two consecutive ')'. On a lone ')', insert one ')'. Match each '))' pair against an open bracket, inserting '(' when none exists. Leftover opens each need two ')'.
Time: O(n) | Space: O(1)

---

## Java

```java
class Solution {
    public int minInsertions(String s) {
        int open = 0;
        int insertions = 0;


        for (int i = 0; i < s.length(); i++) {


            if (s.charAt(i) == '(') {
                open++;
            } else {


                // If the next character is not ')',
                // insert one ')' to complete the pair.
                if (i + 1 < s.length() && s.charAt(i + 1) == ')') {
                    i++;
                } else {
                    insertions++;
                }


                // Match the closing pair with an opening bracket.
                if (open > 0) {
                    open--;
                } else {
                    // No opening bracket exists; insert '('.
                    insertions++;
                }
            }
        }


        // Each remaining '(' needs two ')'.
        insertions += open * 2;


        return insertions;
    }
}
```

---

## Python

```python
class Solution:
    def minInsertions(self, s: str) -> int:
        open_count = 0
        insertions = 0
        i, n = 0, len(s)

        while i < n:
            if s[i] == '(':
                open_count += 1
            else:
                # If the next character is not ')',
                # insert one ')' to complete the pair.
                if i + 1 < n and s[i + 1] == ')':
                    i += 1
                else:
                    insertions += 1

                # Match the closing pair with an opening bracket.
                if open_count > 0:
                    open_count -= 1
                else:
                    # No opening bracket exists; insert '('.
                    insertions += 1
            i += 1

        # Each remaining '(' needs two ')'.
        insertions += open_count * 2

        return insertions
```

---

## C++

```cpp
class Solution {
public:
    int minInsertions(string s) {
        int open = 0;
        int insertions = 0;
        int n = s.size();

        for (int i = 0; i < n; i++) {
            if (s[i] == '(') {
                open++;
            } else {
                // If the next character is not ')',
                // insert one ')' to complete the pair.
                if (i + 1 < n && s[i + 1] == ')') {
                    i++;
                } else {
                    insertions++;
                }

                // Match the closing pair with an opening bracket.
                if (open > 0) {
                    open--;
                } else {
                    // No opening bracket exists; insert '('.
                    insertions++;
                }
            }
        }

        // Each remaining '(' needs two ')'.
        insertions += open * 2;

        return insertions;
    }
};
```

---

## C

```c
int minInsertions(char* s) {
    int open = 0;
    int insertions = 0;
    int n = strlen(s);

    for (int i = 0; i < n; i++) {
        if (s[i] == '(') {
            open++;
        } else {
            // If the next character is not ')',
            // insert one ')' to complete the pair.
            if (i + 1 < n && s[i + 1] == ')') {
                i++;
            } else {
                insertions++;
            }

            // Match the closing pair with an opening bracket.
            if (open > 0) {
                open--;
            } else {
                // No opening bracket exists; insert '('.
                insertions++;
            }
        }
    }

    // Each remaining '(' needs two ')'.
    insertions += open * 2;

    return insertions;
}
```
