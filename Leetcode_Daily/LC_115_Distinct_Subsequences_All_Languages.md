# LeetCode 115 - Distinct Subsequences

**Problem Link:** https://leetcode.com/problems/distinct-subsequences/

**Companies:** Amazon, Bloomberg, Google, JPMorgan, Oracle, Salesforce, Zoho

---

## Approach: Pick / Skip Pattern with Memoization (Recursion + DP)

Count distinct subsequences of `s` that equal `t` using recursion with memoization. At each position, if characters match, pick (use it) or skip; if no match, only skip.

Time: O(m * n) | Space: O(m * n)

---

## Java

```java
class Solution {
    public int numDistinct(String s, String t) {
        int[][] dp = new int[s.length()][t.length()];
        for (int[] row : dp) {
            java.util.Arrays.fill(row, -1);
        }
        return solve(s, t, 0, 0, dp);
    }

    private int solve(String s, String t, int i, int j, int[][] dp) {
        if (j == t.length()) {
            return 1;
        }
        if (i == s.length()) {
            return 0;
        }
        if (dp[i][j] != -1) {
            return dp[i][j];
        }
        if (s.charAt(i) == t.charAt(j)) {
            int pick = solve(s, t, i + 1, j + 1, dp);
            int skip = solve(s, t, i + 1, j, dp);
            return dp[i][j] = pick + skip;
        }
        int skip = solve(s, t, i + 1, j, dp);
        return dp[i][j] = skip;
    }
}
```

---

## Python

```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        from functools import lru_cache

        @lru_cache(maxsize=None)
        def solve(i: int, j: int) -> int:
            if j == len(t):
                return 1
            if i == len(s):
                return 0
            if s[i] == t[j]:
                return solve(i + 1, j + 1) + solve(i + 1, j)
            return solve(i + 1, j)

        return solve(0, 0)
```

---

## C++

```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        int m = s.size(), n = t.size();
        vector<vector<int>> dp(m, vector<int>(n, -1));
        return solve(s, t, 0, 0, dp);
    }

private:
    int solve(const string& s, const string& t, int i, int j, vector<vector<int>>& dp) {
        if (j == t.size()) return 1;
        if (i == s.size()) return 0;
        if (dp[i][j] != -1) return dp[i][j];
        if (s[i] == t[j]) {
            return dp[i][j] = solve(s, t, i + 1, j + 1, dp) + solve(s, t, i + 1, j, dp);
        }
        return dp[i][j] = solve(s, t, i + 1, j, dp);
    }
};
```

---

## C

```c
int solve(char* s, char* t, int i, int j, int m, int n, int** dp) {
    if (j == n) return 1;
    if (i == m) return 0;
    if (dp[i][j] != -1) return dp[i][j];
    if (s[i] == t[j]) {
        return dp[i][j] = solve(s, t, i + 1, j + 1, m, n, dp) + solve(s, t, i + 1, j, m, n, dp);
    }
    return dp[i][j] = solve(s, t, i + 1, j, m, n, dp);
}

int numDistinct(char* s, char* t) {
    int m = strlen(s), n = strlen(t);
    int** dp = (int**)malloc(m * sizeof(int*));
    for (int i = 0; i < m; i++) {
        dp[i] = (int*)malloc(n * sizeof(int));
        for (int j = 0; j < n; j++) dp[i][j] = -1;
    }
    int result = solve(s, t, 0, 0, m, n, dp);
    for (int i = 0; i < m; i++) free(dp[i]);
    free(dp);
    return result;
}
```
