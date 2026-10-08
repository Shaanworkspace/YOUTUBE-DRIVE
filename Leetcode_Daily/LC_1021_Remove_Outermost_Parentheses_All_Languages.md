# LeetCode 1021 - Remove Outermost Parentheses

**Problem Link:** https://leetcode.com/problems/remove-outermost-parentheses/

**Companies:** Google, Amazon, Microsoft, Adobe, Bloomberg

**Approach:** Depth Counter (Single Pass)

Track nesting depth while scanning the string once. An opening bracket is kept only when depth is already non-zero (not outermost). A closing bracket is kept only when depth stays non-zero after decrementing (not outermost). Every primitive decomposition resets depth to zero at its boundary, so the rule holds for each primitive automatically.

**Complexity:** Time O(n) | Space O(n) for the answer (O(1) extra besides output)

---

## Java

```java
class Solution {
    public String removeOuterParentheses(String s) {

        StringBuilder answer = new StringBuilder();
        int depth = 0;

        for (char ch : s.toCharArray()) {

            // Opening bracket
            if (ch == '(') {

                // If we are already inside,
                // this is not the outermost bracket.
                if (depth != 0) {
                    answer.append('(');
                }

                depth++;
            }

            // Closing bracket
            else {

                depth--;

                // If we are still inside,
                // this is not the outermost bracket.
                if (depth != 0) {
                    answer.append(')');
                }
            }
        }

        return answer.toString();
    }
}
```

---

## Python

```python
class Solution:
    def removeOuterParentheses(self, s: str) -> str:
        answer = []
        depth = 0

        for ch in s:
            # Opening bracket
            if ch == '(':
                # Already inside, so not the outermost bracket.
                if depth != 0:
                    answer.append('(')
                depth += 1
            # Closing bracket
            else:
                depth -= 1
                # Still inside, so not the outermost bracket.
                if depth != 0:
                    answer.append(')')

        return ''.join(answer)
```

---

## C++

```cpp
class Solution {
public:
    string removeOuterParentheses(string s) {
        string answer;
        int depth = 0;

        for (char ch : s) {
            // Opening bracket
            if (ch == '(') {
                // Already inside, so not the outermost bracket.
                if (depth != 0) {
                    answer += '(';
                }
                depth++;
            }
            // Closing bracket
            else {
                depth--;
                // Still inside, so not the outermost bracket.
                if (depth != 0) {
                    answer += ')';
                }
            }
        }

        return answer;
    }
};
```

---

## C

```c
char* removeOuterParentheses(char* s) {
    int idx = 0;
    int depth = 0;
    int n = 0;
    while (s[n] != '\0') {
        n++;
    }
    char* answer = (char*)malloc((n + 1) * sizeof(char));

    for (int i = 0; s[i] != '\0'; i++) {
        /* Opening bracket */
        if (s[i] == '(') {
            /* Already inside, so not the outermost bracket. */
            if (depth != 0) {
                answer[idx++] = '(';
            }
            depth++;
        }
        /* Closing bracket */
        else {
            depth--;
            /* Still inside, so not the outermost bracket. */
            if (depth != 0) {
                answer[idx++] = ')';
            }
        }
    }

    answer[idx] = '\0';
    return answer;
}
```
