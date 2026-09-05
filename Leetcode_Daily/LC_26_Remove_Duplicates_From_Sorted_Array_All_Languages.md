# LeetCode 26 - Remove Duplicates from Sorted Array

**Problem Link:** https://leetcode.com/problems/remove-duplicates-from-sorted-array/

**Companies:** Amazon, Google, Meta, Microsoft, Bloomberg, Apple, TCS, Infosys, Wipro

---

## Approach 1: Brute Force — Using a Set

Use a HashSet to collect unique elements, then overwrite the array.
Time: O(n) | Space: O(n)

## Approach 2: Optimal — Two Pointers (In-Place)

Use slow/fast pointers. When fast finds a new element, move it behind slow.
Time: O(n) | Space: O(1)

---

## Java

```java
// Approach 1: Brute Force — Using a Set
class Solution {
    public int removeDuplicates(int[] nums) {
        java.util.LinkedHashSet<Integer> set = new java.util.LinkedHashSet<>();
        for (int num : nums) {
            set.add(num);
        }
        int i = 0;
        for (int val : set) {
            nums[i++] = val;
        }
        return set.size();
    }
}

// Approach 2: Optimal — Two Pointers (In-Place)
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0, j = 0, n = nums.length;
        while (j < n) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
            j++;
        }
        return i + 1;
    }
}
```

---

## Python

```python
# Approach 1: Brute Force — Using a Set
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        unique = list(dict.fromkeys(nums))
        for i, val in enumerate(unique):
            nums[i] = val
        return len(unique)

# Approach 2: Optimal — Two Pointers (In-Place)
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        i, j, n = 0, 0, len(nums)
        while j < n:
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]
            j += 1
        return i + 1
```

---

## C++

```cpp
// Approach 1: Brute Force — Using a Set
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        set<int> s(nums.begin(), nums.end());
        int i = 0;
        for (int val : s) {
            nums[i++] = val;
        }
        return s.size();
    }
};

// Approach 2: Optimal — Two Pointers (In-Place)
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int i = 0, j = 0, n = nums.size();
        while (j < n) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
            j++;
        }
        return i + 1;
    }
};
```

---

## C

```c
// Approach 1: Brute Force — Using extra array
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize == 0) return 0;
    int temp[numsSize];
    int k = 0;
    for (int i = 0; i < numsSize; i++) {
        if (i == 0 || nums[i] != nums[i - 1]) {
            temp[k++] = nums[i];
        }
    }
    for (int i = 0; i < k; i++) {
        nums[i] = temp[i];
    }
    return k;
}

// Approach 2: Optimal — Two Pointers (In-Place)
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize == 0) return 0;
    int i = 0, j = 0;
    while (j < numsSize) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
        j++;
    }
    return i + 1;
}
```
