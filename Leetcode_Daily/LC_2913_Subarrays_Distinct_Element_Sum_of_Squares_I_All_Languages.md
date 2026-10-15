# LeetCode 2913 - Subarrays Distinct Element Sum of Squares I

**Problem Link:** https://leetcode.com/problems/subarrays-distinct-element-sum-of-squares-i/description

**Approach:** Brute Force Enumeration with HashSet — fix left endpoint i, expand right endpoint j, track distinct elements in a set, add set size squared to the answer.
Time: O(n squared) | Space: O(n) | Constraints n at most 100 make enumeration legal.

---

## Java

```java
class Solution {
    public int sumCounts(List<Integer> nums) {
        int ans = 0;

        for (int i = 0; i < nums.size(); i++) {
            Set<Integer> set = new HashSet<>();

            for (int j = i; j < nums.size(); j++) {
                set.add(nums.get(j));
                ans += set.size() * set.size();
            }
        }

        return ans;
    }
}
```

---

## Python

```python
class Solution:
    def sumCounts(self, nums: list[int]) -> int:
        ans = 0
        n = len(nums)

        for i in range(n):
            seen = set()

            for j in range(i, n):
                seen.add(nums[j])
                ans += len(seen) * len(seen)

        return ans
```

---

## C++

```cpp
class Solution {
public:
    int sumCounts(vector<int>& nums) {
        int ans = 0;
        int n = nums.size();

        for (int i = 0; i < n; i++) {
            unordered_set<int> seen;

            for (int j = i; j < n; j++) {
                seen.insert(nums[j]);
                ans += seen.size() * seen.size();
            }
        }

        return ans;
    }
};
```

---

## C

```c
int sumCounts(int* nums, int numsSize) {
    int ans = 0;

    for (int i = 0; i < numsSize; i++) {
        int seen[101] = {0};
        int distinct = 0;

        for (int j = i; j < numsSize; j++) {
            if (seen[nums[j]] == 0) {
                seen[nums[j]] = 1;
                distinct++;
            }
            ans += distinct * distinct;
        }
    }

    return ans;
}
```
