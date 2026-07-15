# LeetCode 3658 - GCD of Odd and Even Sums

## Java

```java
class Solution {

    public int gcdOfOddEvenSums(int n) {

        int sumOdd = 0;
        int sumEven = 0;

        for (int i = 1; i <= n; i++) {
            sumOdd += (2 * i - 1);
            sumEven += (2 * i);
        }

        for (int d = Math.min(sumOdd, sumEven); d >= 1; d--) {
            if (sumOdd % d == 0 && sumEven % d == 0) {
                return d;
            }
        }

        return 1;
    }
}
```

---

## Python

```python
class Solution:
    def gcdOfOddEvenSums(self, n: int) -> int:

        sum_odd = 0
        sum_even = 0

        for i in range(1, n + 1):
            sum_odd += 2 * i - 1
            sum_even += 2 * i

        for d in range(min(sum_odd, sum_even), 0, -1):
            if sum_odd % d == 0 and sum_even % d == 0:
                return d

        return 1
```

---

## C++

```cpp
class Solution {
public:
    int gcdOfOddEvenSums(int n) {

        int sumOdd = 0;
        int sumEven = 0;

        for (int i = 1; i <= n; i++) {
            sumOdd += (2 * i - 1);
            sumEven += (2 * i);
        }

        for (int d = min(sumOdd, sumEven); d >= 1; d--) {
            if (sumOdd % d == 0 && sumEven % d == 0) {
                return d;
            }
        }

        return 1;
    }
};
```

---

## C

```c
int gcdOfOddEvenSums(int n) {

    int sumOdd = 0;
    int sumEven = 0;

    for (int i = 1; i <= n; i++) {
        sumOdd += (2 * i - 1);
        sumEven += (2 * i);
    }

    int limit = (sumOdd < sumEven) ? sumOdd : sumEven;

    for (int d = limit; d >= 1; d--) {
        if (sumOdd % d == 0 && sumEven % d == 0) {
            return d;
        }
    }

    return 1;
}
```