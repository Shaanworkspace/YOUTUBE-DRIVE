# LeetCode 3517 - Smallest Palindromic Rearrangement I

## Java

```java
class Solution {

    public String smallestPalindrome(String s) {

        int[] freq = new int[26];

        for (char ch : s.toCharArray()) {
            freq[ch - 'a']++;
        }

        StringBuilder left = new StringBuilder();
        String middle = "";

        for (int i = 0; i < 26; i++) {

            for (int j = 0; j < freq[i] / 2; j++) {
                left.append((char) (i + 'a'));
            }

            if (freq[i] % 2 == 1) {
                middle = String.valueOf((char) (i + 'a'));
            }
        }

        String right = new StringBuilder(left).reverse().toString();

        return left.toString() + middle + right;
    }
}
```

---

## Python

```python
class Solution:

    def smallestPalindrome(self, s: str) -> str:

        freq = [0] * 26

        for ch in s:
            freq[ord(ch) - ord('a')] += 1

        left = []
        middle = ""

        for i in range(26):

            left.extend(chr(i + ord('a')) for _ in range(freq[i] // 2))

            if freq[i] % 2 == 1:
                middle = chr(i + ord('a'))

        left = "".join(left)
        right = left[::-1]

        return left + middle + right
```

---

## C++

```cpp
class Solution {
public:

    string smallestPalindrome(string s) {

        vector<int> freq(26, 0);

        for (char ch : s) {
            freq[ch - 'a']++;
        }

        string left = "";
        string middle = "";

        for (int i = 0; i < 26; i++) {

            for (int j = 0; j < freq[i] / 2; j++) {
                left += char(i + 'a');
            }

            if (freq[i] % 2 == 1) {
                middle = char(i + 'a');
            }
        }

        string right = left;
        reverse(right.begin(), right.end());

        return left + middle + right;
    }
};
```

---

## C

```c
#include <stdlib.h>
#include <string.h>

char* smallestPalindrome(char* s) {

    int freq[26] = {0};
    int n = strlen(s);

    for (int i = 0; i < n; i++) {
        freq[s[i] - 'a']++;
    }

    char* left = (char*)malloc(n + 1);
    int leftSize = 0;
    char middle = '\0';

    for (int i = 0; i < 26; i++) {

        for (int j = 0; j < freq[i] / 2; j++) {
            left[leftSize++] = (char)(i + 'a');
        }

        if (freq[i] % 2 == 1) {
            middle = (char)(i + 'a');
        }
    }

    char* ans = (char*)malloc(n + 1);
    int index = 0;

    for (int i = 0; i < leftSize; i++) {
        ans[index++] = left[i];
    }

    if (middle != '\0') {
        ans[index++] = middle;
    }

    for (int i = leftSize - 1; i >= 0; i--) {
        ans[index++] = left[i];
    }

    ans[index] = '\0';

    free(left);

    return ans;
}
```