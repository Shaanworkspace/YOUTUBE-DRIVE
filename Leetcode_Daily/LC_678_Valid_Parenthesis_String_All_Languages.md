# LeetCode 678 - Valid Parenthesis String

**Problem Link:** https://leetcode.com/problems/valid-parenthesis-string/description

**Companies:** Amazon, Google, Microsoft, Meta, Bloomberg, Apple, Samsung, Goldman Sachs

**Approach:** Recursion with Memoization (Top-Down DP). State is index plus balance. Star tries open, close, and empty. Memo caches visited states to fix TLE.
**Time:** O(n squared) | **Space:** O(n squared)

---

## Java

```java
class Solution {

    Boolean[][] memo;

    public boolean checkValidString(String s) {

        // index = current position
        // balance can be at most s.length()
        memo = new Boolean[s.length()][s.length() + 1];

        return solve(s, 0, 0);
    }

    private boolean solve(String s, int index, int balance) {

        // Invalid path
        if (balance < 0) {
            return false;
        }

        // All characters are processed
        if (index == s.length()) {
            return balance == 0;
        }

        // Already calculated
        if (memo[index][balance] != null) {
            return memo[index][balance];
        }

        char currentCharacter = s.charAt(index);

        boolean result;

        // '('
        if (currentCharacter == '(') {

            result = solve(s, index + 1, balance + 1);
        }

        // ')'
        else if (currentCharacter == ')') {

            result = solve(s, index + 1, balance - 1);
        }

        // '*'
        else {

            // '*' as '('
            boolean useAsOpening =
                solve(s, index + 1, balance + 1);

            // '*' as ')'
            boolean useAsClosing =
                solve(s, index + 1, balance - 1);

            // '*' as empty
            boolean useAsEmpty =
                solve(s, index + 1, balance);

            result = useAsOpening ||
                     useAsClosing ||
                     useAsEmpty;
        }

        // Store answer for this state
        memo[index][balance] = result;

        return result;
    }
}
```

---

## Python

```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        n = len(s)
        memo = [[None] * (n + 1) for _ in range(n)]

        def solve(index: int, balance: int) -> bool:
            if balance < 0:
                return False
            if index == n:
                return balance == 0
            if memo[index][balance] is not None:
                return memo[index][balance]
            ch = s[index]
            if ch == '(':
                result = solve(index + 1, balance + 1)
            elif ch == ')':
                result = solve(index + 1, balance - 1)
            else:
                use_as_opening = solve(index + 1, balance + 1)
                use_as_closing = solve(index + 1, balance - 1)
                use_as_empty = solve(index + 1, balance)
                result = use_as_opening or use_as_closing or use_as_empty
            memo[index][balance] = result
            return result

        return solve(0, 0)
```

---

## C++

```cpp
class Solution {
public:
    vector<vector<int>> memo;
    bool checkValidString(string s) {
        int n = s.size();
        memo.assign(n, vector<int>(n + 1, -1));
        return solve(s, 0, 0);
    }
private:
    bool solve(const string& s, int index, int balance) {
        if (balance < 0) return false;
        if (index == (int)s.size()) return balance == 0;
        if (memo[index][balance] != -1) return memo[index][balance];
        char c = s[index];
        bool result = false;
        if (c == '(') {
            result = solve(s, index + 1, balance + 1);
        } else if (c == ')') {
            result = solve(s, index + 1, balance - 1);
        } else {
            bool useAsOpening = solve(s, index + 1, balance + 1);
            bool useAsClosing = solve(s, index + 1, balance - 1);
            bool useAsEmpty = solve(s, index + 1, balance);
            result = useAsOpening || useAsClosing || useAsEmpty;
        }
        memo[index][balance] = result;
        return result;
    }
};
```

---

## C

```c
bool solve678(char* s, int index, int balance, int n, int** memo) {
    if (balance < 0) return false;
    if (index == n) return balance == 0;
    if (memo[index][balance] != -1) return memo[index][balance];
    char c = s[index];
    bool result = false;
    if (c == '(') {
        result = solve678(s, index + 1, balance + 1, n, memo);
    } else if (c == ')') {
        result = solve678(s, index + 1, balance - 1, n, memo);
    } else {
        bool useAsOpening = solve678(s, index + 1, balance + 1, n, memo);
        bool useAsClosing = solve678(s, index + 1, balance - 1, n, memo);
        bool useAsEmpty = solve678(s, index + 1, balance, n, memo);
        result = useAsOpening || useAsClosing || useAsEmpty;
    }
    memo[index][balance] = result;
    return result;
}

bool checkValidString(char* s) {
    int n = strlen(s);
    if (n == 0) return true;
    int** memo = (int**)malloc(n * sizeof(int*));
    for (int i = 0; i < n; i++) {
        memo[i] = (int*)malloc((n + 1) * sizeof(int));
        for (int j = 0; j <= n; j++) memo[i][j] = -1;
    }
    bool ans = solve678(s, 0, 0, n, memo);
    for (int i = 0; i < n; i++) free(memo[i]);
    free(memo);
    return ans;
}
```
