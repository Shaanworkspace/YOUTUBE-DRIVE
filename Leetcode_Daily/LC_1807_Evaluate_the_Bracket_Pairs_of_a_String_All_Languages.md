# LeetCode 1807 - Evaluate the Bracket Pairs of a String

**Problem Link:** https://leetcode.com/problems/evaluate-the-bracket-pairs-of-a-string/description

**Companies:** Google, Remitly

**Approach:** HashMap Lookup + Single Pass Traversal
Build a HashMap from the knowledge pairs, then traverse the string once. Append plain letters directly; on '(' extract the key until ')', replace with the mapped value or "?" if unknown.
Time: O(n + m) | Space: O(m) where n = s.length, m = total knowledge characters.

---

## Java

```java
class Solution {
    public String evaluate(String s, List<List<String>> knowledge) {

        int n = s.length();

        HashMap<String, String> mp = new HashMap<>();

        for (List<String> vec : knowledge) {
            mp.put(vec.get(0), vec.get(1));
        }

        StringBuilder result = new StringBuilder();

        int i = 0;

        while (i < n) {

            if (Character.isLetter(s.charAt(i))) {
                result.append(s.charAt(i));

            } else { // '('
                i++;

                StringBuilder temp = new StringBuilder();

                while (i < n && s.charAt(i) != ')') {
                    temp.append(s.charAt(i));
                    i++;
                }

                String key = temp.toString();

                if (mp.containsKey(key)) {
                    result.append(mp.get(key));
                } else {
                    result.append("?");
                }
            }

            i++;
        }

        return result.toString();
    }
}
```

---

## Python

```python
class Solution:
    def evaluate(self, s: str, knowledge: list[list[str]]) -> str:
        mp = {k: v for k, v in knowledge}

        result = []
        i, n = 0, len(s)

        while i < n:
            if s[i] == '(':
                i += 1
                temp = []
                while i < n and s[i] != ')':
                    temp.append(s[i])
                    i += 1
                key = ''.join(temp)
                result.append(mp.get(key, '?'))
            else:
                result.append(s[i])
            i += 1

        return ''.join(result)
```

---

## C++

```cpp
class Solution {
public:
    string evaluate(string s, vector<vector<string>>& knowledge) {
        unordered_map<string, string> mp;
        for (auto& vec : knowledge) {
            mp[vec[0]] = vec[1];
        }

        string result;
        int i = 0, n = s.length();

        while (i < n) {
            if (isalpha(s[i])) {
                result += s[i];
            } else { // '('
                i++;
                string key;
                while (i < n && s[i] != ')') {
                    key += s[i];
                    i++;
                }
                auto it = mp.find(key);
                result += (it != mp.end() ? it->second : "?");
            }
            i++;
        }

        return result;
    }
};
```

---

## C

```c
char* evaluate(char* s, char*** knowledge, int knowledgeSize, int* knowledgeColSize) {
    int n = strlen(s);
    char* result = (char*)malloc((2 * n + 1) * sizeof(char));
    int r = 0, i = 0;

    while (i < n) {
        if (isalpha(s[i])) {
            result[r++] = s[i];
        } else { // '('
            i++;
            char key[12];
            int k = 0;
            while (i < n && s[i] != ')') {
                key[k++] = s[i];
                i++;
            }
            key[k] = '\0';

            char* val = NULL;
            for (int j = 0; j < knowledgeSize; j++) {
                if (strcmp(knowledge[j][0], key) == 0) {
                    val = knowledge[j][1];
                    break;
                }
            }
            if (val) {
                int len = strlen(val);
                strcpy(result + r, val);
                r += len;
            } else {
                result[r++] = '?';
            }
        }
        i++;
    }
    result[r] = '\0';
    return result;
}
```
