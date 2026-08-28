# LeetCode 3734 - Lexicographically Smallest Palindromic Permutation Greater Than Target

Problem: https://leetcode.com/problems/lexicographically-smallest-palindromic-permutation-greater-than-target/
Difficulty: Hard
Topics: String, Backtracking, Greedy, Two Pointers

## Approach
1. Count the frequency of every character in `s`.
2. A palindrome is possible only if at most ONE character has an odd frequency
   (that character becomes the middle of the palindrome). If more than one odd
   frequency exists, return `""`.
3. Keep HALF of every frequency (each side of the palindrome gets one copy).
4. Build the LEFT half greedily with backtracking:
   - At each position we may start from `'a'` if we are already strictly greater
     than the `target` prefix, otherwise we must start from `target[pos]` (we
     cannot go smaller than the target at the first differing position).
   - Try characters `'a'..'z'` in order; the first complete left half that yields
     a full palindrome strictly greater than `target` is the lexicographically
     smallest valid answer.
5. Mirror the left half to form the final palindrome and compare with `target`.

## Complexity
- Time:  O(26 * n)  — at each of the n/2 positions we try at most 26 characters.
- Space: O(26)      — fixed frequency array.

---

## Java
```java
class Solution {
    public String lexPalindromicPermutation(String s, String target) {
        // --------------------------------------------------
        // STEP 1: Count frequency of every character
        // --------------------------------------------------
        int[] characterFrequency = new int[26];
        for (char currentCharacter : s.toCharArray()) {
            int characterIndex = currentCharacter - 'a';
            characterFrequency[characterIndex]++;
        }

        // --------------------------------------------------
        // STEP 2: Check whether a palindrome is possible
        // --------------------------------------------------
        int oddFrequencyCount = 0;
        char middleCharacter = 0;
        for (int characterIndex = 0; characterIndex < 26; characterIndex++) {
            if (characterFrequency[characterIndex] % 2 == 1) {
                oddFrequencyCount++;
                middleCharacter = (char) ('a' + characterIndex);
            }
        }
        // More than one odd frequency means palindrome is impossible.
        if (oddFrequencyCount > 1) {
            return "";
        }

        // --------------------------------------------------
        // STEP 3: Keep only half of every frequency
        // --------------------------------------------------
        for (int characterIndex = 0; characterIndex < 26; characterIndex++) {
            characterFrequency[characterIndex] /= 2;
        }

        int stringLength = s.length();
        int halfLength = stringLength / 2;
        char[] leftHalf = new char[halfLength];

        // --------------------------------------------------
        // STEP 4: Build the left half using backtracking
        // --------------------------------------------------
        if (buildLeftHalf(0, false, target, characterFrequency, leftHalf,
                middleCharacter, stringLength)) {
            // --------------------------------------------------
            // STEP 5: Construct the final palindrome
            // --------------------------------------------------
            String leftPart = new String(leftHalf);
            String rightPart = new StringBuilder(leftPart).reverse().toString();
            String palindrome = leftPart;
            if (stringLength % 2 == 1) {
                palindrome += middleCharacter;
            }
            palindrome += rightPart;
            return palindrome;
        }
        return "";
    }

    private boolean buildLeftHalf(int currentPosition, boolean alreadyGreaterThanTarget,
            String target, int[] characterFrequency, char[] leftHalf,
            char middleCharacter, int stringLength) {
        if (currentPosition == leftHalf.length) {
            String leftPart = new String(leftHalf);
            String rightPart = new StringBuilder(leftPart).reverse().toString();
            String palindrome = leftPart;
            if (stringLength % 2 == 1) {
                palindrome += middleCharacter;
            }
            palindrome += rightPart;
            return palindrome.compareTo(target) > 0;
        }

        char firstCharacterToTry;
        if (alreadyGreaterThanTarget) {
            firstCharacterToTry = 'a';
        } else {
            firstCharacterToTry = target.charAt(currentPosition);
        }

        for (char currentCharacter = firstCharacterToTry;
                currentCharacter <= 'z'; currentCharacter++) {
            int characterIndex = currentCharacter - 'a';
            if (characterFrequency[characterIndex] == 0) {
                continue;
            }
            leftHalf[currentPosition] = currentCharacter;
            characterFrequency[characterIndex]--;
            boolean nowGreaterThanTarget = alreadyGreaterThanTarget
                    || currentCharacter > target.charAt(currentPosition);
            if (buildLeftHalf(currentPosition + 1, nowGreaterThanTarget, target,
                    characterFrequency, leftHalf, middleCharacter, stringLength)) {
                return true;
            }
            characterFrequency[characterIndex]++;
        }
        return false;
    }
}
```

---

