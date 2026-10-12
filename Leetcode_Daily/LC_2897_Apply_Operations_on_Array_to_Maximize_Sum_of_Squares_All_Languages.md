# LeetCode 2897 - Apply Operations on Array to Maximize Sum of Squares

**Problem Link:** https://leetcode.com/problems/apply-operations-on-array-to-maximize-sum-of-squares/description

**Companies:** Sprinklr (reported); bit-manipulation greedy variants appear at Google, Amazon, Meta

**Approach:** Bit counting plus greedy — AND OR operations only redistribute set bits, so total count per bit position never changes. Count set bits across 32 positions, then build k largest numbers by taking every available bit, square each, and accumulate modulo 1e9 plus 7.

**Complexity:** Time O((n plus k) times 32), Space O(32).

---

## Java

```java
import java.util.*;

class Solution {
    public int maxSum(List<Integer> nums, int k) {
        long MOD = 1_000_000_007L;
        int[] count = new int[32];

        // Step 1: Count set bits
        for (int num : nums) {
            for (int bit = 0; bit < 32; bit++) {
                if ((num & (1 << bit)) != 0) {
                    count[bit]++;
                }
            }
        }

        long ans = 0;

        // Step 2: Construct k numbers
        for (int i = 0; i < k; i++) {
            long num = 0;

            for (int bit = 0; bit < 32; bit++) {
                if (count[bit] > 0) {
                    num |= (1L << bit);
                    count[bit]--;
                }
            }

            // Step 3: Add square
            ans = (ans + num * num) % MOD;
        }

        return (int) ans;
    }
}
```

---

## Python

```python
class Solution:
    def maxSum(self, nums: list[int], k: int) -> int:
        MOD = 1_000_000_007
        count = [0] * 32

        # Step 1: Count set bits
        for num in nums:
            for bit in range(32):
                if num & (1 << bit):
                    count[bit] += 1

        ans = 0

        # Step 2: Construct k numbers
        for _ in range(k):
            num = 0
            for bit in range(32):
                if count[bit] > 0:
                    num |= (1 << bit)
                    count[bit] -= 1

            # Step 3: Add square
            ans = (ans + num * num) % MOD

        return ans
```

---

## C++

```cpp
class Solution {
public:
    int maxSum(vector<int>& nums, int k) {
        const long long MOD = 1000000007LL;
        long long count[32] = {0};

        // Step 1: Count set bits
        for (int num : nums) {
            for (int bit = 0; bit < 32; bit++) {
                if (num & (1LL << bit)) {
                    count[bit]++;
                }
            }
        }

        long long ans = 0;

        // Step 2: Construct k numbers
        for (int i = 0; i < k; i++) {
            long long num = 0;
            for (int bit = 0; bit < 32; bit++) {
                if (count[bit] > 0) {
                    num |= (1LL << bit);
                    count[bit]--;
                }
            }

            // Step 3: Add square
            ans = (ans + num * num) % MOD;
        }

        return (int)ans;
    }
};
```

---

## C

```c
int maxSum(int* nums, int numsSize, int k) {
    const long long MOD = 1000000007LL;
    long long count[32] = {0};

    // Step 1: Count set bits
    for (int i = 0; i < numsSize; i++) {
        for (int bit = 0; bit < 32; bit++) {
            if (nums[i] & (1LL << bit)) {
                count[bit]++;
            }
        }
    }

    long long ans = 0;

    // Step 2: Construct k numbers
    for (int i = 0; i < k; i++) {
        long long num = 0;
        for (int bit = 0; bit < 32; bit++) {
            if (count[bit] > 0) {
                num |= (1LL << bit);
                count[bit]--;
            }
        }

        // Step 3: Add square
        ans = (ans + num * num) % MOD;
    }

    return (int)ans;
}
```
