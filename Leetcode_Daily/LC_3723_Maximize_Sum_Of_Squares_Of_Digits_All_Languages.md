# LeetCode 3723 - Maximize Sum of Squares of Digits

**Problem Link:**
- LeetCode: https://leetcode.com/problems/maximize-sum-of-squares-of-digits/description

**Approach:** Greedy — concentrate the digit sum into as many 9s as possible
Time: O(num) | Space: O(num) for the answer string

**Intuition:** Squaring is convex, so moving value from a smaller digit to a larger digit always increases the sum of squares. The optimal string is k nines plus one remainder digit plus zeros. If sum is greater than 9 times num, no valid integer exists.

---

## Java

```java
class Solution {
    public String maxSumOfSquares(int num, int sum) {


        if (sum > num * 9) {
            return "";
        }


        StringBuilder ans = new StringBuilder();


        for (int i = 0; i < num; i++) {


            if (sum >= 9) {
                ans.append(9);
                sum -= 9;
            } 
            else {
                ans.append(sum);
                sum = 0;
            }
        }


        return ans.toString();
    }
}
```

---

## Python

```python
class Solution:
    def maxSumOfSquares(self, num: int, sum: int) -> str:
        if sum > num * 9:
            return ""

        ans = []
        for _ in range(num):
            if sum >= 9:
                ans.append("9")
                sum -= 9
            else:
                ans.append(str(sum))
                sum = 0
        return "".join(ans)
```

---

## C++

```cpp
class Solution {
public:
    string maxSumOfSquares(int num, int sum) {
        if (sum > num * 9) {
            return "";
        }

        string ans;
        ans.reserve(num);
        for (int i = 0; i < num; i++) {
            if (sum >= 9) {
                ans += '9';
                sum -= 9;
            } else {
                ans += char('0' + sum);
                sum = 0;
            }
        }
        return ans;
    }
};
```

---

## C

```c
char* maxSumOfSquares(int num, int sum) {
    char* ans = (char*)malloc((num + 1) * sizeof(char));
    if (sum > num * 9) {
        ans[0] = '\0';
        return ans;
    }

    for (int i = 0; i < num; i++) {
        if (sum >= 9) {
            ans[i] = '9';
            sum -= 9;
        } else {
            ans[i] = '0' + sum;
            sum = 0;
        }
    }
    ans[num] = '\0';
    return ans;
}
```
