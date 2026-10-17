# LeetCode 3551 - Minimum Swaps to Sort by Digit Sum

**Problem Link:** https://leetcode.com/problems/minimum-swaps-to-sort-by-digit-sum/

**Difficulty:** Medium (Weekly Contest 450, Q2)

**Approach:** Sorting + Permutation Cycles
- Compute the digit sum of every number and sort elements by `(digitSum, value)`.
- Build a map from each original index to its target index in the sorted order.
- Decompose the permutation into cycles; a cycle of length `k` needs `k - 1` swaps.

**Time Complexity:** O(n log n) (sorting dominates; cycle walk is O(n))
**Space Complexity:** O(n)

---

## Java

```java
import java.util.Arrays;

class Solution {
    public int minSwaps(int[] nums) {
        int n = nums.length;

        // Step 1: Calculate digit sum of every number
        int[] digitSum = new int[n];
        for (int i = 0; i < n; i++) {
            int number = nums[i];
            while (number > 0) {
                digitSum[i] += number % 10;
                number /= 10;
            }
        }

        // Step 2: Store the old position of every number
        Integer[] oldPosition = new Integer[n];
        for (int i = 0; i < n; i++) {
            oldPosition[i] = i;
        }

        // Step 3: Sort old positions by digit sum
        // If digit sums are equal, smaller number comes first
        Arrays.sort(oldPosition, (a, b) -> {
            if (digitSum[a] != digitSum[b]) {
                return Integer.compare(digitSum[a], digitSum[b]);
            }
            return Integer.compare(nums[a], nums[b]);
        });

        // Step 4: Find the target position of every number
        int[] targetPosition = new int[n];
        for (int target = 0; target < n; target++) {
            int old = oldPosition[target];
            targetPosition[old] = target;
        }

        // Step 5: Count minimum swaps using cycles
        boolean[] visited = new boolean[n];
        int swaps = 0;
        for (int i = 0; i < n; i++) {
            // Skip if already visited or at the correct position
            if (visited[i] || targetPosition[i] == i) {
                visited[i] = true;
                continue;
            }

            int currentPosition = i;
            int cycleSize = 0;

            // Follow target positions until the cycle is complete
            while (!visited[currentPosition]) {
                visited[currentPosition] = true;
                currentPosition = targetPosition[currentPosition];
                cycleSize++;
            }

            // A cycle of k elements requires k - 1 swaps
            swaps += cycleSize - 1;
        }

        // Step 6: Return the total minimum swaps
        return swaps;
    }
}
```

---

## Python

```python
class Solution:
    def minSwaps(self, nums: list[int]) -> int:
        n = len(nums)

        # Step 1: Calculate digit sum of every number
        digit_sum = [0] * n
        for i, num in enumerate(nums):
            number = num
            while number > 0:
                digit_sum[i] += number % 10
                number //= 10

        # Step 2: Store the old position of every number
        old_position = list(range(n))

        # Step 3: Sort old positions by digit sum, then by value
        old_position.sort(key=lambda i: (digit_sum[i], nums[i]))

        # Step 4: Find the target position of every number
        target_position = [0] * n
        for target, old in enumerate(old_position):
            target_position[old] = target

        # Step 5: Count minimum swaps using cycles
        visited = [False] * n
        swaps = 0
        for i in range(n):
            if visited[i] or target_position[i] == i:
                visited[i] = True
                continue

            current_position = i
            cycle_size = 0
            while not visited[current_position]:
                visited[current_position] = True
                current_position = target_position[current_position]
                cycle_size += 1

            # A cycle of k elements requires k - 1 swaps
            swaps += cycle_size - 1

        # Step 6: Return the total minimum swaps
        return swaps
```

---

## C++

```cpp
#include <vector>
#include <numeric>
#include <algorithm>

class Solution {
public:
    int minSwaps(std::vector<int>& nums) {
        int n = nums.size();

        // Step 1: Calculate digit sum of every number
        std::vector<int> digitSum(n, 0);
        for (int i = 0; i < n; i++) {
            int number = nums[i];
            while (number > 0) {
                digitSum[i] += number % 10;
                number /= 10;
            }
        }

        // Step 2: Store the old position of every number
        std::vector<int> oldPosition(n);
        std::iota(oldPosition.begin(), oldPosition.end(), 0);

        // Step 3: Sort old positions by digit sum, then by value
        std::sort(oldPosition.begin(), oldPosition.end(), [&](int a, int b) {
            if (digitSum[a] != digitSum[b]) {
                return digitSum[a] < digitSum[b];
            }
            return nums[a] < nums[b];
        });

        // Step 4: Find the target position of every number
        std::vector<int> targetPosition(n, 0);
        for (int target = 0; target < n; target++) {
            int old = oldPosition[target];
            targetPosition[old] = target;
        }

        // Step 5: Count minimum swaps using cycles
        std::vector<bool> visited(n, false);
        int swaps = 0;
        for (int i = 0; i < n; i++) {
            if (visited[i] || targetPosition[i] == i) {
                visited[i] = true;
                continue;
            }

            int currentPosition = i;
            int cycleSize = 0;
            while (!visited[currentPosition]) {
                visited[currentPosition] = true;
                currentPosition = targetPosition[currentPosition];
                cycleSize++;
            }

            // A cycle of k elements requires k - 1 swaps
            swaps += cycleSize - 1;
        }

        // Step 6: Return the total minimum swaps
        return swaps;
    }
};
```

---

## C

```c
#include <stdlib.h>

typedef struct {
    int digitSum;
    int value;
    int index;
} NumInfo;

static int compare(const void* a, const void* b) {
    const NumInfo* x = (const NumInfo*)a;
    const NumInfo* y = (const NumInfo*)b;
    if (x->digitSum != y->digitSum) {
        return x->digitSum - y->digitSum;
    }
    return x->value - y->value;
}

int minSwaps(int* nums, int numsSize) {
    int n = numsSize;

    // Step 1 + 2: Calculate digit sum and store original position
    NumInfo* info = (NumInfo*)malloc(n * sizeof(NumInfo));
    for (int i = 0; i < n; i++) {
        int number = nums[i];
        int sum = 0;
        while (number > 0) {
            sum += number % 10;
            number /= 10;
        }
        info[i].digitSum = sum;
        info[i].value = nums[i];
        info[i].index = i;
    }

    // Step 3: Sort by digit sum, then by value
    qsort(info, n, sizeof(NumInfo), compare);

    // Step 4: Find the target position of every number
    int* targetPosition = (int*)malloc(n * sizeof(int));
    for (int target = 0; target < n; target++) {
        targetPosition[info[target].index] = target;
    }

    // Step 5: Count minimum swaps using cycles
    bool* visited = (bool*)calloc(n, sizeof(bool));
    int swaps = 0;
    for (int i = 0; i < n; i++) {
        if (visited[i] || targetPosition[i] == i) {
            visited[i] = true;
            continue;
        }

        int currentPosition = i;
        int cycleSize = 0;
        while (!visited[currentPosition]) {
            visited[currentPosition] = true;
            currentPosition = targetPosition[currentPosition];
            cycleSize++;
        }

        // A cycle of k elements requires k - 1 swaps
        swaps += cycleSize - 1;
    }

    free(info);
    free(targetPosition);
    free(visited);

    // Step 6: Return the total minimum swaps
    return swaps;
}
```
