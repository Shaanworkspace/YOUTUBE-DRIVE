# Digital Root - GeeksforGeeks

**Problem Link:** https://www.geeksforgeeks.org/problems/digital-root/1

**Approach:** Mathematical Formula (Modulo 9)
- Digital root of a number is n % 9
- Special case: if n % 9 == 0 and n != 0, return 9
- Special case: if n == 0, return 0

**Brute Force:** repeatedly sum digits until single digit — O(log n) time
**Optimized:** modulo 9 formula — O(1) time, O(1) space

---

## Java

```java
class Solution {
    public int digitalRoot(int n) {
        if (n == 0) return 0;
        if (n % 9 == 0) return 9;
        return (n % 9);
    }
}
```

---

## Python

```python
class Solution:
    def digitalRoot(self, n):
        if n == 0:
            return 0
        if n % 9 == 0:
            return 9
        return n % 9
```

---

## C++

```cpp
class Solution {
  public:
    int digitalRoot(int n) {
        if (n == 0) return 0;
        if (n % 9 == 0) return 9;
        return n % 9;
    }
};
```

---

## C

```c
int digitalRoot(int n) {
    if (n == 0) return 0;
    if (n % 9 == 0) return 9;
    return n % 9;
}
```
