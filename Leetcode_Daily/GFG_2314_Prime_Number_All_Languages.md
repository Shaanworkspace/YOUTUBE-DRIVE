# GFG 2314 - Prime Number

**Problem:** Check if a number is prime or not.
**Link:** https://www.geeksforgeeks.org/problems/prime-number2314
**Approach:** Count all divisors using i * i <= n. If count > 2, the number is not prime. This works because every divisor pair (i, n/i) contributes 2 divisors, except perfect squares which contribute 1.
**Time Complexity:** O(sqrt(n))
**Space Complexity:** O(1)

---

## Java

```java
class Solution {
    static boolean isPrime(int n) {
        if (n == 1) return false;
        int count = 0;
        for (int i = 1; i * i <= n; i++) {
            if (n % i == 0) {
                if (i * i == n) count++;
                else count += 2;
            }
        }
        if (count > 2) return false;
        else return true;
    }
}
```

---

## Python

```python
class Solution:
    def isPrime(self, n):
        if n == 1:
            return False
        count = 0
        i = 1
        while i * i <= n:
            if n % i == 0:
                if i * i == n:
                    count += 1
                else:
                    count += 2
            i += 1
        if count > 2:
            return False
        else:
            return True
```

---

## C++

```cpp
class Solution {
public:
    bool isPrime(int n) {
        if (n == 1) return false;
        int count = 0;
        for (int i = 1; i * i <= n; i++) {
            if (n % i == 0) {
                if (i * i == n) count++;
                else count += 2;
            }
        }
        if (count > 2) return false;
        else return true;
    }
};
```

---

## C

```c
#include <stdbool.h>

bool isPrime(int n) {
    if (n == 1) return false;
    int count = 0;
    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i == n) count++;
            else count += 2;
        }
    }
    if (count > 2) return false;
    else return true;
}
```
