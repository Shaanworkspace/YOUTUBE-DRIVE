# GFG — Remove Duplicates Sorted Array

**Problem Link:** https://www.geeksforgeeks.org/problems/remove-duplicate-elements-from-sorted-array/1

**Companies:** Zoho, Morgan Stanley, Microsoft, Samsung, Google, Wipro, Xome

---

## Approach: Two Pointer (In-Place)

Use a write pointer to track the position of the next unique element. Scan with a read pointer; when a new unique element is found, place it at the write position.

Time: O(n) | Space: O(1)

---

## Java

```java
class Solution {
    ArrayList<Integer> removeDuplicates(int[] arr) {
        ArrayList<Integer> ans = new ArrayList<>();
        ans.add(arr[0]);
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] != arr[i - 1]) {
                ans.add(arr[i]);
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
    def removeDuplicates(self, arr):
        ans = [arr[0]]
        for i in range(1, len(arr)):
            if arr[i] != arr[i - 1]:
                ans.append(arr[i])
        return ans
```

---

## C++

```cpp
class Solution {
public:
    vector<int> removeDuplicates(vector<int>& arr) {
        vector<int> ans;
        ans.push_back(arr[0]);
        for (int i = 1; i < arr.size(); i++) {
            if (arr[i] != arr[i - 1]) {
                ans.push_back(arr[i]);
            }
        }
        return ans;
    }
};
```

---

## C

```c
int removeDuplicates(int arr[], int n) {
    if (n == 0) return 0;
    int write = 1;
    for (int read = 1; read < n; read++) {
        if (arr[read] != arr[read - 1]) {
            arr[write] = arr[read];
            write++;
        }
    }
    return write;
}
```
