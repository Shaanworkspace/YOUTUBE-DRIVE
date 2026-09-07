# LeetCode 940 - Distinct Subsequences II

**Problem Link:** https://leetcode.com/problems/distinct-subsequences-ii/

**Companies:** Google, Amazon

**Difficulty:** Hard

**Approach:** Dynamic Programming — count distinct subsequences ending with each character, update using previous total to avoid duplicates.

**Time Complexity:** O(n * 26) | **Space Complexity:** O(26)

---

## Java

```java
class Solution {
    public int distinctSubseqII(String s) {
        int MOD = 1_000_000_007;
        int total = 0;
        int[] end = new int[26];

        for (char c : s.toCharArray()) {
            int index = c - 'a';
            int oldTotal = total;
            int newSubsequences = (oldTotal + 1 - end[index] + MOD) % MOD;
            total = (total + newSubsequences) % MOD;
            end[index] = (end[index] + newSubsequences) % MOD;
        }

        return total;
    }
}
```

---

## Python

```python
class Solution:
    def distinctSubseqII(self, s: str) -> int:
        MOD = 10**9 + 7
        total = 0
        end = [0] * 26

        for c in s:
            index = ord(c) - ord('a')
            old_total = total
            new_subsequences = (old_total + 1 - end[index]) % MOD
            total = (total + new_subsequences) % MOD
            end[index] = (end[index] + new_subsequences) % MOD

        return total
```

---

## C++

```cpp
class Solution {
public:
    int distinctSubseqII(string s) {
        const int MOD = 1e9 + 7;
        int total = 0;
        int end[26] = {0};

        for (char c : s) {
            int index = c - 'a';
            int oldTotal = total;
            int newSubsequences = (oldTotal + 1 - end[index] + MOD) % MOD;
            total = (total + newSubsequences) % MOD;
            end[index] = (end[index] + newSubsequences) % MOD;
        }

        return total;
    }
};
```

---

## C

```c
int distinctSubseqII(char* s) {
    int MOD = 1000000007;
    int total = 0;
    int end[26] = {0};
    int len = strlen(s);

    for (int i = 0; i < len; i++) {
        int index = s[i] - 'a';
        int oldTotal = total;
        int newSubsequences = (int)(((long long)oldTotal + 1 - end[index] + MOD) % MOD);
        total = (int)(((long long)total + newSubsequences) % MOD);
        end[index] = (int)(((long long)end[index] + newSubsequences) % MOD);
    }

    return total;
}
```
