# LeetCode 301 - Remove Invalid Parentheses

**Problem Link:** https://leetcode.com/problems/remove-invalid-parentheses/

**Approach:** BFS level by level — each level removes exactly one parenthesis.
The first level that yields any valid string is the minimum-removal answer.

**Complexity:** Time O(2^n), Space O(2^n)

**Companies:** Meta, Amazon, Google, Microsoft, Bloomberg, Apple, Uber

---

## Java

```java
class Solution {

    public List<String> removeInvalidParentheses(String s) {

        List<String> answer = new ArrayList<>();

        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();

        queue.offer(s);
        visited.add(s);

        boolean found = false;

        while (!queue.isEmpty()) {

            int size = queue.size();

            // Process only the current BFS level
            for (int i = 0; i < size; i++) {

                String current = queue.poll();

                // Check whether current string is valid
                if (isValid(current)) {
                    answer.add(current);
                    found = true;
                }

                // If valid strings are found,
                // don't generate the next level
                if (found) {
                    continue;
                }

                // Remove one parenthesis
                for (int j = 0; j < current.length(); j++) {

                    char ch = current.charAt(j);

                    // We can remove only parentheses
                    if (ch != '(' && ch != ')') {
                        continue;
                    }

                    String next =
                            current.substring(0, j)
                            + current.substring(j + 1);

                    // Avoid duplicate strings
                    if (!visited.contains(next)) {
                        visited.add(next);
                        queue.offer(next);
                    }
                }
            }

            // First valid level = minimum removals
            if (found) {
                break;
            }
        }

        return answer;
    }

    private boolean isValid(String s) {

        int count = 0;

        for (char ch : s.toCharArray()) {

            if (ch == '(') {
                count++;
            }
            else if (ch == ')') {
                count--;

                // More closing brackets than opening brackets
                if (count < 0) {
                    return false;
                }
            }
        }

        // All opening brackets must also be matched
        return count == 0;
    }
}
```

---

## Python

```python
from collections import deque

class Solution:
    def removeInvalidParentheses(self, s: str) -> list[str]:
        def is_valid(t: str) -> bool:
            count = 0
            for ch in t:
                if ch == '(':
                    count += 1
                elif ch == ')':
                    count -= 1
                    # More closing brackets than opening brackets
                    if count < 0:
                        return False
            # All opening brackets must also be matched
            return count == 0

        answer = []
        queue = deque([s])
        visited = {s}
        found = False

        while queue:
            # Process only the current BFS level
            for _ in range(len(queue)):
                current = queue.popleft()

                # Check whether current string is valid
                if is_valid(current):
                    answer.append(current)
                    found = True

                # If valid strings are found,
                # don't generate the next level
                if found:
                    continue

                # Remove one parenthesis
                for j in range(len(current)):
                    ch = current[j]

                    # We can remove only parentheses
                    if ch != '(' and ch != ')':
                        continue

                    nxt = current[:j] + current[j + 1:]

                    # Avoid duplicate strings
                    if nxt not in visited:
                        visited.add(nxt)
                        queue.append(nxt)

            # First valid level = minimum removals
            if found:
                break

        return answer
```

---

## C++

```cpp
class Solution {
public:
    vector<string> removeInvalidParentheses(string s) {
        auto isValid = [](const string& t) {
            int count = 0;
            for (char ch : t) {
                if (ch == '(') {
                    count++;
                } else if (ch == ')') {
                    count--;
                    // More closing brackets than opening brackets
                    if (count < 0) return false;
                }
            }
            // All opening brackets must also be matched
            return count == 0;
        };

        vector<string> answer;
        queue<string> q;
        unordered_set<string> visited;
        q.push(s);
        visited.insert(s);
        bool found = false;

        while (!q.empty()) {
            int size = q.size();

            // Process only the current BFS level
            for (int i = 0; i < size; i++) {
                string current = q.front();
                q.pop();

                // Check whether current string is valid
                if (isValid(current)) {
                    answer.push_back(current);
                    found = true;
                }

                // If valid strings are found,
                // don't generate the next level
                if (found) continue;

                // Remove one parenthesis
                for (int j = 0; j < (int)current.size(); j++) {
                    char ch = current[j];

                    // We can remove only parentheses
                    if (ch != '(' && ch != ')') continue;

                    string nxt = current.substr(0, j) + current.substr(j + 1);

                    // Avoid duplicate strings
                    if (!visited.count(nxt)) {
                        visited.insert(nxt);
                        q.push(nxt);
                    }
                }
            }

            // First valid level = minimum removals
            if (found) break;
        }

        return answer;
    }
};
```

---

## C

```c
// isValid: counter check, never negative, ends at zero
static bool isValid301(char* t) {
    int count = 0;
    for (int i = 0; t[i] != '\0'; i++) {
        if (t[i] == '(') {
            count++;
        } else if (t[i] == ')') {
            count--;
            // More closing brackets than opening brackets
            if (count < 0) return false;
        }
    }
    // All opening brackets must also be matched
    return count == 0;
}

static char* copyStr301(const char* t) {
    size_t n = strlen(t);
    char* c = (char*)malloc(n + 1);
    strcpy(c, t);
    return c;
}

// BFS level by level; queue + visited set of owned strings
char** removeInvalidParentheses(char* s, int* returnSize) {
    int ansCap = 64;
    char** answer = (char**)malloc(sizeof(char*) * ansCap);
    int ansCount = 0;

    int qCap = 4096;
    char** q = (char**)malloc(sizeof(char*) * qCap);
    int qh = 0, qt = 0;

    int vCap = 8192;
    char** vis = (char**)malloc(sizeof(char*) * vCap);
    int vCount = 0;

    q[qt++] = copyStr301(s);
    vis[vCount++] = copyStr301(s);

    bool found = false;

    while (qh < qt) {
        int size = qt - qh;

        // Process only the current BFS level
        for (int i = 0; i < size; i++) {
            char* current = q[qh++];

            // Check whether current string is valid
            if (isValid301(current)) {
                if (ansCount == ansCap) {
                    ansCap *= 2;
                    answer = (char**)realloc(answer, sizeof(char*) * ansCap);
                }
                answer[ansCount++] = copyStr301(current);
                found = true;
            }

            // If valid strings are found,
            // don't generate the next level
            if (found) continue;

            int len = strlen(current);
            // Remove one parenthesis
            for (int j = 0; j < len; j++) {
                char ch = current[j];

                // We can remove only parentheses
                if (ch != '(' && ch != ')') continue;

                char* nxt = (char*)malloc(len); // len - 1 chars + terminator
                strncpy(nxt, current, j);
                strcpy(nxt + j, current + j + 1);

                // Avoid duplicate strings (linear scan, n is small)
                bool seen = false;
                for (int k = 0; k < vCount; k++) {
                    if (strcmp(vis[k], nxt) == 0) { seen = true; break; }
                }
                if (!seen) {
                    if (vCount == vCap) {
                        vCap *= 2;
                        vis = (char**)realloc(vis, sizeof(char*) * vCap);
                    }
                    vis[vCount++] = copyStr301(nxt);
                    if (qt == qCap) {
                        qCap *= 2;
                        q = (char**)realloc(q, sizeof(char*) * qCap);
                    }
                    q[qt++] = nxt;
                } else {
                    free(nxt);
                }
            }
        }

        // First valid level = minimum removals
        if (found) break;
    }

    *returnSize = ansCount;
    return answer;
}
```
