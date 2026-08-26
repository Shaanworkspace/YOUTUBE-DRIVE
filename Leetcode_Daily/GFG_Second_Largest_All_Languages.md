# GeeksforGeeks — Second Largest Element (O(n) Optimal)

> **Problem:** https://www.geeksforgeeks.org/problems/second-largest3735/1
>
> Return the **second largest distinct** element in an array, or `-1` if no such
> element exists (e.g. all elements equal, or fewer than two distinct values).
> This is the optimal **two-pass** approach: **O(n) time, O(1) space**.

## Approach
1. **Pass 1 — find the maximum.** Scan the array once and keep the running `largest` (start from `arr[0]`).
2. **Pass 2 — find the second largest.** Scan again and keep the largest value that is **strictly smaller** than `largest`. Initialize `secondLargest = -1` and update it only when `arr[i] < largest` **and** `arr[i] > secondLargest`.
3. Return `secondLargest` (stays `-1` when no second distinct value exists).

### Why this works / edge cases
- **All-equal array** → no value is `< largest`, so `secondLargest` stays `-1`. ✅
- **Negatives** → comparisons are magnitude-based, so it works for negative inputs too. ✅
- **Size-1 array** → returns `-1`. ✅
- **Exactly two distinct values** → returns the smaller one. ✅
- Using strict `<` skips duplicates of the maximum — the most common bug in second-largest implementations.

## Complexity
| Metric | Value |
|--------|-------|
| Time   | O(n)  (at most two linear passes) |
| Space  | O(1)  (only a few integer variables) |

> Sorting-based solutions cost **O(n log n)** and use **O(n)** extra space — avoid them in interviews.

---

## Java
```java
class Solution {
    public int getSecondLargest(int[] arr) {
        // Step 1: Find the largest element
        int largest = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > largest) {
                largest = arr[i];
            }
        }
        // Step 2: Find the second largest element
        int secondLargest = -1;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] < largest && arr[i] > secondLargest) {
                secondLargest = arr[i];
            }
        }
        return secondLargest;
    }
}
```

## Python
```python
class Solution:
    def getSecondLargest(self, arr):
        largest = arr[0]
        for i in range(1, len(arr)):
            if arr[i] > largest:
                largest = arr[i]
        secondLargest = -1
        for i in range(len(arr)):
            if arr[i] < largest and arr[i] > secondLargest:
                secondLargest = arr[i]
        return secondLargest
```

## C++
```cpp
class Solution {
public:
    int getSecondLargest(vector<int>& arr) {
        int largest = arr[0];
        for (int i = 1; i < (int)arr.size(); i++) {
            if (arr[i] > largest) largest = arr[i];
        }
        int secondLargest = -1;
        for (int i = 0; i < (int)arr.size(); i++) {
            if (arr[i] < largest && arr[i] > secondLargest)
                secondLargest = arr[i];
        }
        return secondLargest;
    }
};
```

## C
```c
int getSecondLargest(int arr[], int n) {
    int largest = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > largest) largest = arr[i];
    }
    int secondLargest = -1;
    for (int i = 0; i < n; i++) {
        if (arr[i] < largest && arr[i] > secondLargest)
            secondLargest = arr[i];
    }
    return secondLargest;
}
```

---

*All four implementations share the same optimal O(n) / O(1) logic so you can submit on any platform.*
