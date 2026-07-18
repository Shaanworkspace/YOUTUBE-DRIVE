# LeetCode 1979 - Find Greatest Common Divisor of Array

## Java

```java
class Solution {

    public int findGCD(int[] nums) {

        int smallest = Integer.MAX_VALUE;
        int largest = Integer.MIN_VALUE;

        for (int num : nums) {
            smallest = Math.min(smallest, num);
            largest = Math.max(largest, num);
        }

        return gcd(smallest, largest);
    }

    private int gcd(int num1, int num2) {

        for (int i = Math.min(num1, num2); i >= 1; i--) {
            if (num1 % i == 0 && num2 % i == 0) {
                return i;
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

    def findGCD(self, nums: list[int]) -> int:

        smallest = min(nums)
        largest = max(nums)

        return self.gcd(smallest, largest)

    def gcd(self, num1: int, num2: int) -> int:

        for i in range(min(num1, num2), 0, -1):
            if num1 % i == 0 and num2 % i == 0:
                return i

        return 1
```

---

## C++

```cpp
class Solution {
public:

    int findGCD(vector<int>& nums) {

        int smallest = INT_MAX;
        int largest = INT_MIN;

        for (int num : nums) {
            smallest = min(smallest, num);
            largest = max(largest, num);
        }

        return gcd(smallest, largest);
    }

    int gcd(int num1, int num2) {

        for (int i = min(num1, num2); i >= 1; i--) {
            if (num1 % i == 0 && num2 % i == 0) {
                return i;
            }
        }

        return 1;
    }
};
```

---

## C

```c
int gcd(int num1, int num2) {

    int limit = (num1 < num2) ? num1 : num2;

    for (int i = limit; i >= 1; i--) {
        if (num1 % i == 0 && num2 % i == 0) {
            return i;
        }
    }

    return 1;
}

int findGCD(int* nums, int numsSize) {

    int smallest = nums[0];
    int largest = nums[0];

    for (int i = 1; i < numsSize; i++) {
        if (nums[i] < smallest)
            smallest = nums[i];

        if (nums[i] > largest)
            largest = nums[i];
    }

    return gcd(smallest, largest);
}
```