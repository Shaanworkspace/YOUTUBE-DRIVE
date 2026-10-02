# LeetCode 22 - Generate Parentheses

**Problem Link:** https://leetcode.com/problems/generate-parentheses/

**Companies:** Amazon, Google, Meta, Microsoft, Apple, Bloomberg

---

## Approach 1: Brute Force — Generate All + Validate

Generate every string of length 2n with '(' and ')', keep only the valid ones using a balance check.
Time: O(2^(2n) * n) | Space: O(n) recursion + output

## Approach 2: Backtracking with Pruning (Best — Interview Standard)

Build only valid strings. Add '(' if open is less than n. Add ')' only if close is less than open. Every partial string stays valid, so no work is wasted.
Time: O(4^n / sqrt(n)) Catalan | Space: O(n) recursion depth

---

## Java

```java
// Approach 1: Brute Force — Generate All + Validate
class Solution {

    public List<String> generateParenthesis(int n) {

        List<String> ans = new ArrayList<>();

        generate("", n, ans);

        return ans;
    }

    // Generate all possible parentheses strings
    void generate(String current, int n, List<String> ans) {

        // String complete ho gayi
        if (current.length() == 2 * n) {

            if (isValid(current)) {
                ans.add(current);
            }

            return;
        }

        // '(' add karo
        generate(current + "(", n, ans);

        // ')' add karo
        generate(current + ")", n, ans);
    }

    // Check whether parentheses are balanced
    boolean isValid(String s) {

        int balanced = 0;

        for (char ch : s.toCharArray()) {

            if (ch == '(') {
                balanced++;
            }
            else {
                balanced--;
            }

            // Closing bracket zyada ho gaya
            if (balanced < 0) {
                return false;
            }
        }

        return balanced == 0;
    }
}
```

```java
// Approach 2: Backtracking with Pruning (Best)
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList<>();
        backtrack(new StringBuilder(), 0, 0, n, ans);
        return ans;
    }

    void backtrack(StringBuilder current, int open, int close, int n, List<String> ans) {
        if (current.length() == 2 * n) {
            ans.add(current.toString());
            return;
        }
        if (open < n) {
            current.append('(');
            backtrack(current, open + 1, close, n, ans);
            current.deleteCharAt(current.length() - 1);
        }
        if (close < open) {
            current.append(')');
            backtrack(current, open, close + 1, n, ans);
            current.deleteCharAt(current.length() - 1);
        }
    }
}
```

---

## Python

```python
# Approach 1: Brute Force — Generate All + Validate
class Solution:
    def generateParenthesis(self, n: int) -> list[str]:
        ans = []
        self.generate("", n, ans)
        return ans

    def generate(self, current: str, n: int, ans: list[str]) -> None:
        if len(current) == 2 * n:
            if self.isValid(current):
                ans.append(current)
            return
        self.generate(current + "(", n, ans)
        self.generate(current + ")", n, ans)

    def isValid(self, s: str) -> bool:
        balanced = 0
        for ch in s:
            if ch == '(':
                balanced += 1
            else:
                balanced -= 1
            if balanced < 0:
                return False
        return balanced == 0

# Approach 2: Backtracking with Pruning (Best)
class Solution:
    def generateParenthesis(self, n: int) -> list[str]:
        ans = []
        stack = []

        def backtrack(openN: int, closedN: int) -> None:
            if openN == closedN == n:
                ans.append("".join(stack))
                return
            if openN < n:
                stack.append("(")
                backtrack(openN + 1, closedN)
                stack.pop()
            if closedN < openN:
                stack.append(")")
                backtrack(openN, closedN + 1)
                stack.pop()

        backtrack(0, 0)
        return ans
```

---

## C++

```cpp
// Approach 1: Brute Force — Generate All + Validate
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        generate("", n, ans);
        return ans;
    }

    void generate(string current, int n, vector<string>& ans) {
        if ((int)current.length() == 2 * n) {
            if (isValid(current)) ans.push_back(current);
            return;
        }
        generate(current + "(", n, ans);
        generate(current + ")", n, ans);
    }

    bool isValid(string s) {
        int balanced = 0;
        for (char ch : s) {
            if (ch == '(') balanced++;
            else balanced--;
            if (balanced < 0) return false;
        }
        return balanced == 0;
    }
};

// Approach 2: Backtracking with Pruning (Best)
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        string current;
        backtrack(current, 0, 0, n, ans);
        return ans;
    }

    void backtrack(string& current, int open, int close, int n, vector<string>& ans) {
        if ((int)current.length() == 2 * n) {
            ans.push_back(current);
            return;
        }
        if (open < n) {
            current.push_back('(');
            backtrack(current, open + 1, close, n, ans);
            current.pop_back();
        }
        if (close < open) {
            current.push_back(')');
            backtrack(current, open, close + 1, n, ans);
            current.pop_back();
        }
    }
};
```

---

## C

```c
#include <stdbool.h>
#include <stdlib.h>
#include <string.h>

// Approach 1: Brute Force — Generate All + Validate
static bool isValidBF(char* s, int len) {
    int balanced = 0;
    for (int i = 0; i < len; i++) {
        if (s[i] == '(') balanced++;
        else balanced--;
        if (balanced < 0) return false;
    }
    return balanced == 0;
}

static void generateBF(char* current, int pos, int n, char** ans, int* returnSize) {
    if (pos == 2 * n) {
        current[pos] = '\0';
        if (isValidBF(current, pos)) {
            ans[*returnSize] = (char*)malloc((2 * n + 1) * sizeof(char));
            strcpy(ans[*returnSize], current);
            (*returnSize)++;
        }
        return;
    }
    current[pos] = '(';
    generateBF(current, pos + 1, n, ans, returnSize);
    current[pos] = ')';
    generateBF(current, pos + 1, n, ans, returnSize);
}

// Approach 2: Backtracking with Pruning (Best)
static void backtrackOpt(char* current, int pos, int open, int close, int n, char** ans, int* returnSize) {
    if (pos == 2 * n) {
        current[pos] = '\0';
        ans[*returnSize] = (char*)malloc((2 * n + 1) * sizeof(char));
        strcpy(ans[*returnSize], current);
        (*returnSize)++;
        return;
    }
    if (open < n) {
        current[pos] = '(';
        backtrackOpt(current, pos + 1, open + 1, close, n, ans, returnSize);
    }
    if (close < open) {
        current[pos] = ')';
        backtrackOpt(current, pos + 1, open, close + 1, n, ans, returnSize);
    }
}

char** generateParenthesis(int n, int* returnSize) {
    int maxSize = 1 << (2 * n);
    char** ans = (char**)malloc(maxSize * sizeof(char*));
    char* current = (char*)malloc((2 * n + 1) * sizeof(char));
    *returnSize = 0;
    backtrackOpt(current, 0, 0, 0, n, ans, returnSize);
    free(current);
    return ans;
}
```
