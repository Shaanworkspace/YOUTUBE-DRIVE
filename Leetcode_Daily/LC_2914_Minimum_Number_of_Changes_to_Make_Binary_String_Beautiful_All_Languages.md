# LeetCode 2914 - Minimum Number of Changes to Make Binary String Beautiful

Problem: https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful/

A binary string is beautiful if it can be split into even-length substrings where each substring contains only one character (all 0s or all 1s). Pair up adjacent characters (0,1), (2,3), ... and count how many pairs differ. That count is the minimum number of changes.

## Java

```java
class Solution {
    public int minChanges(String s) {
        int count = 0;
        for (int i = 0; i < s.length(); i += 2) {
            if (s.charAt(i) != s.charAt(i + 1)) count++;
        }
        return count;
    }
}
```

---

## Python

```python
class Solution:
    def minChanges(self, s: str) -> int:
        count = 0
        for i in range(0, len(s), 2):
            if s[i] != s[i + 1]:
                count += 1
        return count
```

---

## C++

```cpp
class Solution {
public:
    int minChanges(string s) {
        int count = 0;
        for (int i = 0; i < (int)s.length(); i += 2) {
            if (s[i] != s[i + 1]) count++;
        }
        return count;
    }
};
```

---

## C

```c
#include <string.h>

int minChanges(char* s) {
    int count = 0;
    int len = strlen(s);
    for (int i = 0; i < len; i += 2) {
        if (s[i] != s[i + 1]) count++;
    }
    return count;
}
```
