# LeetCode 189 - Rotate Array

Problem: https://leetcode.com/problems/rotate-array/
Companies that ask this: TCS.

## Intuition
The key realization is that rotating an array to the right by `k` steps is equivalent to moving the last `k` elements to the front. Instead of shifting elements one by one (which would be O(n*k)), we can do it in-place with three reversals: reverse the whole array, then reverse the first `k` elements, then reverse the remaining `n-k` elements. This runs in O(n) time with O(1) extra space and is the standard interview-optimal approach.

## Approach
1. Compute `k %= n` to handle cases where `k >= n`.
2. Reverse the entire array — this brings the last `k` elements to the front (but in reversed order).
3. Reverse the first `k` elements — this puts them in the correct order.
4. Reverse the remaining `n-k` elements — this puts the rest in the correct order.
5. Return the modified array.

Time: O(n) — three linear passes, each O(n). Space: O(1) — in-place, only the extra variables and the swap temp.

---

## Java

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k %=n;
        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }
    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;


            left++;
            right--;
        }
    }
}
```

---

## Python

```python
class Solution:
    def rotate(self, nums: list[int], k: int) -> None:
        n = len(nums)
        k %= n
        self._reverse(nums, 0, n - 1)
        self._reverse(nums, 0, k - 1)
        self._reverse(nums, k, n - 1)

    def _reverse(self, nums: list[int], left: int, right: int) -> None:
        while left < right:
            temp = nums[left]
            nums[left] = nums[right]
            nums[right] = temp
            left += 1
            right -= 1
```

---

## C++

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k %= n;
        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }
    void reverse(vector<int>& nums, int left, int right) {
        while (left < right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
};
```

---

## C

```c
void reverse(int* nums, int left, int right) {
    while (left < right) {
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
        left++;
        right--;
    }
}

void rotate(int* nums, int numsSize, int k) {
    k %= numsSize;
    reverse(nums, 0, numsSize - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, numsSize - 1);
}
```