# LeetCode 1927 - Sum Game

Problem: https://leetcode.com/problems/sum-game/
A two-player game on a string of digits and '?'. Alice and Bob take turns; the winner is
decided by whether the final sum of the left half can equal the right half. Optimal play
reduces to a simple math check on digit sums and the count of '?'.

---

## Java

```java
class Solution {
    public boolean sumGame(String num) {
        int n = num.length();
        int leftSum = 0;
        int rightSum = 0;
        int leftQ = 0;
        int rightQ = 0;
        // First half
        for (int i = 0; i < n / 2; i++) {
            if (num.charAt(i) == '?') {
                leftQ++;
            } else {
                leftSum += num.charAt(i) - '0';
            }
        }
        // Second half
        for (int i = n / 2; i < n; i++) {
            if (num.charAt(i) == '?') {
                rightQ++;
            } else {
                rightSum += num.charAt(i) - '0';
            }
        }
        int sumDiff = leftSum - rightSum;
        int qDiff = leftQ - rightQ;
        if (qDiff == 0) {
            if (sumDiff == 0) {
                return false;
            } else {
                return true;
            }
        } else if ((leftQ + rightQ) % 2 != 0) {
            return true;
        } else {
            int maxDifference = -9 * qDiff / 2;
            if (sumDiff == maxDifference) {
                return false;
            } else {
                return true;
            }
        }
    }
}
```

---

## Python

```python
class Solution:
    def sumGame(self, num: str) -> bool:
        n = len(num)
        left_sum = 0
        right_sum = 0
        left_q = 0
        right_q = 0
        for i in range(n // 2):
            if num[i] == '?':
                left_q += 1
            else:
                left_sum += int(num[i])
        for i in range(n // 2, n):
            if num[i] == '?':
                right_q += 1
            else:
                right_sum += int(num[i])
        sum_diff = left_sum - right_sum
        q_diff = left_q - right_q
        if q_diff == 0:
            return sum_diff != 0
        elif (left_q + right_q) % 2 != 0:
            return True
        else:
            max_difference = -9 * q_diff // 2
            return sum_diff != max_difference
```

---

## C++

```cpp
class Solution {
  public:
    bool sumGame(string num) {
        int n = num.length();
        int leftSum = 0;
        int rightSum = 0;
        int leftQ = 0;
        int rightQ = 0;
        for (int i = 0; i < n / 2; i++) {
            if (num[i] == '?') {
                leftQ++;
            } else {
                leftSum += num[i] - '0';
            }
        }
        for (int i = n / 2; i < n; i++) {
            if (num[i] == '?') {
                rightQ++;
            } else {
                rightSum += num[i] - '0';
            }
        }
        int sumDiff = leftSum - rightSum;
        int qDiff = leftQ - rightQ;
        if (qDiff == 0) {
            return sumDiff != 0;
        } else if ((leftQ + rightQ) % 2 != 0) {
            return true;
        } else {
            int maxDifference = -9 * qDiff / 2;
            return sumDiff != maxDifference;
        }
    }
};
```

---

## C

```c
#include <stdbool.h>
#include <string.h>

bool sumGame(char* num) {
    int n = (int)strlen(num);
    int leftSum = 0;
    int rightSum = 0;
    int leftQ = 0;
    int rightQ = 0;
    for (int i = 0; i < n / 2; i++) {
        if (num[i] == '?') {
            leftQ++;
        } else {
            leftSum += num[i] - '0';
        }
    }
    for (int i = n / 2; i < n; i++) {
        if (num[i] == '?') {
            rightQ++;
        } else {
            rightSum += num[i] - '0';
        }
    }
    int sumDiff = leftSum - rightSum;
    int qDiff = leftQ - rightQ;
    if (qDiff == 0) {
        return sumDiff != 0;
    } else if ((leftQ + rightQ) % 2 != 0) {
        return true;
    } else {
        int maxDifference = -9 * qDiff / 2;
        return sumDiff != maxDifference;
    }
}
```
