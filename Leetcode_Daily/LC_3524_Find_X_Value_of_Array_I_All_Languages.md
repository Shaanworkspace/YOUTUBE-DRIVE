# LeetCode 3524 - Find X Value of Array I

**Problem Link:**
- LeetCode: https://leetcode.com/problems/find-x-value-of-array-i/description

**Approach:** DP over remainders — count subarrays ending at each position by product modulo k.
Time: O(n * k) | Space: O(k)

**Core transition:** newRemainder = (oldRemainder * numRemainder) % k

---

## Java

```java
class Solution {
    public long[] resultArray(int[] nums, int k) {
        long[] result = new long[k];
        long[] previousRemainderCount = new long[k];

        for (int num : nums) {
            long[] currentRemainderCount = new long[k];

            int numRemainder = num % k;
            currentRemainderCount[numRemainder]++;

            for (int oldRemainder = 0; oldRemainder < k; oldRemainder++) {
                int newRemainder =
                    (oldRemainder * numRemainder) % k;

                currentRemainderCount[newRemainder]
                    += previousRemainderCount[oldRemainder];
            }

            previousRemainderCount = currentRemainderCount;

            for (int remainder = 0; remainder < k; remainder++) {
                result[remainder] += previousRemainderCount[remainder];
            }
        }

        return result;
    }
}
```

---

## Python

```python
class Solution:
    def resultArray(self, nums: list[int], k: int) -> list[int]:
        result = [0] * k
        prev = [0] * k

        for num in nums:
            cur = [0] * k

            r = num % k
            cur[r] += 1

            for old in range(k):
                cur[(old * r) % k] += prev[old]

            prev = cur

            for i in range(k):
                result[i] += prev[i]

        return result
```

---

## C++

```cpp
class Solution {
public:
    vector<long long> resultArray(vector<int>& nums, int k) {
        vector<long long> result(k, 0), prev(k, 0);

        for (int num : nums) {
            vector<long long> cur(k, 0);

            int r = num % k;
            cur[r]++;

            for (int old = 0; old < k; old++)
                cur[(old * r) % k] += prev[old];

            prev = cur;

            for (int i = 0; i < k; i++)
                result[i] += prev[i];
        }

        return result;
    }
};
```

---

## C

```c
long long* resultArray(int* nums, int numsSize, int k, int* returnSize) {
    long long* result = (long long*)calloc(k, sizeof(long long));
    long long* prev = (long long*)calloc(k, sizeof(long long));
    long long* cur = (long long*)calloc(k, sizeof(long long));

    for (int i = 0; i < numsSize; i++) {
        int r = nums[i] % k;
        memset(cur, 0, k * sizeof(long long));
        cur[r]++;

        for (int old = 0; old < k; old++)
            cur[(old * r) % k] += prev[old];

        long long* tmp = prev;
        prev = cur;
        cur = tmp;

        for (int j = 0; j < k; j++)
            result[j] += prev[j];
    }

    free(cur);
    free(prev);
    *returnSize = k;
    return result;
}
```
