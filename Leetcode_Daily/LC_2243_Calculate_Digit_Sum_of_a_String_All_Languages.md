# LeetCode 2243 - Calculate Digit Sum of a String

Problem: https://leetcode.com/problems/calculate-digit-sum-of-a-string/

You are given a string `s` and an integer `k`. Repeatedly divide `s` into groups of size `k` (the last group may be smaller), replace each group with the sum of its digits, and merge the sums into a new string. Repeat until the length of `s` is less than or equal to `k`. Return the final string.

## Java

```java
class Solution {
    public String digitSum(String s, int k) {
        while (s.length() > k) {
            StringBuilder result = new StringBuilder();
            for (int i = 0; i < s.length(); i += k) {
                int sum = 0;
                int end = Math.min(i + k, s.length());
                for (int j = i; j < end; j++) {
                    sum += s.charAt(j) - '0';
                }
                result.append(sum);
            }
            s = result.toString();
        }
        return s;
    }
}
```

---

## Python

```python
class Solution:
    def digitSum(self, s: str, k: int) -> str:
        while len(s) > k:
            result = []
            for i in range(0, len(s), k):
                end = min(i + k, len(s))
                total = sum(int(c) for c in s[i:end])
                result.append(str(total))
            s = ''.join(result)
        return s
```

---

## C++

```cpp
class Solution {
public:
    string digitSum(string s, int k) {
        while ((int)s.length() > k) {
            string result;
            for (int i = 0; i < (int)s.length(); i += k) {
                int sum = 0;
                int end = min(i + k, (int)s.length());
                for (int j = i; j < end; j++) {
                    sum += s[j] - '0';
                }
                result += to_string(sum);
            }
            s = result;
        }
        return s;
    }
};
```

---

## C

```c
#include <string.h>
#include <stdlib.h>
#include <stdio.h>

char* digitSum(char* s, int k) {
    int len = (int)strlen(s);
    while (len > k) {
        char* result = (char*)malloc((size_t)(len * 2 + 2));
        int pos = 0;
        for (int i = 0; i < len; i += k) {
            int sum = 0;
            int end = (i + k < len) ? i + k : len;
            for (int j = i; j < end; j++) {
                sum += s[j] - '0';
            }
            pos += sprintf(result + pos, "%d", sum);
        }
        result[pos] = '\0';
        strcpy(s, result);
        free(result);
        len = pos;
    }
    return s;
}
```
