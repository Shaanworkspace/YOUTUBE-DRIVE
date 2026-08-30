# LeetCode 2091 - Removing Minimum and Maximum From Array

Problem: https://leetcode.com/problems/removing-minimum-and-maximum-from-array/

Given a 0-indexed array of **distinct** integers `nums`, your goal is to remove BOTH the
minimum and the maximum element using the fewest deletions, where a single deletion removes
either the front OR the back of the array. Return the minimum number of deletions.

---

## Approach (Greedy, O(n))

1. Find the index of the minimum element (`minIdx`) and the maximum element (`maxIdx`) in a
   single pass.
2. Let `left = min(minIdx, maxIdx)` and `right = max(minIdx, maxIdx)`. These bound the
   smallest window that contains both extremes.
3. There are only three ways to delete both elements:
   - **Delete from the front only**: remove everything up to `right` → `right + 1` deletions.
   - **Delete from the back only**: remove everything from `left` onward → `n - left` deletions.
   - **Delete one from each end**: remove front up to `left` AND back from `right` onward →
     `(left + 1) + (n - right)` deletions.
4. The answer is `min(front, back, both)`.

Time: **O(n)** — one pass to locate min/max. Space: **O(1)**.

---

## Java

```java
class Solution {
    public int minimumDeletions(int[] nums) {
        int n = nums.length;

        int minIdx = 0;
        int maxIdx = 0;
        for (int i = 0; i < n; i++) {
            if (nums[i] < nums[minIdx])
                minIdx = i;
            if (nums[i] > nums[maxIdx])
                maxIdx = i;
        }

        int left = Math.min(minIdx, maxIdx);
        int right = Math.max(minIdx, maxIdx);

        int front = right + 1;
        int back = n - left;
        int both = (left + 1) + (n - right);

        return Math.min(front, Math.min(back, both));
    }
}
```

---

## Python

```python
from typing import List

class Solution:
    def minimumDeletions(self, nums: List[int]) -> int:
        n = len(nums)

        min_idx = 0
        max_idx = 0
        for i in range(n):
            if nums[i] < nums[min_idx]:
                min_idx = i
            if nums[i] > nums[max_idx]:
                max_idx = i

        left = min(min_idx, max_idx)
        right = max(min_idx, max_idx)

        front = right + 1
        back = n - left
        both = (left + 1) + (n - right)

        return min(front, min(back, both))
```

---

## C++

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int minimumDeletions(vector<int>& nums) {
        int n = nums.size();

        int minIdx = 0;
        int maxIdx = 0;
        for (int i = 0; i < n; i++) {
            if (nums[i] < nums[minIdx])
                minIdx = i;
            if (nums[i] > nums[maxIdx])
                maxIdx = i;
        }

        int left = min(minIdx, maxIdx);
        int right = max(minIdx, maxIdx);

        int front = right + 1;
        int back = n - left;
        int both = (left + 1) + (n - right);

        return min({front, back, both});
    }
};
```

---

## C

```c
int minimumDeletions(int* nums, int numsSize) {
    int minIdx = 0;
    int maxIdx = 0;
    for (int i = 0; i < numsSize; i++) {
        if (nums[i] < nums[minIdx])
            minIdx = i;
        if (nums[i] > nums[maxIdx])
            maxIdx = i;
    }

    int left = (minIdx < maxIdx) ? minIdx : maxIdx;
    int right = (minIdx > maxIdx) ? minIdx : maxIdx;

    int front = right + 1;
    int back = numsSize - left;
    int both = (left + 1) + (numsSize - right);

    int m = (front < back) ? front : back;
    return (m < both) ? m : both;
}
```
