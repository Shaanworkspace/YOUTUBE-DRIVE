# LeetCode 2778 - Sum of Squares of Special Elements

**Problem Link:** https://leetcode.com/problems/sum-of-squares-of-special-elements/description

**Companies:** Google, TCS, Wipro, Capgemini

**Approach:** Single pass with 1-based indexing — an element at position i is special when n modulo i equals 0. Square nums of i minus 1 and add to the sum.

**Complexity:** Time O(n), Space O(1).

---

## Java

```java
class Solution {
    public int sumOfSquares(int[] nums) {
        int sum = 0;
        int n = nums.length;
        for (int i = 1; i <= n; i++) {
            if (n % i == 0) {
                int num = nums[i - 1];
                sum += num * num;
            }
        }
        return sum;
    }
}
```

---

## Python

```python
class Solution:
    def sumOfSquares(self, nums: list[int]) -> int:
        n = len(nums)
        total = 0
        for i in range(1, n + 1):
            if n % i == 0:
                total += nums[i - 1] * nums[i - 1]
        return total
```

---

## C++

```cpp
class Solution {
public:
    int sumOfSquares(vector<int>& nums) {
        int sum = 0;
        int n = nums.size();
        for (int i = 1; i <= n; i++) {
            if (n % i == 0) {
                sum += nums[i - 1] * nums[i - 1];
            }
        }
        return sum;
    }
};
```

---

## C

```c
int sumOfSquares(int* nums, int numsSize) {
    int sum = 0;
    int n = numsSize;
    for (int i = 1; i <= n; i++) {
        if (n % i == 0) {
            sum += nums[i - 1] * nums[i - 1];
        }
    }
    return sum;
}
```
