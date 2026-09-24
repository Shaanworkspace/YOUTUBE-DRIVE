# LeetCode 3550 - Smallest Index With Digit Sum Equal to Index

**Problem Link:**
- LeetCode: https://leetcode.com/problems/smallest-index-with-digit-sum-equal-to-index/description

**Approach:** Brute Force — Single Pass Simulation
Traverse the array. For each index `i`, compute the digit sum of `nums[i]` using modulo extraction, compare with `i`, return the first match. Return -1 if none found.

**Complexity:** Time: O(n * d) where d = digits per number | Space: O(1)

---

## Java

```java
class Solution {
    public int smallestIndex(int[] nums) {

        for (int i = 0; i < nums.length; i++) {
            int n = nums[i];
            int sum = 0;

            while (n > 0) {
                sum += n % 10;
                n /= 10;
            }

            if (sum == i)
                return i;
        }

        return -1;
    }
}
```

---

## Python

```python
class Solution:
    def smallestIndex(self, nums: list[int]) -> int:
        for i, n in enumerate(nums):
            total = 0
            while n > 0:
                total += n % 10
                n //= 10

            if total == i:
                return i

        return -1
```

---

## C++

```cpp
class Solution {
public:
    int smallestIndex(vector<int>& nums) {
        for (int i = 0; i < (int)nums.size(); i++) {
            int n = nums[i];
            int sum = 0;

            while (n > 0) {
                sum += n % 10;
                n /= 10;
            }

            if (sum == i)
                return i;
        }

        return -1;
    }
};
```

---

## C

```c
int smallestIndex(int* nums, int numsSize) {
    for (int i = 0; i < numsSize; i++) {
        int n = nums[i];
        int sum = 0;

        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }

        if (sum == i)
            return i;
    }

    return -1;
}
```
