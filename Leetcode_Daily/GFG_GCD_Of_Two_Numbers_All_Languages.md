# GFG - GCD of Two Numbers

Problem: https://www.geeksforgeeks.org/problems/gcd-of-two-numbers3459/1

The GCD (Greatest Common Divisor) or HCF (Highest Common Factor) of two numbers
is the largest number that divides both of them. This uses the Euclidean
algorithm by repeated modulo (optimal O(log(min(a,b))) time, O(1) space).

---

## Java

```java
class Solution {
    public static int gcd(int a, int b) {
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
    @staticmethod
    def gcd(a, b):
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
    static int gcd(int a, int b) {
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
    if (a == 0) return b;
    else return a;
}
```

---

Complexity:
- Time:  O(log(min(a, b)))  (Euclidean modulo)
- Space: O(1)
