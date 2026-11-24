# LeetCode 3411 - Maximum Subarray With Equal Products

Problem: https://leetcode.com/problems/maximum-subarray-with-equal-products/

## Approach
A subarray is product equivalent when `prod == lcm * gcd`.

- Enumerate every starting index `i` and extend `j` from `i` to `n - 1`.
- Keep the running product, GCD and LCM of the current subarray.
  - `gcd` starts at 0 (`gcd(0, x) = x`).
  - `lcm` starts at 1 (`lcm(1, x) = x`).
  - `product` starts at 1.
- Every time `product == gcd * lcm`, update the answer with `j - i + 1`.
- GCD uses Euclid; LCM uses `a / gcd(a, b) * b` to reduce overflow risk.

## Complexity
- Time: O(n^2) subarrays, each updated in O(log(max value)) for GCD/LCM.
- Space: O(1) extra space.

---

## Java
```java
class Solution {
    public int maxLength(int[] nums) {

        int n = nums.length;
        int ans = 0;

        for (int i = 0; i < n; i++) {

            long product = 1;
            long gcd = 0;
            long lcm = 1;

            for (int j = i; j < n; j++) {

                product *= nums[j];

                gcd = findGCD(gcd, nums[j]);

                lcm = findLCM(lcm, nums[j]);

                if (product == gcd * lcm) {
                    ans = Math.max(ans, j - i + 1);
                }
            }
        }

        return ans;
    }

    // GCD Function
    private long findGCD(long a, long b) {

        while (b != 0) {
            long temp = b;
            b = a % b;
            a = temp;
        }

        return a;
    }

    // LCM Function
    private long findLCM(long a, long b) {

        return (a / findGCD(a, b)) * b;
    }
}
```

---

## Python
```python
class Solution:
    def maxLength(self, nums: List[int]) -> int:
        n = len(nums)
        ans = 0

        for i in range(n):
            product = 1
            gcd_val = 0
            lcm_val = 1

            for j in range(i, n):
                product *= nums[j]
                gcd_val = self.find_gcd(gcd_val, nums[j])
                lcm_val = self.find_lcm(lcm_val, nums[j])

                if product == gcd_val * lcm_val:
                    ans = max(ans, j - i + 1)

        return ans

    # GCD Function
    def find_gcd(self, a: int, b: int) -> int:
        while b != 0:
            a, b = b, a % b
        return a

    # LCM Function
    def find_lcm(self, a: int, b: int) -> int:
        return (a // self.find_gcd(a, b)) * b
```

---

## C++
```cpp
class Solution {
public:
    int maxLength(vector<int>& nums) {
        int n = nums.size();
        int ans = 0;

        for (int i = 0; i < n; i++) {
            long long product = 1;
            long long g = 0;
            long long l = 1;

            for (int j = i; j < n; j++) {
                product *= nums[j];

                g = findGCD(g, nums[j]);
                l = findLCM(l, nums[j]);

                if (product == g * l) {
                    ans = max(ans, j - i + 1);
                }
            }
        }

        return ans;
    }

private:
    // GCD Function
    long long findGCD(long long a, long long b) {
        while (b != 0) {
            long long temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    // LCM Function
    long long findLCM(long long a, long long b) {
        return (a / findGCD(a, b)) * b;
    }
};
```

---

## C
```c
// LeetCode C signature: int maxLength(int* nums, int numsSize)

static long long findGCD(long long a, long long b) {
    while (b != 0) {
        long long temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

static long long findLCM(long long a, long long b) {
    return (a / findGCD(a, b)) * b;
}

int maxLength(int* nums, int numsSize) {
    int n = numsSize;
    int ans = 0;

    for (int i = 0; i < n; i++) {
        long long product = 1;
        long long g = 0;
        long long l = 1;

        for (int j = i; j < n; j++) {
            product *= nums[j];

            g = findGCD(g, nums[j]);
            l = findLCM(l, nums[j]);

            if (product == g * l) {
                int len = j - i + 1;
                if (len > ans) {
                    ans = len;
                }
            }
        }
    }

    return ans;
}
```
