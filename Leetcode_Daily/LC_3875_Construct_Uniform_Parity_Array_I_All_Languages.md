# LeetCode 3875 - Construct Uniform Parity Array I

## Problem Link
https://leetcode.com/problems/construct-uniform-parity-array-i/

## Approach
This is a brain teaser. The answer is always `true` regardless of the input.

**Key Insight:** You can always construct a uniform parity array because:
1. If all elements are already the same parity (all odd or all even), just copy nums1 directly.
2. If there's a mix of odd and even, subtract any odd element from each even element (even - odd = odd), making everything odd.

Since every case yields `true`, the optimal solution is simply `return true`.

## Complexity
- Time: O(1)
- Space: O(1)

---

## Java
```java
class Solution {
    public boolean uniformArray(int[] nums1) {
        return true;
    }
}
```

---

## Python
```python
class Solution:
    def uniformArray(self, nums1: List[int]) -> bool:
        return True
```

---

## C++
```cpp
class Solution {
public:
    bool uniformArray(vector<int>& nums1) {
        return true;
    }
};
```

---

## C
```c
bool uniformArray(int* nums1, int nums1Size) {
    return true;
}
```
