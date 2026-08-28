# GeeksforGeeks — Armstrong Numbers

Problem: https://www.geeksforgeeks.org/problems/armstrong-numbers2727

Given an integer `n`, return `true` if `n` is an Armstrong number, else `false`.
An Armstrong number (narcissistic number) equals the sum of its own digits each
raised to the power of the digit count (e.g. 153 = 1³ + 5³ + 3³).

---

## Java
```java
class Solution {
    static boolean armstrongNumber(int n) {
        int countNum = 0;
        int temp = n;
        while(temp>0){
            countNum++;
            temp/=10;
        }


        temp = n;
        int sum =0;

        while(temp>0){
            int ele = temp%10;
            sum+=Math.pow(ele,countNum);
            temp/=10;
        }

        return sum==n;

    }
}
```

---

## Python
```python
class Solution:
    @staticmethod
    def armstrongNumber(n: int) -> bool:
        temp = n
        count_num = 0
        while temp > 0:
            count_num += 1
            temp //= 10
        temp = n
        total = 0
        while temp > 0:
            ele = temp % 10
            total += ele ** count_num
            temp //= 10
        return total == n
```

---

## C++
```cpp
class Solution {
  public:
    static bool armstrongNumber(int n) {
        int temp = n, countNum = 0;
        while (temp > 0) {
            countNum++;
            temp /= 10;
        }
        temp = n;
        int sum = 0;
        while (temp > 0) {
            int ele = temp % 10;
            int p = 1;
            for (int i = 0; i < countNum; i++) p *= ele;
            sum += p;
            temp /= 10;
        }
        return sum == n;
    }
};
```

---

## C
```c
#include <math.h>

int armstrongNumber(int n) {
    int temp = n, countNum = 0;
    while (temp > 0) {
        countNum++;
        temp /= 10;
    }
    temp = n;
    int sum = 0;
    while (temp > 0) {
        int ele = temp % 10;
        sum += (int)pow(ele, countNum);
        temp /= 10;
    }
    return sum == n;
}
```
