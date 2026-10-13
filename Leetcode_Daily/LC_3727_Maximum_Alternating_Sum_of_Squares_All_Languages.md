# LeetCode 3727 - Maximum Alternating Sum of Squares

**Problem Link:** https://leetcode.com/problems/maximum-alternating-sum-of-squares/

**Companies:** Philips

**Approach:** Square and Sort Greedy — square every element, sort ascending, subtract the smallest n/2 squares, add the rest.
**Time:** O(n log n) | **Space:** O(n)

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
class Solution:
    def maxAlternatingSum(self, nums: list[int]) -> int:
        n = len(nums)

        # Step 1: Calculate the square of each number
        squares = [x * x for x in nums]

        # Step 2: Sort squares in ascending order
        squares.sort()

        score = 0

        # Step 3: Subtract the smallest n//2 squares
        for i in range(n // 2):
            score -= squares[i]

        # Step 4: Add the remaining squares
        for i in range(n // 2, n):
            score += squares[i]

        # Step 5: Return the maximum score
        return score
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

        // Step 1: Calculate the square of each number
        for (int i = 0; i < n; i++) {
            squares[i] = (long long)nums[i] * nums[i];
        }

        // Step 2: Sort squares in ascending order
        sort(squares.begin(), squares.end());

        long long score = 0;

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
};
```

---

## C

```c
#include <stdlib.h>

static int cmpLongLong(const void* a, const void* b) {
    long long x = *(const long long*)a;
    long long y = *(const long long*)b;
    return (x > y) - (x < y);
}

long long maxAlternatingSum(int* nums, int numsSize) {
    int n = numsSize;
    long long* squares = (long long*)malloc(sizeof(long long) * n);

    // Step 1: Calculate the square of each number
    for (int i = 0; i < n; i++) {
        squares[i] = (long long)nums[i] * nums[i];
    }

    // Step 2: Sort squares in ascending order
    qsort(squares, n, sizeof(long long), cmpLongLong);

    long long score = 0;

    // Step 3: Subtract the smallest n/2 squares
    for (int i = 0; i < n / 2; i++) {
        score -= squares[i];
    }

    // Step 4: Add the remaining squares
    for (int i = n / 2; i < n; i++) {
        score += squares[i];
    }

    free(squares);

    // Step 5: Return the maximum score
    return score;
}
```
