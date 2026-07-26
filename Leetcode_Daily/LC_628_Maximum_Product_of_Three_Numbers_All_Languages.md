# LeetCode 628 - Maximum Product of Three Numbers

## Java

```java
import java.util.Arrays;

class Solution {

    public int maximumProduct(int[] nums) {

        Arrays.sort(nums);

        int n = nums.length;

        return Math.max(
            nums[n - 1] * nums[n - 2] * nums[n - 3],
            nums[0] * nums[1] * nums[n - 1]
        );
    }
}
```

---

## Python

```python
class Solution:

    def maximumProduct(self, nums: list[int]) -> int:

        nums.sort()

        n = len(nums)

        return max(
            nums[n - 1] * nums[n - 2] * nums[n - 3],
            nums[0] * nums[1] * nums[n - 1]
        )
```

---

## C++

```cpp
class Solution {
public:

    int maximumProduct(vector<int>& nums) {

        sort(nums.begin(), nums.end());

        int n = nums.size();

        return max(
            nums[n - 1] * nums[n - 2] * nums[n - 3],
            nums[0] * nums[1] * nums[n - 1]
        );
    }
};
```

---

## C

```c
#include <stdlib.h>

int compare(const void* a, const void* b) {
    return (*(int*)a - *(int*)b);
}

int maximumProduct(int* nums, int numsSize) {

    qsort(nums, numsSize, sizeof(int), compare);

    return ((nums[numsSize - 1] * nums[numsSize - 2] * nums[numsSize - 3]) >
            (nums[0] * nums[1] * nums[numsSize - 1]))
        ? (nums[numsSize - 1] * nums[numsSize - 2] * nums[numsSize - 3])
        : (nums[0] * nums[1] * nums[numsSize - 1]);
}
```