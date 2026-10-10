# LeetCode 2333 - Minimum Sum of Squared Difference

**Problem Link:** https://leetcode.com/problems/minimum-sum-of-squared-difference/description

**Companies:** Amazon, Google, Microsoft, Uber

**Approach:** Greedy with frequency array — always reduce the largest difference first, since lowering x to x minus 1 saves 2x minus 1, which is biggest for the largest x. Combine k1 plus k2 into one budget. If total differences fit in the budget, answer is 0. Otherwise shift frequencies down from maxDiff and sum d squared times freq of d.

**Complexity:** Time O(n plus D), Space O(D), where D is max difference (100000).

---

## Java

```java
class Solution {
    public long minSumSquareDiff(int[] nums1, int[] nums2, int k1, int k2) {
        int[] freq = new int[100001];
        int maxDiff = 0;
        long totalDiff = 0;

        // Step 1: Calculate differences and frequencies
        for (int i = 0; i < nums1.length; i++) {
            int diff = Math.abs(nums1[i] - nums2[i]);
            freq[diff]++;
            totalDiff += diff;
            maxDiff = Math.max(maxDiff, diff);
        }

        // Step 2: Combine operations
        long k = (long) k1 + k2;

        // Step 3: Check if all differences can become zero
        if (totalDiff <= k) {
            return 0;
        }

        // Step 4: Reduce the largest differences first
        for (int d = maxDiff; d > 0 && k > 0; d--) {
            int moves = (int) Math.min(k, (long) freq[d]);
            freq[d] -= moves;
            freq[d - 1] += moves;
            k -= moves;
        }

        // Step 5: Calculate the final squared sum
        long answer = 0;
        for (int d = 1; d <= maxDiff; d++) {
            answer += (long) d * d * freq[d];
        }
        return answer;
    }
}
```

---

## Python

```python
class Solution:
    def minSumSquareDiff(self, nums1: list[int], nums2: list[int], k1: int, k2: int) -> int:
        MAX_D = 100000
        freq = [0] * (MAX_D + 1)
        maxDiff = 0
        totalDiff = 0

        # Step 1: Calculate differences and frequencies
        for a, b in zip(nums1, nums2):
            d = abs(a - b)
            freq[d] += 1
            totalDiff += d
            if d > maxDiff:
                maxDiff = d

        # Step 2: Combine operations
        k = k1 + k2

        # Step 3: Check if all differences can become zero
        if totalDiff <= k:
            return 0

        # Step 4: Reduce the largest differences first
        d = maxDiff
        while d > 0 and k > 0:
            moves = min(k, freq[d])
            freq[d] -= moves
            freq[d - 1] += moves
            k -= moves
            d -= 1

        # Step 5: Calculate the final squared sum
        return sum(i * i * f for i, f in enumerate(freq) if f)
```

---

## C++

```cpp
class Solution {
public:
    long long minSumSquareDiff(vector<int>& nums1, vector<int>& nums2, int k1, int k2) {
        const int MAXD = 100000;
        vector<long long> freq(MAXD + 1, 0);
        int maxDiff = 0;
        long long totalDiff = 0;

        // Step 1: Calculate differences and frequencies
        for (size_t i = 0; i < nums1.size(); i++) {
            int d = abs(nums1[i] - nums2[i]);
            freq[d]++;
            totalDiff += d;
            maxDiff = max(maxDiff, d);
        }

        // Step 2: Combine operations
        long long k = (long long)k1 + k2;

        // Step 3: Check if all differences can become zero
        if (totalDiff <= k) return 0;

        // Step 4: Reduce the largest differences first
        for (int d = maxDiff; d > 0 && k > 0; d--) {
            long long moves = min(k, freq[d]);
            freq[d] -= moves;
            freq[d - 1] += moves;
            k -= moves;
        }

        // Step 5: Calculate the final squared sum
        long long ans = 0;
        for (int d = 1; d <= maxDiff; d++) ans += (long long)d * d * freq[d];
        return ans;
    }
};
```

---

## C

```c
long long minSumSquareDiff(int* nums1, int nums1Size, int* nums2, int nums2Size, int k1, int k2) {
    static long long freq[100001];
    memset(freq, 0, sizeof(freq));
    int maxDiff = 0;
    long long totalDiff = 0;

    // Step 1: Calculate differences and frequencies
    for (int i = 0; i < nums1Size; i++) {
        int d = abs(nums1[i] - nums2[i]);
        freq[d]++;
        totalDiff += d;
        if (d > maxDiff) maxDiff = d;
    }

    // Step 2: Combine operations
    long long k = (long long)k1 + k2;

    // Step 3: Check if all differences can become zero
    if (totalDiff <= k) return 0;

    // Step 4: Reduce the largest differences first
    for (int d = maxDiff; d > 0 && k > 0; d--) {
        long long moves = k < freq[d] ? k : freq[d];
        freq[d] -= moves;
        freq[d - 1] += moves;
        k -= moves;
    }

    // Step 5: Calculate the final squared sum
    long long ans = 0;
    for (int d = 1; d <= maxDiff; d++) ans += (long long)d * d * freq[d];
    return ans;
}
```
