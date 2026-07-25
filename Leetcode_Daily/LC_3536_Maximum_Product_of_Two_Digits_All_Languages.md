# LeetCode 3536 - Maximum Product of Two Digits

## Java

```java
class Solution {

    public int maxProduct(int n) {

        int first = 0;
        int second = 0;

        while (n > 0) {

            int digit = n % 10;

            if (digit >= first) {
                second = first;
                first = digit;
            } else if (digit > second) {
                second = digit;
            }

            n /= 10;
        }

        return first * second;
    }
}
```

---

## Python

```python
class Solution:

    def maxProduct(self, n: int) -> int:

        first = 0
        second = 0

        while n > 0:

            digit = n % 10

            if digit >= first:
                second = first
                first = digit
            elif digit > second:
                second = digit

            n //= 10

        return first * second
```

---

## C++

```cpp
class Solution {
public:

    int maxProduct(int n) {

        int first = 0;
        int second = 0;

        while (n > 0) {

            int digit = n % 10;

            if (digit >= first) {
                second = first;
                first = digit;
            } else if (digit > second) {
                second = digit;
            }

            n /= 10;
        }

        return first * second;
    }
};
```

---

## C

```c
int maxProduct(int n) {

    int first = 0;
    int second = 0;

    while (n > 0) {

        int digit = n % 10;

        if (digit >= first) {
            second = first;
            first = digit;
        } else if (digit > second) {
            second = digit;
        }

        n /= 10;
    }

    return first * second;
}
```