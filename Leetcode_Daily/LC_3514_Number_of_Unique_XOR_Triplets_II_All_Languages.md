# LeetCode 3514 - Number of Unique XOR Triplets II

## Java

```java
class Solution {

    public int uniqueXorTriplets(int[] nums) {

        int n = nums.length;

        boolean[] pairSeen = new boolean[2048];

        // Pass 1: Store every pair XOR
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                pairSeen[nums[i] ^ nums[j]] = true;
            }
        }

        // Pass 2: Generate triplet XORs
        boolean[] tripleSeen = new boolean[2048];
        int count = 0;

        for (int s = 0; s < 2048; s++) {

            if (!pairSeen[s])
                continue;

            for (int k = 0; k < n; k++) {

                int value = s ^ nums[k];

                if (!tripleSeen[value]) {
                    tripleSeen[value] = true;
                    count++;
                }
            }
        }

        return count;
    }
}
```

---

## Python

```python
class Solution:

    def uniqueXorTriplets(self, nums: list[int]) -> int:

        pair_seen = [False] * 2048

        for a in nums:
            for b in nums:
                pair_seen[a ^ b] = True

        triple_seen = [False] * 2048
        count = 0

        for value in range(2048):

            if not pair_seen[value]:
                continue

            for num in nums:

                xor_value = value ^ num

                if not triple_seen[xor_value]:
                    triple_seen[xor_value] = True
                    count += 1

        return count
```

---

## C++

```cpp
class Solution {
public:

    int uniqueXorTriplets(vector<int>& nums) {

        int n = nums.size();

        vector<bool> pairSeen(2048, false);

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                pairSeen[nums[i] ^ nums[j]] = true;
            }
        }

        vector<bool> tripleSeen(2048, false);
        int count = 0;

        for (int s = 0; s < 2048; s++) {

            if (!pairSeen[s])
                continue;

            for (int k = 0; k < n; k++) {

                int value = s ^ nums[k];

                if (!tripleSeen[value]) {
                    tripleSeen[value] = true;
                    count++;
                }
            }
        }

        return count;
    }
};
```

---

## C

```c
#include <stdbool.h>

int uniqueXorTriplets(int* nums, int numsSize) {

    bool pairSeen[2048] = {false};

    for (int i = 0; i < numsSize; i++) {
        for (int j = 0; j < numsSize; j++) {
            pairSeen[nums[i] ^ nums[j]] = true;
        }
    }

    bool tripleSeen[2048] = {false};
    int count = 0;

    for (int s = 0; s < 2048; s++) {

        if (!pairSeen[s])
            continue;

        for (int k = 0; k < numsSize; k++) {

            int value = s ^ nums[k];

            if (!tripleSeen[value]) {
                tripleSeen[value] = true;
                count++;
            }
        }
    }

    return count;
}
```