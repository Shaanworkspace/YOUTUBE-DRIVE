# GeeksforGeeks — LCM of Two Numbers

Problem: https://www.geeksforgeeks.org/problems/lcm-of-two-numbers/1

Optimal approach:
- LCM(a, b) = (a * b) / GCD(a, b)
- GCD computed with the Euclidean algorithm (repeated modulo until one operand is 0).
- Time: O(log(min(a, b)))  |  Space: O(1)

---

## Java

```java
class Solution {
    public int lcm(int a, int b) {
        return (a * b) / gcd(a, b);
    }

    int gcd(int a, int b) {
        while (a != 0 && b != 0) {
            if (a > b) a = a % b;
            else b = b % a;
        }
        if (a == 0) return b;
        else return a;
    }
}
```

---

## Python

```python
class Solution:
    def lcm(self, a, b):
        return (a * b) // self.gcd(a, b)

    def gcd(self, a, b):
        while a != 0 and b != 0:
            if a > b:
                a = a % b
            else:
                b = b % a
        if a == 0:
            return b
        else:
            return a
```

---

## C++

```cpp
class Solution {
public:
    int lcm(int a, int b) {
        return (a * b) / gcd(a, b);
    }

    int gcd(int a, int b) {
        while (a != 0 && b != 0) {
            if (a > b) a = a % b;
            else b = b % a;
        }
        if (a == 0) return b;
        else return a;
    }
};
```

---

## C

```c
int gcd(int a, int b) {
    while (a != 0 && b != 0) {
        if (a > b) a = a % b;
        else b = b % a;
    }
    return (a == 0) ? b : a;
}

int lcm(int a, int b) {
    return (a * b) / gcd(a, b);
}
```