## Python
```python
class Solution(object):
    def lexPalindromicPermutation(self, s, target):
        """
        :type s: str
        :type target: str
        :rtype: str
        """
        cnt = [0] * 26
        for ch in s:
            cnt[ord(ch) - 97] += 1

        odd = 0
        mid = -1
        for i in range(26):
            if cnt[i] % 2 == 1:
                odd += 1
                mid = i
        if odd > 1:
            return ""

        for i in range(26):
            cnt[i] //= 2

        n = len(s)
        half = n // 2
        left = [''] * half

        def build(pos, greater):
            if pos == half:
                left_part = ''.join(left)
                right_part = left_part[::-1]
                pal = left_part + (chr(97 + mid) if n % 2 else '') + right_part
                return pal > target
            start = 97 if greater else ord(target[pos])
            for c in range(start, 123):
                idx = c - 97
                if cnt[idx] == 0:
                    continue
                left[pos] = chr(c)
                cnt[idx] -= 1
                now_greater = greater or c > ord(target[pos])
                if build(pos + 1, now_greater):
                    return True
                cnt[idx] += 1
            return False

        if build(0, False):
            left_part = ''.join(left)
            right_part = left_part[::-1]
            return left_part + (chr(97 + mid) if n % 2 else '') + right_part
        return ""
```

---

## C++
```cpp
class Solution {
public:
    string lexPalindromicPermutation(string s, string target) {
        vector<int> cnt(26, 0);
        for (char c : s) cnt[c - 'a']++;

        int odd = 0;
        char mid = 0;
        for (int i = 0; i < 26; ++i) {
            if (cnt[i] % 2 == 1) {
                odd++;
                mid = 'a' + i;
            }
        }
        if (odd > 1) return "";

        for (int i = 0; i < 26; ++i) cnt[i] /= 2;

        int n = s.length();
        int half = n / 2;
        string left(half, ' ');

        function<bool(int, bool)> build = [&](int pos, bool greater) -> bool {
            if (pos == half) {
                string lp = left;
                string rp = string(lp.rbegin(), lp.rend());
                string pal = lp + (n % 2 ? string(1, mid) : "") + rp;
                return pal > target;
            }
            char start = greater ? 'a' : target[pos];
            for (char c = start; c <= 'z'; ++c) {
                int idx = c - 'a';
                if (cnt[idx] == 0) continue;
                left[pos] = c;
                cnt[idx]--;
                bool ng = greater || c > target[pos];
                if (build(pos + 1, ng)) return true;
                cnt[idx]++;
            }
            return false;
        };

        if (build(0, false)) {
            string lp = left;
            string rp = string(lp.rbegin(), lp.rend());
            return lp + (n % 2 ? string(1, mid) : "") + rp;
        }
        return "";
    }
};
```

---

## C
```c
#include <stdlib.h>
#include <string.h>

static int g_cnt[26];
static char* g_left;
static int g_half;
static char* g_target;
static int g_n;
static int g_mid;

static int build(int pos, int greater) {
    if (pos == g_half) {
        char* lp = (char*)malloc(g_half + 1);
        strncpy(lp, g_left, g_half);
        lp[g_half] = '\0';
        int len = g_n;
        char* pal = (char*)malloc(len + 1);
        for (int i = 0; i < g_half; ++i) pal[i] = g_left[i];
        int idx = g_half;
        if (g_n % 2) pal[idx++] = (char)('a' + g_mid);
        for (int i = g_half - 1; i >= 0; --i) pal[idx++] = g_left[i];
        pal[len] = '\0';
        int cmp = strcmp(pal, g_target);
        free(lp);
        free(pal);
        return cmp > 0 ? 1 : 0;
    }
    char start = greater ? 'a' : g_target[pos];
    for (char c = start; c <= 'z'; ++c) {
        int ci = c - 'a';
        if (g_cnt[ci] == 0) continue;
        g_left[pos] = c;
        g_cnt[ci]--;
        int ng = greater || c > g_target[pos];
        if (build(pos + 1, ng)) {
            g_cnt[ci]++;
            return 1;
        }
        g_cnt[ci]++;
    }
    return 0;
}

char* lexPalindromicPermutation(char* s, char* target, int* returnSize) {
    for (int i = 0; i < 26; ++i) g_cnt[i] = 0;
    g_n = (int)strlen(s);
    g_half = g_n / 2;
    g_target = target;
    for (int i = 0; i < g_n; ++i) g_cnt[s[i] - 'a']++;
    int odd = 0;
    g_mid = -1;
    for (int i = 0; i < 26; ++i)
        if (g_cnt[i] % 2) { odd++; g_mid = i; }
    if (odd > 1) { *returnSize = 0; return strdup(""); }
    for (int i = 0; i < 26; ++i) g_cnt[i] /= 2;
    g_left = (char*)malloc(g_half + 1);
    g_left[g_half] = '\0';
    if (build(0, 0)) {
        char* res = (char*)malloc(g_n + 1);
        for (int i = 0; i < g_half; ++i) res[i] = g_left[i];
        int idx = g_half;
        if (g_n % 2) res[idx++] = (char)('a' + g_mid);
        for (int i = g_half - 1; i >= 0; --i) res[idx++] = g_left[i];
        res[g_n] = '\0';
        *returnSize = g_n;
        free(g_left);
        return res;
    }
    free(g_left);
    *returnSize = 0;
    return strdup("");
}
```
