# LeetCode 2567 - Minimum Score by Changing Two Elements

Problem: https://leetcode.com/problems/minimum-score-by-changing-two-elements/

You are given an integer array `nums`. The low score is the minimum absolute difference between any two integers, the high score is the maximum absolute difference, and the score is low + high. You may change at most two elements. Return the minimum possible score. Sorting lets us test the three ways to remove two extremes (two smallest, one from each end, two largest).

## Java

```java
class Solution {
    public int minimizeSum(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        int case1 = nums[n - 1] - nums[2];
        int case2 = nums[n - 2] - nums[1];
        int case3 = nums[n - 3] - nums[0];
        return Math.min(case1, Math.min(case2, case3));
    }
}
```

---

## Python

```python
from typing import List

class Solution:
    def minimizeSum(self, nums: List[int]) -> int:
        nums.sort()
        n = len(nums)
        case1 = nums[n - 1] - nums[2]
        case2 = nums[n - 2] - nums[1]
        case3 = nums[n - 3] - nums[0]
        return min(case1, case2, case3)
```

---

## C++

```cpp
class Solution {
public:
    int minimizeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = (int)nums.size();
        int case1 = nums[n - 1] - nums[2];
        int case2 = nums[n - 2] - nums[1];
        int case3 = nums[n - 3] - nums[0];
        return min(case1, min(case2, case3));
    }
};
```

---

## C

```c
#include <stdlib.h>

static int cmp(const void* a, const void* b) {
    return (*(const int*)a - *(const int*)b);
}

int minimizeSum(int* nums, int numsSize) {
    qsort(nums, numsSize, sizeof(int), cmp);
    int n = numsSize;
    int case1 = nums[n - 1] - nums[2];
    int case2 = nums[n - 2] - nums[1];
    int case3 = nums[n - 3] - nums[0];
    int m = case1 < case2 ? case1 : case2;
    return m < case3 ? m : case3;
}
```
