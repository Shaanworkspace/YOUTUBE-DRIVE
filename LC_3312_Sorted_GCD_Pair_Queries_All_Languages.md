# LeetCode 3312 - Sorted GCD Pair Queries

## Java

```java
class Solution {

    public int[] gcdValues(int[] nums, long[] queries) {

        int maxVal = 0;

        // Step 1: Find maximum value
        for (int num : nums) {
            maxVal = Math.max(maxVal, num);
        }

        // Step 2: Frequency of every value
        int[] freq = new int[maxVal + 1];
        for (int num : nums) {
            freq[num]++;
        }

        // Step 3: Count numbers divisible by every divisor
        int[] cntDivisible = new int[maxVal + 1];

        for (int d = 1; d <= maxVal; d++) {
            for (int multiple = d; multiple <= maxVal; multiple += d) {
                cntDivisible[d] += freq[multiple];
            }
        }

        // Step 4: Count pairs having exact GCD = d
        long[] exactGcdCount = new long[maxVal + 1];

        for (int d = maxVal; d >= 1; d--) {

            long count = cntDivisible[d];

            exactGcdCount[d] = count * (count - 1) / 2;

            for (int multiple = d * 2; multiple <= maxVal; multiple += d) {
                exactGcdCount[d] -= exactGcdCount[multiple];
            }
        }

        // Step 5: Prefix sum
        long[] prefix = new long[maxVal + 1];

        for (int d = 1; d <= maxVal; d++) {
            prefix[d] = prefix[d - 1] + exactGcdCount[d];
        }

        // Step 6: Answer queries
        int[] ans = new int[queries.length];

        for (int i = 0; i < queries.length; i++) {

            long k = queries[i];

            int low = 1;
            int high = maxVal;

            while (low < high) {

                int mid = low + (high - low) / 2;

                if (prefix[mid] > k) {
                    high = mid;
                } else {
                    low = mid + 1;
                }
            }

            ans[i] = low;
        }

        return ans;
    }
}
```

---

## Python

```python
class Solution:
    def gcdValues(self, nums: list[int], queries: list[int]) -> list[int]:

        max_val = max(nums)

        freq = [0] * (max_val + 1)
        for num in nums:
            freq[num] += 1

        cnt_divisible = [0] * (max_val + 1)

        for d in range(1, max_val + 1):
            for multiple in range(d, max_val + 1, d):
                cnt_divisible[d] += freq[multiple]

        exact_gcd_count = [0] * (max_val + 1)

        for d in range(max_val, 0, -1):

            count = cnt_divisible[d]
            exact_gcd_count[d] = count * (count - 1) // 2

            for multiple in range(d * 2, max_val + 1, d):
                exact_gcd_count[d] -= exact_gcd_count[multiple]

        prefix = [0] * (max_val + 1)

        for d in range(1, max_val + 1):
            prefix[d] = prefix[d - 1] + exact_gcd_count[d]

        ans = []

        for k in queries:

            low = 1
            high = max_val

            while low < high:

                mid = low + (high - low) // 2

                if prefix[mid] > k:
                    high = mid
                else:
                    low = mid + 1

            ans.append(low)

        return ans
```

---

## C++

```cpp
class Solution {
public:
    vector<int> gcdValues(vector<int>& nums, vector<long long>& queries) {

        int maxVal = *max_element(nums.begin(), nums.end());

        vector<int> freq(maxVal + 1);

        for (int num : nums)
            freq[num]++;

        vector<int> cntDivisible(maxVal + 1);

        for (int d = 1; d <= maxVal; d++) {
            for (int multiple = d; multiple <= maxVal; multiple += d) {
                cntDivisible[d] += freq[multiple];
            }
        }

        vector<long long> exactGcdCount(maxVal + 1);

        for (int d = maxVal; d >= 1; d--) {

            long long count = cntDivisible[d];

            exactGcdCount[d] = count * (count - 1) / 2;

            for (int multiple = d * 2; multiple <= maxVal; multiple += d) {
                exactGcdCount[d] -= exactGcdCount[multiple];
            }
        }

        vector<long long> prefix(maxVal + 1);

        for (int d = 1; d <= maxVal; d++) {
            prefix[d] = prefix[d - 1] + exactGcdCount[d];
        }

        vector<int> ans;

        for (long long k : queries) {

            int low = 1;
            int high = maxVal;

            while (low < high) {

                int mid = low + (high - low) / 2;

                if (prefix[mid] > k)
                    high = mid;
                else
                    low = mid + 1;
            }

            ans.push_back(low);
        }

        return ans;
    }
};
```

---

## C

```c
#include <stdlib.h>

int compare(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);
}

int* gcdValues(int* nums, int numsSize, long long* queries, int queriesSize, int* returnSize) {

    int maxVal = 0;

    for (int i = 0; i < numsSize; i++)
        if (nums[i] > maxVal)
            maxVal = nums[i];

    int* freq = calloc(maxVal + 1, sizeof(int));

    for (int i = 0; i < numsSize; i++)
        freq[nums[i]]++;

    int* cntDivisible = calloc(maxVal + 1, sizeof(int));

    for (int d = 1; d <= maxVal; d++)
        for (int multiple = d; multiple <= maxVal; multiple += d)
            cntDivisible[d] += freq[multiple];

    long long* exactGcdCount = calloc(maxVal + 1, sizeof(long long));

    for (int d = maxVal; d >= 1; d--) {

        long long count = cntDivisible[d];

        exactGcdCount[d] = count * (count - 1) / 2;

        for (int multiple = d * 2; multiple <= maxVal; multiple += d)
            exactGcdCount[d] -= exactGcdCount[multiple];
    }

    long long* prefix = calloc(maxVal + 1, sizeof(long long));

    for (int d = 1; d <= maxVal; d++)
        prefix[d] = prefix[d - 1] + exactGcdCount[d];

    int* ans = malloc(sizeof(int) * queriesSize);

    for (int i = 0; i < queriesSize; i++) {

        long long k = queries[i];

        int low = 1;
        int high = maxVal;

        while (low < high) {

            int mid = low + (high - low) / 2;

            if (prefix[mid] > k)
                high = mid;
            else
                low = mid + 1;
        }

        ans[i] = low;
    }

    *returnSize = queriesSize;

    free(freq);
    free(cntDivisible);
    free(exactGcdCount);
    free(prefix);

    return ans;
}
```