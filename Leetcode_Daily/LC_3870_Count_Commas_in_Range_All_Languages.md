# LeetCode 3870 - Count Commas in Range

**Problem Link:** https://leetcode.com/problems/count-commas-in-range/description

**Approach:** Brain Teaser — O(1) time, O(1) space. Numbers 1-999 have zero commas. For n >= 1000, every number from 1000 to n contributes exactly one comma (since n <= 10^5, we never hit the second comma threshold at 1,000,000). Answer = max(0, n - 999).

---

## Java

```java
class Solution {
    public int countCommas(int n) {
        if (n <= 999) return 0;
        return n - 999;
    }
}
```

---

## Python

```python
class Solution:
    def countCommas(self, n: int) -> int:
        return max(0, n - 999)
```

---

## C++

```cpp
class Solution {
public:
    int countCommas(int n) {
        return max(0, n - 999);
    }
};
```

---

## C

```c
int countCommas(int n) {
    if (n <= 999) return 0;
    return n - 999;
}
```
