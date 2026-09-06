# LeetCode 1563 - Stone Game V

**Problem Link:** https://leetcode.com/problems/stone-game-v/

**Approach:** Recursion + Memoization (Fixed 4-Step Memorization DP)

---

## The Fixed 4 Steps of Memorization DP

1. Identify the changing variables (left, right)
2. Create the 2D DP table sized n x n
3. Fill with -1
4. Check DP before every call, save result into DP before returning

---

## Java

```java
class Solution {
    public int stoneGameV(int[] stoneValue) {
        int n = stoneValue.length;
        int[] prefix = new int[n + 1];
        for (int i = 0; i < n; i++) {
            prefix[i + 1] = prefix[i] + stoneValue[i];
        }
        int[][] dp = new int[n][n];
        for (int[] row : dp) {
            java.util.Arrays.fill(row, -1);
        }
        return solve(stoneValue, prefix, 0, n - 1, dp);
    }

    private int solve(int[] stone, int[] prefix, int left, int right, int[][] dp) {
        if (left == right) return 0;
        if (dp[left][right] != -1) return dp[left][right];

        int best = 0;
        for (int k = left; k < right; k++) {
            int leftSum = prefix[k + 1] - prefix[left];
            int rightSum = prefix[right + 1] - prefix[k + 1];

            if (leftSum > rightSum) {
                best = Math.max(best, rightSum + solve(stone, prefix, k + 1, right, dp));
            } else if (rightSum > leftSum) {
                best = Math.max(best, leftSum + solve(stone, prefix, left, k, dp));
            } else {
                best = Math.max(best, leftSum + Math.max(
                    solve(stone, prefix, left, k, dp),
                    solve(stone, prefix, k + 1, right, dp)
                ));
            }
        }
        return dp[left][right] = best;
    }
}
```

---

## Python

```python
class Solution:
    def stoneGameV(self, stoneValue: list[int]) -> int:
        n = len(stoneValue)
        prefix = [0] * (n + 1)
        for i in range(n):
            prefix[i + 1] = prefix[i] + stoneValue[i]

        dp = [[-1] * n for _ in range(n)]

        def solve(left: int, right: int) -> int:
            if left == right:
                return 0
            if dp[left][right] != -1:
                return dp[left][right]

            best = 0
            for k in range(left, right):
                left_sum = prefix[k + 1] - prefix[left]
                right_sum = prefix[right + 1] - prefix[k + 1]

                if left_sum > right_sum:
                    best = max(best, right_sum + solve(k + 1, right))
                elif right_sum > left_sum:
                    best = max(best, left_sum + solve(left, k))
                else:
                    best = max(best, left_sum + max(solve(left, k), solve(k + 1, right)))

            dp[left][right] = best
            return best

        return solve(0, n - 1)
```

---

## C++

```cpp
class Solution {
public:
    int stoneGameV(vector<int>& stoneValue) {
        int n = stoneValue.size();
        vector<int> prefix(n + 1, 0);
        for (int i = 0; i < n; i++) {
            prefix[i + 1] = prefix[i] + stoneValue[i];
        }
        vector<vector<int>> dp(n, vector<int>(n, -1));
        return solve(stoneValue, prefix, 0, n - 1, dp);
    }

private:
    int solve(vector<int>& stone, vector<int>& prefix, int left, int right, vector<vector<int>>& dp) {
        if (left == right) return 0;
        if (dp[left][right] != -1) return dp[left][right];

        int best = 0;
        for (int k = left; k < right; k++) {
            int leftSum = prefix[k + 1] - prefix[left];
            int rightSum = prefix[right + 1] - prefix[k + 1];

            if (leftSum > rightSum) {
                best = max(best, rightSum + solve(stone, prefix, k + 1, right, dp));
            } else if (rightSum > leftSum) {
                best = max(best, leftSum + solve(stone, prefix, left, k, dp));
            } else {
                best = max(best, leftSum + max(
                    solve(stone, prefix, left, k, dp),
                    solve(stone, prefix, k + 1, right, dp)
                ));
            }
        }
        return dp[left][right] = best;
    }
};
```

---

## C

```c
int solve(int* stone, int* prefix, int left, int right, int n, int** dp) {
    if (left == right) return 0;
    if (dp[left][right] != -1) return dp[left][right];

    int best = 0;
    for (int k = left; k < right; k++) {
        int leftSum = prefix[k + 1] - prefix[left];
        int rightSum = prefix[right + 1] - prefix[k + 1];

        if (leftSum > rightSum) {
            int val = rightSum + solve(stone, prefix, k + 1, right, n, dp);
            if (val > best) best = val;
        } else if (rightSum > leftSum) {
            int val = leftSum + solve(stone, prefix, left, k, n, dp);
            if (val > best) best = val;
        } else {
            int v1 = solve(stone, prefix, left, k, n, dp);
            int v2 = solve(stone, prefix, k + 1, right, n, dp);
            int val = leftSum + (v1 > v2 ? v1 : v2);
            if (val > best) best = val;
        }
    }
    return dp[left][right] = best;
}

int stoneGameV(int* stoneValue, int stoneValueSize) {
    int n = stoneValueSize;
    int* prefix = (int*)calloc(n + 1, sizeof(int));
    for (int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + stoneValue[i];

    int** dp = (int**)malloc(n * sizeof(int*));
    for (int i = 0; i < n; i++) {
        dp[i] = (int*)malloc(n * sizeof(int));
        for (int j = 0; j < n; j++) dp[i][j] = -1;
    }

    int result = solve(stoneValue, prefix, 0, n - 1, n, dp);

    for (int i = 0; i < n; i++) free(dp[i]);
    free(dp);
    free(prefix);
    return result;
}
```
