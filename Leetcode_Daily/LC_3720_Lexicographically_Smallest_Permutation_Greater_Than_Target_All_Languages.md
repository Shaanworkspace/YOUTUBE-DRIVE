# LeetCode 3720 - Lexicographically Smallest Permutation Greater Than Target

Problem: https://leetcode.com/problems/lexicographically-smallest-permutation-greater-than-target/description

- Difficulty: Medium (Weekly Contest 472 Q3)
- Topics: Hash Table, String, Greedy, Counting, Enumeration
- Asked at: Amazon, Google
- Constraints: 1 <= s.length == target.length <= 300, lowercase English letters only

Given two strings `s` and `target`, both length `n`, consisting of lowercase
English letters, return the lexicographically smallest permutation of `s` that is
strictly greater than `target`. If no permutation of `s` is strictly greater than
`target`, return an empty string.

Intuition: This is a "next permutation" variant where the source pool (`s`) and
the target may be different strings. We walk left-to-right, trying to match
`target[i]` when possible; the moment we must exceed `target[i]` we pick the
smallest available character greater than `target[i]`, then dump the remaining
characters in ascending order to keep the result lexicographically smallest.

Time: O(26 * n)  |  Space: O(26)

---

## Java

```java
class Solution {
    public String lexGreaterPermutation(String s, String target) {
        int n = s.length();

        // Count characters of s
        int[] count = new int[26];

        for (int i = 0; i < n; i++) {
            count[s.charAt(i) - 'a']++;
        }

        StringBuilder result = new StringBuilder();

        for (int i = 0; i < n; i++) {

            int targetChar = target.charAt(i) - 'a';

            // ------------------------------------------------
            // OPTION 1:
            // Try to keep the same character as target[i]
            // ------------------------------------------------

            if (count[targetChar] > 0) {

                // Temporarily use target[i]
                count[targetChar]--;

                // Check whether the remaining characters
                // can make something greater than target suffix
                if (canMakeGreater(count, target, i + 1)) {

                    // Keeping target[i] is possible
                    result.append(target.charAt(i));

                    continue;
                }

                // Keeping this character does not work.
                // Put it back.
                count[targetChar]++;
            }

            // ------------------------------------------------
            // OPTION 2:
            // Choose the smallest character greater than target[i]
            // ------------------------------------------------

            for (int c = targetChar + 1; c < 26; c++) {

                if (count[c] > 0) {

                    // Put this slightly larger character
                    result.append((char) ('a' + c));

                    count[c]--;

                    // Put all remaining characters
                    // in ascending order
                    for (int k = 0; k < 26; k++) {

                        while (count[k] > 0) {
                            result.append((char) ('a' + k));
                            count[k]--;
                        }
                    }

                    return result.toString();
                }
            }

            // We cannot keep target[i]
            // and cannot choose anything larger.
            // Therefore this prefix is impossible.
            return "";
        }

        // target itself was the largest possible permutation
        return "";
    }

    private boolean canMakeGreater(
        int[] count,
        String target,
        int start
    ) {

        // Create the LARGEST possible string
        // from the remaining characters.
        //
        // If even this largest string
        // is NOT greater than target's suffix,
        // then no arrangement can work.

        StringBuilder largest = new StringBuilder();

        for (int c = 25; c >= 0; c--) {

            while (count[c] > 0) {
                largest.append((char) ('a' + c));
                count[c]--;
            }
        }

        // Restore count because this was only a check
        for (int i = 0; i < largest.length(); i++) {
            count[largest.charAt(i) - 'a']++;
        }

        String targetSuffix = target.substring(start);

        return largest.toString().compareTo(targetSuffix) > 0;
    }
}
```

---

## Python

```python
class Solution(object):
    def lexGreaterPermutation(self, s, target):
        """
        :type s: str
        :type target: str
        :rtype: str
        """
        n = len(s)
        count = [0] * 26
        for ch in s:
            count[ord(ch) - ord('a')] += 1
        result = []

        def can_make_greater(start):
            # Build the LARGEST string from remaining characters
            largest = []
            for c in range(25, -1, -1):
                while count[c] > 0:
                    largest.append(chr(ord('a') + c))
                    count[c] -= 1
            # Restore count (this was only a check)
            for ch in largest:
                count[ord(ch) - ord('a')] += 1
            return ''.join(largest) > target[start:]

        for i in range(n):
            tc = ord(target[i]) - ord('a')
            if count[tc] > 0:
                count[tc] -= 1
                if can_make_greater(i + 1):
                    result.append(target[i])
                    continue
                count[tc] += 1
            # Choose the smallest character greater than target[i]
            for c in range(tc + 1, 26):
                if count[c] > 0:
                    result.append(chr(ord('a') + c))
                    count[c] -= 1
                    for k in range(26):
                        while count[k] > 0:
                            result.append(chr(ord('a') + k))
                            count[k] -= 1
                    return ''.join(result)
            return ''
        return ''.join(result)
```

---

## C++

```cpp
class Solution {
public:
    string lexGreaterPermutation(string s, string target) {
        int n = s.length();
        vector<int> count(26, 0);
        for (char ch : s) count[ch - 'a']++;

        string result = "";

        auto canMakeGreater = [&](int start) -> bool {
            string largest = "";
            for (int c = 25; c >= 0; c--) {
                while (count[c] > 0) {
                    largest += char('a' + c);
                    count[c]--;
                }
            }
            for (char ch : largest) count[ch - 'a']++;
            return largest > target.substr(start);
        };

        for (int i = 0; i < n; i++) {
            int tc = target[i] - 'a';

            if (count[tc] > 0) {
                count[tc]--;
                if (canMakeGreater(i + 1)) {
                    result += target[i];
                    continue;
                }
                count[tc]++;
            }

            for (int c = tc + 1; c < 26; c++) {
                if (count[c] > 0) {
                    result += char('a' + c);
                    count[c]--;
                    for (int k = 0; k < 26; k++) {
                        while (count[k] > 0) {
                            result += char('a' + k);
                            count[k]--;
                        }
                    }
                    return result;
                }
            }
            return "";
        }
        return result;
    }
};
```

---

## C

```c
#include <stdlib.h>
#include <string.h>

char* lexGreaterPermutation(char* s, char* target, int* returnSize) {
    int n = (int)strlen(s);
    int count[26] = {0};
    for (int i = 0; i < n; i++) count[s[i] - 'a']++;

    char* result = (char*)malloc((n + 1) * sizeof(char));
    int pos = 0;

    for (int i = 0; i < n; i++) {
        int tc = target[i] - 'a';

        if (count[tc] > 0) {
            count[tc]--;
            char largest[305]; int li = 0;
            for (int c = 25; c >= 0; c--)
                while (count[c] > 0) { largest[li++] = (char)('a' + c); count[c]--; }
            largest[li] = '\0';
            for (int j = 0; j < li; j++) count[largest[j] - 'a']++;
            if (strcmp(largest, target + i + 1) > 0) {
                result[pos++] = target[i];
                continue;
            }
            count[tc]++;
        }

        int taken = 0;
        for (int c = tc + 1; c < 26; c++) {
            if (count[c] > 0) {
                result[pos++] = (char)('a' + c);
                count[c]--;
                for (int k = 0; k < 26; k++)
                    while (count[k] > 0) { result[pos++] = (char)('a' + k); count[k]--; }
                taken = 1;
                break;
            }
        }
        if (!taken) {
            free(result);
            *returnSize = 0;
            return (char*)calloc(1, sizeof(char));
        }
    }
    result[pos] = '\0';
    *returnSize = pos;
    return result;
}
```
