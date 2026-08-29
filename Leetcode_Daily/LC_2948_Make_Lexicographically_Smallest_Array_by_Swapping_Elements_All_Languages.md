# LeetCode 2948 - Make Lexicographically Smallest Array by Swapping Elements

Problem: https://leetcode.com/problems/make-lexicographically-smallest-array-by-swapping-elements/
Companies that ask this: Amazon, Google, Atlassian, IBM, PhonePe, Uber.

## Intuition
You may swap two elements only if their absolute difference is `<= limit`. That means
values form connected groups: any two values whose gap is `<= limit` can eventually be
reordered among themselves (transitively). Within each group we can place the smallest
values at the smallest original indices to make the whole array lexicographically smallest.

## Approach
1. Tag every value with its original index and sort by value.
2. Walk the sorted values; extend a group while `sorted[i+1] - sorted[i] <= limit`.
3. Collect the original indices of the group, sort them, and write the group's smallest
   values into those smallest indices.
4. Repeat for every group; return the rebuilt array.

Time: O(n log n) — sorting + grouping. Space: O(n) — for the value/index pairs.

---

## Java

```java
import java.util.*;

class Solution {

    static class Pair {
        int value;
        int index;

        Pair(int value, int index) {
            this.value = value;
            this.index = index;
        }
    }

    public int[] lexicographicallySmallestArray(int[] nums, int limit) {

        // Step 1: Store value with original index
        ArrayList<Pair> arr = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
            arr.add(new Pair(nums[i], i));
        }

        // Step 2: Sort Pairs according to value
        arr.sort((a, b) -> Integer.compare(a.value, b.value));

        int start = 0;

        // Step 3: Process every group
        while (start < arr.size()) {

            int end = start;

            // Find the end of current group
            while (end + 1 < arr.size()
                    && arr.get(end + 1).value - arr.get(end).value <= limit) {
                end++;
            }

            // Step 4: Store original indices of this group
            ArrayList<Integer> indices = new ArrayList<>();

            for (int i = start; i <= end; i++) {
                indices.add(arr.get(i).index);
            }

            // Step 5: Sort original indices
            Collections.sort(indices);

            // Step 6: Put smallest values at smallest indices
            for (int i = 0; i < indices.size(); i++) {
                nums[indices.get(i)] = arr.get(start + i).value;
            }

            // Move to next group
            start = end + 1;
        }

        return nums;
    }
}
```

---

## Python

```python
from typing import List


class Solution:
    def lexicographicallySmallestArray(self, nums: List[int], limit: int) -> List[int]:
        # pair each value with its original index, then sort by value
        arr = sorted((nums[i], i) for i in range(len(nums)))

        n = len(nums)
        ans = [0] * n

        start = 0
        while start < n:
            end = start
            # grow the group while consecutive values differ by at most limit
            while end + 1 < n and arr[end + 1][0] - arr[end][0] <= limit:
                end += 1

            # original indices of this group, sorted ascending
            indices = sorted(arr[i][1] for i in range(start, end + 1))

            # place the smallest values at the smallest original indices
            for k, (val, _) in zip(range(len(indices)), arr[start:start + len(indices)]):
                ans[indices[k]] = val

            start = end + 1

        return ans
```

---

## C++

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    vector<int> lexicographicallySmallestArray(vector<int>& nums, int limit) {
        int n = nums.size();
        vector<pair<int, int>> arr;
        arr.reserve(n);
        for (int i = 0; i < n; ++i) {
            arr.push_back({nums[i], i});
        }
        sort(arr.begin(), arr.end());

        vector<int> ans(n);
        int start = 0;
        while (start < n) {
            int end = start;
            while (end + 1 < n && arr[end + 1].first - arr[end].first <= limit) {
                ++end;
            }
            vector<int> indices;
            for (int i = start; i <= end; ++i) {
                indices.push_back(arr[i].second);
            }
            sort(indices.begin(), indices.end());
            for (int k = 0; k < (int)indices.size(); ++k) {
                ans[indices[k]] = arr[start + k].first;
            }
            start = end + 1;
        }
        return ans;
    }
};
```

---

## C

```c
#include <stdlib.h>

typedef struct {
    int value;
    int index;
} Pair;

int cmpPair(const void* a, const void* b) {
    int va = ((const Pair*)a)->value;
    int vb = ((const Pair*)b)->value;
    return (va > vb) - (va < vb);
}

int cmpInt(const void* a, const void* b) {
    int ia = *(const int*)a;
    int ib = *(const int*)b;
    return (ia > vb) - (ia < vb);
}

int* lexicographicallySmallestArray(int* nums, int numsSize, int limit, int* returnSize) {
    Pair* arr = (Pair*)malloc(sizeof(Pair) * numsSize);
    for (int i = 0; i < numsSize; ++i) {
        arr[i].value = nums[i];
        arr[i].index = i;
    }
    qsort(arr, numsSize, sizeof(Pair), cmpPair);

    int* ans = (int*)malloc(sizeof(int) * numsSize);
    int start = 0;
    while (start < numsSize) {
        int end = start;
        while (end + 1 < numsSize && arr[end + 1].value - arr[end].value <= limit) {
            ++end;
        }
        int gsize = end - start + 1;
        int* gidx = (int*)malloc(sizeof(int) * gsize);
        for (int i = 0; i < gsize; ++i) {
            gidx[i] = arr[start + i].index;
        }
        qsort(gidx, gsize, sizeof(int), cmpInt);
        for (int k = 0; k < gsize; ++k) {
            ans[gidx[k]] = arr[start + k].value;
        }
        free(gidx);
        start = end + 1;
    }
    free(arr);
    *returnSize = numsSize;
    return ans;
}
```
