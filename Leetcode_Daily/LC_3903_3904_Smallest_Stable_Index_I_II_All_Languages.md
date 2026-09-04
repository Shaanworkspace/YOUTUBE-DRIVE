# LeetCode 3903 & 3904 - Smallest Stable Index I & II

**Problem Links:**
- Part I: https://leetcode.com/problems/smallest-stable-index-i/
- Part II: https://leetcode.com/problems/smallest-stable-index-ii/

**Approach:** Prefix Maximum + Suffix Minimum
- Part I (LC 3903): n ≤ 100, brute force O(n^2) also accepted, optimized O(n)
- Part II (LC 3904): n ≤ 10^5, ONLY O(n) works, brute force TLE

**Time Complexity:** O(n) both parts
**Space Complexity:** O(n) both parts

---

## Java

```java
// LC 3903 — Smallest Stable Index I (n <= 100, brute force OK)
class Solution {
    public int firstStableIndex(int[] nums, int k) {
        int n = nums.length;
        int[] suffixMin = new int[n];
        suffixMin[n - 1] = nums[n - 1];

        for (int i = n - 2; i >= 0; i--) {
            suffixMin[i] = Math.min(nums[i], suffixMin[i + 1]);
        }

        int prefixMax = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            prefixMax = Math.max(prefixMax, nums[i]);
            int instability = prefixMax - suffixMin[i];
            if (instability <= k) {
                return i;
            }
        }
        return -1;
    }
}

// LC 3904 — Smallest Stable Index II (n <= 10^5, ONLY O(n) works)
class Solution {
    public int firstStableIndex(int[] nums, int k) {
        int n = nums.length;
        int[] suffixMin = new int[n];
        suffixMin[n - 1] = nums[n - 1];

        for (int i = n - 2; i >= 0; i--) {
            suffixMin[i] = Math.min(nums[i], suffixMin[i + 1]);
        }

        int prefixMax = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            prefixMax = Math.max(prefixMax, nums[i]);
            int instability = prefixMax - suffixMin[i];
            if (instability <= k) {
                return i;
            }
        }
        return -1;
    }
}
```

---

## Python

```python
# LC 3903 — Smallest Stable Index I (n <= 100, brute force OK)
class Solution:
    def firstStableIndex(self, nums: list[int], k: int) -> int:
        n = len(nums)
        suffix_min = [0] * n
        suffix_min[-1] = nums[-1]

        for i in range(n - 2, -1, -1):
            suffix_min[i] = min(nums[i], suffix_min[i + 1])

        prefix_max = float('-inf')
        for i in range(n):
            prefix_max = max(prefix_max, nums[i])
            instability = prefix_max - suffix_min[i]
            if instability <= k:
                return i
        return -1

# LC 3904 — Smallest Stable Index II (n <= 10^5, ONLY O(n) works)
class Solution:
    def firstStableIndex(self, nums: list[int], k: int) -> int:
        n = len(nums)
        suffix_min = [0] * n
        suffix_min[-1] = nums[-1]

        for i in range(n - 2, -1, -1):
            suffix_min[i] = min(nums[i], suffix_min[i + 1])

        prefix_max = float('-inf')
        for i in range(n):
            prefix_max = max(prefix_max, nums[i])
            instability = prefix_max - suffix_min[i]
            if instability <= k:
                return i
        return -1
```

---

## C++

```cpp
// LC 3903 — Smallest Stable Index I (n <= 100, brute force OK)
class Solution {
public:
    int firstStableIndex(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> suffixMin(n);
        suffixMin[n - 1] = nums[n - 1];

        for (int i = n - 2; i >= 0; i--) {
            suffixMin[i] = min(nums[i], suffixMin[i + 1]);
        }

        int prefixMax = INT_MIN;
        for (int i = 0; i < n; i++) {
            prefixMax = max(prefixMax, nums[i]);
            int instability = prefixMax - suffixMin[i];
            if (instability <= k) {
                return i;
            }
        }
        return -1;
    }
};

// LC 3904 — Smallest Stable Index II (n <= 10^5, ONLY O(n) works)
class Solution {
public:
    int firstStableIndex(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> suffixMin(n);
        suffixMin[n - 1] = nums[n - 1];

        for (int i = n - 2; i >= 0; i--) {
            suffixMin[i] = min(nums[i], suffixMin[i + 1]);
        }

        int prefixMax = INT_MIN;
        for (int i = 0; i < n; i++) {
            prefixMax = max(prefixMax, nums[i]);
            int instability = prefixMax - suffixMin[i];
            if (instability <= k) {
                return i;
            }
        }
        return -1;
    }
};
```

---

## C

```c
// LC 3903 — Smallest Stable Index I (n <= 100, brute force OK)
int firstStableIndex(int* nums, int numsSize, int k) {
    int suffixMin[numsSize];
    suffixMin[numsSize - 1] = nums[numsSize - 1];

    for (int i = numsSize - 2; i >= 0; i--) {
        suffixMin[i] = nums[i] < suffixMin[i + 1] ? nums[i] : suffixMin[i + 1];
    }

    int prefixMax = -2147483648;
    for (int i = 0; i < numsSize; i++) {
        if (nums[i] > prefixMax) prefixMax = nums[i];
        int instability = prefixMax - suffixMin[i];
        if (instability <= k) {
            return i;
        }
    }
    return -1;
}

// LC 3904 — Smallest Stable Index II (n <= 10^5, ONLY O(n) works)
int firstStableIndex(int* nums, int numsSize, int k) {
    int suffixMin[numsSize];
    suffixMin[numsSize - 1] = nums[numsSize - 1];

    for (int i = numsSize - 2; i >= 0; i--) {
        suffixMin[i] = nums[i] < suffixMin[i + 1] ? nums[i] : suffixMin[i + 1];
    }

    int prefixMax = -2147483648;
    for (int i = 0; i < numsSize; i++) {
        if (nums[i] > prefixMax) prefixMax = nums[i];
        int instability = prefixMax - suffixMin[i];
        if (instability <= k) {
            return i;
        }
    }
    return -1;
}
```
