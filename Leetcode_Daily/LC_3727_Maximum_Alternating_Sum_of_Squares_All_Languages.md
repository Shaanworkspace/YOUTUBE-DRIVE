# LeetCode 3727 - Maximum Alternating Sum of Squares

**Problem Link:** https://leetcode.com/problems/maximum-alternating-sum-of-squares/

**Approach:** Square and Sort Greedy
Square every element (sign disappears), sort ascending, subtract the smallest
n / 2 squares, add the remaining squares. Largest squares land on even
(positive) indices, smallest on odd (negative) indices.

Time: O(n log n) | Space: O(n)

---

## Java

```java
import java.util.Arrays;

class Solution {
    public long maxAlternatingSum(int[] nums) {
        int n = nums.length;
        long[] squares = new long[n];

        // Step 1: Calculate the square of each number
        for (int i = 0; i < n; i++) {
            squares[i] = (long) nums[i] * nums[i];
        }

        // Step 2: Sort squares in ascending order
        Arrays.sort(squares);

        long score = 0;

        // Step 3: Subtract the smallest n/2 squares
        for (int i = 0; i < n / 2; i++) {
            score -= squares[i];
        }

        // Step 4: Add the remaining squares
        for (int i = n / 2; i < n; i++) {
            score += squares[i];
        }

        // Step 5: Return the maximum score
        return score;
    }
}
```

---

## Python

```python
from typing import List

class Solution:
    def maxAlternatingSum(self, nums: List[int]) -> int:
        squares = sorted(x * x for x in nums)
        n = len(nums)
        return sum(squares[n // 2:]) - sum(squares[:n // 2])
```

---

## C++

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    long long maxAlternatingSum(vector<int>& nums) {
        int n = nums.size();
        vector<long long> squares(n);
        for (int i = 0; i < n; i++) {
            squares[i] = 1LL * nums[i] * nums[i];
        }
        sort(squares.begin(), squares.end());
        long long score = 0;
        for (int i = 0; i < n / 2; i++) {
            score -= squares[i];
        }
        for (int i = n / 2; i < n; i++) {
            score += squares[i];
        }
        return score;
    }
};
```

---

## C

```c
#include <stdlib.h>

static int cmpLongLong(const void* a, const void* b) {
    long long x = *(const long long*)a;
    long long y = *(const long long*)b;
    if (x < y) return -1;
    if (x > y) return 1;
    return 0;
}

long long maxAlternatingSum(int* nums, int numsSize) {
    long long* squares = (long long*)malloc(numsSize * sizeof(long long));
    for (int i = 0; i < numsSize; i++) {
        squares[i] = (long long)nums[i] * nums[i];
    }
    qsort(squares, numsSize, sizeof(long long), cmpLongLong);
    long long score = 0;
    for (int i = 0; i < numsSize / 2; i++) {
        score -= squares[i];
    }
    for (int i = numsSize / 2; i < numsSize; i++) {
        score += squares[i];
    }
    free(squares);
    return score;
}
```
