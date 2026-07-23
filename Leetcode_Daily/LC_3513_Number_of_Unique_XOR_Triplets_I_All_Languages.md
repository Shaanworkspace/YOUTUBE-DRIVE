# LeetCode 3513 - Number of Unique XOR Triplets I

## Java

```java
class Solution {

    public int uniqueXorTriplets(int[] nums) {

        int n = nums.length;

        if (n < 3)
            return n;

        int bits = 0;
        int temp = n;

        while (temp > 0) {
            bits++;
            temp >>= 1;
        }

        return (int) Math.pow(2, bits);
    }
}
```

---

## Python

```python
class Solution:

    def uniqueXorTriplets(self, nums: list[int]) -> int:

        n = len(nums)

        if n < 3:
            return n

        bits = 0
        temp = n

        while temp > 0:
            bits += 1
            temp >>= 1

        return 1 << bits
```

---

## C++

```cpp
class Solution {
public:

    int uniqueXorTriplets(vector<int>& nums) {

        int n = nums.size();

        if (n < 3)
            return n;

        int bits = 0;
        int temp = n;

        while (temp > 0) {
            bits++;
            temp >>= 1;
        }

        return 1 << bits;
    }
};
```

---

## C

```c
int uniqueXorTriplets(int* nums, int numsSize) {

    int n = numsSize;

    if (n < 3)
        return n;

    int bits = 0;
    int temp = n;

    while (temp > 0) {
        bits++;
        temp >>= 1;
    }

    return 1 << bits;
}
```