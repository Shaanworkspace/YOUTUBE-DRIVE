# LeetCode 3498 - Reverse Degree of a String

**Problem Link:**
- LeetCode: https://leetcode.com/problems/reverse-degree-of-a-string/description/

**Companies:** None verified (recent Easy problem; no official company tags found)

**Approach:** Single-pass simulation — for each character compute reverse alphabet value (27 minus forward value) and multiply by 1-indexed string position, then accumulate the sum.
Time: O(n) | Space: O(1)

---

## Java

```java
class Solution {
    public int reverseDegree(String s) {
        int sum = 0;

        for (int i = 0; i < s.length(); i++) {

            char ch = s.charAt(i);

            int alphabet = ch - 'a' + 1;

            int reverse = 27 - alphabet;

            int position = i + 1;

            int product = reverse * position;

            sum = sum + product;
        }

        return sum;
    }
}
```

---

## Python

```python
class Solution:
    def reverseDegree(self, s: str) -> int:
        total = 0

        for i, ch in enumerate(s):
            alphabet = ord(ch) - ord('a') + 1

            reverse = 27 - alphabet

            position = i + 1

            product = reverse * position

            total = total + product

        return total
```

---

## C++

```cpp
class Solution {
public:
    int reverseDegree(string s) {
        int sum = 0;

        for (int i = 0; i < (int)s.length(); i++) {

            char ch = s[i];

            int alphabet = ch - 'a' + 1;

            int reverse = 27 - alphabet;

            int position = i + 1;

            int product = reverse * position;

            sum = sum + product;
        }

        return sum;
    }
};
```

---

## C

```c
int reverseDegree(char* s) {
    int sum = 0;

    for (int i = 0; s[i] != '\0'; i++) {

        char ch = s[i];

        int alphabet = ch - 'a' + 1;

        int reverse = 27 - alphabet;

        int position = i + 1;

        int product = reverse * position;

        sum = sum + product;
    }

    return sum;
}
```
