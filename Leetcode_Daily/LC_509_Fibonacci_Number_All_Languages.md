# LeetCode 509 - Fibonacci Number

**Problem Link:** https://leetcode.com/problems/fibonacci-number/description/

**Approach:** Top-down Dynamic Programming (Memoization) — store computed Fibonacci values in a DP array to avoid redundant recursive calls.

**Complexity:**
- Time: O(n)
- Space: O(n)

---

## Java

```java
import java.util.Arrays;

class Solution {
    public int fib(int n) {
        int[] dp = new int[n+1];
        Arrays.fill(dp,-1);
        return fun(n,dp);
    }
    int fun(int n,int[] dp){
        // base case
        if(n==0) return 0;
        if(n==1) return 1;

        if(dp[n] !=-1) return dp[n];
       // recursive call
       int oneless = fun(n-1,dp);
       int twoless = fun(n-2,dp);
       return dp[n] = oneless+twoless;
    }
}
```

---

## Python

```python
class Solution:
    def fib(self, n: int) -> int:
        dp = [-1] * (n + 1)
        return self.fun(n, dp)
    
    def fun(self, n: int, dp: list) -> int:
        if n == 0:
            return 0
        if n == 1:
            return 1
        if dp[n] != -1:
            return dp[n]
        oneless = self.fun(n - 1, dp)
        twoless = self.fun(n - 2, dp)
        dp[n] = oneless + twoless
        return dp[n]
```

---

## C++

```cpp
class Solution {
public:
    int fib(int n) {
        vector<int> dp(n + 1, -1);
        return fun(n, dp);
    }
    int fun(int n, vector<int>& dp) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        if (dp[n] != -1) return dp[n];
        int oneless = fun(n - 1, dp);
        int twoless = fun(n - 2, dp);
        return dp[n] = oneless + twoless;
    }
};
```

---

## C

```c
#include <stdlib.h>

int fun(int n, int* dp) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    if (dp[n] != -1) return dp[n];
    int oneless = fun(n - 1, dp);
    int twoless = fun(n - 2, dp);
    dp[n] = oneless + twoless;
    return dp[n];
}

int fib(int n) {
    int* dp = (int*)malloc((n + 1) * sizeof(int));
    for (int i = 0; i <= n; i++) dp[i] = -1;
    int result = fun(n, dp);
    free(dp);
    return result;
}
```
