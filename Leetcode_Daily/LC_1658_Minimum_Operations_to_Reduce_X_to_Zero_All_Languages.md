# LeetCode 1658 - Minimum Operations to Reduce X to Zero

**Problem Link:** https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/

**Companies:** Amazon, Google, Meta

**Approach:** Think in reverse. Removing min prefix + suffix with sum x equals keeping the longest middle subarray with sum total minus x. Prefix Sum + HashMap finds that longest subarray in one pass. No recursion, no DP.
Time: O(n) | Space: O(n)

---

## Java

```java
class Solution {
    public int minOperations(int[] nums, int x) {
        int n = nums.length;

        // Step 1: Calculate total sum
        int total = 0;
        for (int num : nums) {
            total += num;
        }

        // Step 2: Remaining subarray sum
        int target = total - x;

        if (target < 0) return -1;
        if (target == 0) return n;

        // Step 3: Prefix Sum + HashMap
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);

        int prefixSum = 0;
        int maxLength = -1;

        for (int i = 0; i < n; i++) {
            prefixSum += nums[i];

            int required = prefixSum - target;

            if (map.containsKey(required)) {
                int length = i - map.get(required);
                maxLength = Math.max(maxLength, length);
            }

            if (!map.containsKey(prefixSum)) {
                map.put(prefixSum, i);
            }
        }

        // No valid subarray
        if (maxLength == -1) {
            return -1;
        }

        // Minimum operations
        return n - maxLength;
    }
}
```

---

## Python

```python
class Solution:
    def minOperations(self, nums: list[int], x: int) -> int:
        n = len(nums)

        # Step 1: Calculate total sum
        total = sum(nums)

        # Step 2: Remaining subarray sum
        target = total - x

        if target < 0:
            return -1
        if target == 0:
            return n

        # Step 3: Prefix Sum + HashMap
        mp = {0: -1}

        prefix_sum = 0
        max_length = -1

        for i, num in enumerate(nums):
            prefix_sum += num

            required = prefix_sum - target

            if required in mp:
                max_length = max(max_length, i - mp[required])

            if prefix_sum not in mp:
                mp[prefix_sum] = i

        # No valid subarray
        if max_length == -1:
            return -1

        # Minimum operations
        return n - max_length
```

---

## C++

```cpp
class Solution {
public:
    int minOperations(vector<int>& nums, int x) {
        int n = nums.size();

        // Step 1: Calculate total sum
        int total = 0;
        for (int num : nums) total += num;

        // Step 2: Remaining subarray sum
        int target = total - x;

        if (target < 0) return -1;
        if (target == 0) return n;

        // Step 3: Prefix Sum + HashMap
        unordered_map<int, int> mp;
        mp[0] = -1;

        int prefixSum = 0;
        int maxLength = -1;

        for (int i = 0; i < n; i++) {
            prefixSum += nums[i];

            int required = prefixSum - target;

            if (mp.find(required) != mp.end()) {
                maxLength = max(maxLength, i - mp[required]);
            }

            if (mp.find(prefixSum) == mp.end()) {
                mp[prefixSum] = i;
            }
        }

        // No valid subarray
        if (maxLength == -1) return -1;

        // Minimum operations
        return n - maxLength;
    }
};
```

---

## C

```c
// Simple open-addressing hash map: key -> first index
typedef struct {
    int key;
    int val;
    int used;
} Entry;

static unsigned hashInt(int k, unsigned cap) {
    unsigned u = (unsigned)(k * 2654435761u);
    return u % cap;
}

static int mapGet(Entry* t, unsigned cap, int key, int* out) {
    unsigned i = hashInt(key, cap);
    for (unsigned c = 0; c < cap; c++) {
        unsigned j = (i + c) % cap;
        if (!t[j].used) return 0;
        if (t[j].key == key) { *out = t[j].val; return 1; }
    }
    return 0;
}

static void mapPutIfAbsent(Entry* t, unsigned cap, int key, int val) {
    unsigned i = hashInt(key, cap);
    for (unsigned c = 0; c < cap; c++) {
        unsigned j = (i + c) % cap;
        if (!t[j].used) { t[j].used = 1; t[j].key = key; t[j].val = val; return; }
        if (t[j].key == key) return;
    }
}

int minOperations(int* nums, int numsSize, int x) {
    int n = numsSize;

    // Step 1: Calculate total sum
    int total = 0;
    for (int i = 0; i < n; i++) total += nums[i];

    // Step 2: Remaining subarray sum
    int target = total - x;

    if (target < 0) return -1;
    if (target == 0) return n;

    // Step 3: Prefix Sum + HashMap
    unsigned cap = (unsigned)(2 * n + 3);
    Entry* mp = (Entry*)calloc(cap, sizeof(Entry));
    mapPutIfAbsent(mp, cap, 0, -1);

    int prefixSum = 0;
    int maxLength = -1;

    for (int i = 0; i < n; i++) {
        prefixSum += nums[i];

        int required = prefixSum - target;
        int idx = 0;
        if (mapGet(mp, cap, required, &idx)) {
            int length = i - idx;
            if (length > maxLength) maxLength = length;
        }

        mapPutIfAbsent(mp, cap, prefixSum, i);
    }

    free(mp);

    // No valid subarray
    if (maxLength == -1) return -1;

    // Minimum operations
    return n - maxLength;
}
```
