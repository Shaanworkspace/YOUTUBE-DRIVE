# LeetCode 75 - Sort Colors (Sort 0s, 1s and 2s)

**Problem Links:**
- LeetCode: https://leetcode.com/problems/sort-colors/
- GeeksforGeeks: https://www.geeksforgeeks.org/problems/sort-an-array-of-0s-1s-and-2s4231/1

**Companies:** Amazon, Google, Meta, Microsoft, Bloomberg, Apple

---

## Approach 1: Brute Force — Counting (Two Pass)

Count occurrences of 0, 1, 2, then overwrite the array.
Time: O(n) | Space: O(1) | Passes: 2

## Approach 2: Dutch National Flag (Single Pass Optimal)

Three pointers: low, mid, high. Swap elements in a single pass.
Time: O(n) | Space: O(1) | Passes: 1

---

## Java

```java
// Approach 1: Brute Force — Counting
class Solution {
    public void sortColors(int[] nums) {
        int count0 = 0, count1 = 0, count2 = 0;

        for (int num : nums) {
            if (num == 0) count0++;
            else if (num == 1) count1++;
            else count2++;
        }

        int i = 0;
        while (count0-- > 0) nums[i++] = 0;
        while (count1-- > 0) nums[i++] = 1;
        while (count2-- > 0) nums[i++] = 2;
    }
}

// Approach 2: Dutch National Flag (Optimal — Single Pass)
class Solution {
    public void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                mid++;
            } else {
                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;
                high--;
            }
        }
    }
}
```

---

## Python

```python
# Approach 1: Brute Force — Counting
class Solution:
    def sortColors(self, nums: list[int]) -> None:
        count0 = count1 = count2 = 0
        for num in nums:
            if num == 0: count0 += 1
            elif num == 1: count1 += 1
            else: count2 += 1

        i = 0
        for _ in range(count0): nums[i] = 0; i += 1
        for _ in range(count1): nums[i] = 1; i += 1
        for _ in range(count2): nums[i] = 2; i += 1

# Approach 2: Dutch National Flag (Optimal — Single Pass)
class Solution:
    def sortColors(self, nums: list[int]) -> None:
        low, mid, high = 0, 0, len(nums) - 1

        while mid <= high:
            if nums[mid] == 0:
                nums[low], nums[mid] = nums[mid], nums[low]
                low += 1
                mid += 1
            elif nums[mid] == 1:
                mid += 1
            else:
                nums[mid], nums[high] = nums[high], nums[mid]
                high -= 1
```

---

## C++

```cpp
// Approach 1: Brute Force — Counting
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int count0 = 0, count1 = 0, count2 = 0;
        for (int num : nums) {
            if (num == 0) count0++;
            else if (num == 1) count1++;
            else count2++;
        }
        int i = 0;
        while (count0--) nums[i++] = 0;
        while (count1--) nums[i++] = 1;
        while (count2--) nums[i++] = 2;
    }
};

// Approach 2: Dutch National Flag (Optimal — Single Pass)
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0, mid = 0, high = nums.size() - 1;
        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums[low++], nums[mid++]);
            } else if (nums[mid] == 1) {
                mid++;
            } else {
                swap(nums[mid], nums[high--]);
            }
        }
    }
};
```

---

## C

```c
// Approach 1: Brute Force — Counting
void sortColors(int* nums, int numsSize) {
    int count0 = 0, count1 = 0, count2 = 0;
    for (int i = 0; i < numsSize; i++) {
        if (nums[i] == 0) count0++;
        else if (nums[i] == 1) count1++;
        else count2++;
    }
    int i = 0;
    while (count0-- > 0) nums[i++] = 0;
    while (count1-- > 0) nums[i++] = 1;
    while (count2-- > 0) nums[i++] = 2;
}

// Approach 2: Dutch National Flag (Optimal — Single Pass)
void sortColors(int* nums, int numsSize) {
    int low = 0, mid = 0, high = numsSize - 1;
    while (mid <= high) {
        if (nums[mid] == 0) {
            int temp = nums[low]; nums[low] = nums[mid]; nums[mid] = temp;
            low++; mid++;
        } else if (nums[mid] == 1) {
            mid++;
        } else {
            int temp = nums[mid]; nums[mid] = nums[high]; nums[high] = temp;
            high--;
        }
    }
}
```
