# LeetCode 3871 - Count Commas in Range II

**Problem Link:** https://leetcode.com/problems/count-commas-in-range-ii/description

**Approach:** Mathematical — Count numbers with at least one comma in [1, n] by summing (n - start + 1) for each power of 1000 (1000, 1000000, 1000000000, ...).

**Time Complexity:** O(log_{1000} n) — one iteration per thousand separator
**Space Complexity:** O(1)

---

## Java

```java
class Solution {
    public long countCommas(long n) {
        long ans = 0;
        for (long start = 1000; start <= n; start *= 1000)
            ans += n - start + 1;
        return ans;
    }
}
```

---

## Python

```python
class Solution:
    def countCommas(self, n: int) -> int:
        ans = 0
        start = 1000
        while start <= n:
            ans += n - start + 1
            start *= 1000
        return ans
```

---

## C++

```cpp
class Solution {
public:
    long long countCommas(long long n) {
        long long ans = 0;
        for (long long start = 1000; start <= n; start *= 1000)
            ans += n - start + 1;
        return ans;
    }
};
```

---

## C

```c
long long countCommas(long long n) {
    long long ans = 0;
    for (long long start = 1000; start <= n; start *= 1000)
        ans += n - start + 1;
    return ans;
}
```
