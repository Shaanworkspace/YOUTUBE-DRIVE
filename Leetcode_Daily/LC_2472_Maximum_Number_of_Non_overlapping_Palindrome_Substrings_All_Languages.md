# LeetCode 2472 - Maximum Number of Non-overlapping Palindrome Substrings

**Problem Link:** https://leetcode.com/problems/maximum-number-of-non-overlapping-palindrome-substrings
**Difficulty:** Hard
**Topics:** String, Dynamic Programming, Greedy, Two Pointers
**Companies:** Google, Amazon, Microsoft, Meta, Oracle, LinkedIn, Salesforce, Walmart Labs

---

## Approach: Greedy — Check Every Possible Palindrome Starting at Earliest Position

Move a right pointer from left to right. For each right pointer position, check palindromes of length k, k+1, k+2... If a palindrome is found, increment the count, move the start pointer to right+1 (to avoid overlap), and break to the next right position.

---

## Java

```java
class Solution {
    public int maxPalindromes(String s, int k) {
        int n = s.length();
        int ans = 0;
        int start = 0;

        for (int r = k - 1; r < n; r++) {
            for (int len = k; len <= r - start + 1; len++) {
                int l = r - len + 1;
                if (check(s, l, r)) {
                    ans++;
                    start = r + 1;
                    break;
                }
            }
        }
        return ans;
    }

    private boolean check(String s, int l, int r) {
        while (l < r) {
            if (s.charAt(l) != s.charAt(r)) {
                return false;
            }
            l++;
            r--;
        }
        return true;
    }
}
```

---

## Python

```python
class Solution:
    def maxPalindromes(self, s: str, k: int) -> int:
        n = len(s)
        ans = 0
        start = 0

        for r in range(k - 1, n):
            for length in range(k, r - start + 2):
                l = r - length + 1
                if l < start:
                    continue
                if self.check(s, l, r):
                    ans += 1
                    start = r + 1
                    break
        return ans

    def check(self, s: str, l: int, r: int) -> bool:
        while l < r:
            if s[l] != s[r]:
                return False
            l += 1
            r -= 1
        return True
```

---

## C++

```cpp
class Solution {
public:
    int maxPalindromes(string s, int k) {
        int n = s.size();
        int ans = 0;
        int start = 0;

        for (int r = k - 1; r < n; r++) {
            for (int len = k; len <= r - start + 1; len++) {
                int l = r - len + 1;
                if (check(s, l, r)) {
                    ans++;
                    start = r + 1;
                    break;
                }
            }
        }
        return ans;
    }

private:
    bool check(string& s, int l, int r) {
        while (l < r) {
            if (s[l] != s[r]) return false;
            l++;
            r--;
        }
        return true;
    }
};
```

---

## C

```c
bool check(char* s, int l, int r) {
    while (l < r) {
        if (s[l] != s[r]) return false;
        l++;
        r--;
    }
    return true;
}

int maxPalindromes(char* s, int k) {
    int n = strlen(s);
    int ans = 0;
    int start = 0;

    for (int r = k - 1; r < n; r++) {
        for (int len = k; len <= r - start + 1; len++) {
            int l = r - len + 1;
            if (check(s, l, r)) {
                ans++;
                start = r + 1;
                break;
            }
        }
    }
    return ans;
}
```
