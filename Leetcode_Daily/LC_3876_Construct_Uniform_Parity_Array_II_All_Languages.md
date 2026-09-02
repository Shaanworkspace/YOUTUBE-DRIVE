# LeetCode 3876 - Construct Uniform Parity Array II

## Problem Link
https://leetcode.com/problems/construct-uniform-parity-array-ii/

## Approach
This is the harder Part 2 of the parity array series. The key constraint is `nums1[i] - nums1[j] >= 1` — the result must be positive.

**Core Insight:** If all elements share the same parity, copy them directly. If mixed, try to make everything odd by subtracting an odd element from each even element. The bottleneck is the smallest odd number — if any even number is smaller than it, you cannot make that even number odd (subtraction would go negative).

**Algorithm:**
1. Find the minimum odd number in the array.
2. If no odd or no even exists, return true (already uniform).
3. Check if any even number is smaller than the minimum odd. If yes, return false. Otherwise, return true.

## Complexity
- Time: O(n) — single pass to find minimums, single pass to check.
- Space: O(1) — only a few integer variables.

---

## Java
```java
class Solution {
    public boolean uniformArray(int[] nums1) {
        final int INF = Integer.MAX_VALUE;
        int minOdd = INF;
        for (int x : nums1) {
            if (x % 2 == 1) {
                minOdd = Math.min(minOdd, x);
            }
        }
        for (int x : nums1) {
            if (x % 2 == 0 && minOdd != INF && x < minOdd) {
                return false;
            }
        }
        return true;
    }
}
```

---

## Python
```python
class Solution:
    def uniformArray(self, nums1: List[int]) -> bool:
        INF = float('inf')
        min_odd = INF
        for x in nums1:
            if x % 2 == 1:
                min_odd = min(min_odd, x)
        for x in nums1:
            if x % 2 == 0 and min_odd != INF and x < min_odd:
                return False
        return True
```

---

## C++
```cpp
class Solution {
public:
    bool uniformArray(vector<int>& nums1) {
        int minOdd = INT_MAX;
        for (int x : nums1) {
            if (x % 2 == 1) {
                minOdd = min(minOdd, x);
            }
        }
        for (int x : nums1) {
            if (x % 2 == 0 && minOdd != INT_MAX && x < minOdd) {
                return false;
            }
        }
        return true;
    }
};
```

---

## C
```c
bool uniformArray(int* nums1, int nums1Size) {
    int minOdd = INT_MAX;
    for (int i = 0; i < nums1Size; i++) {
        if (nums1[i] % 2 == 1 && nums1[i] < minOdd) {
            minOdd = nums1[i];
        }
    }
    for (int i = 0; i < nums1Size; i++) {
        if (nums1[i] % 2 == 0 && minOdd != INT_MAX && nums1[i] < minOdd) {
            return false;
        }
    }
    return true;
}
```
