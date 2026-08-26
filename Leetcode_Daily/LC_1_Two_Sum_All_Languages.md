# LeetCode 1 - Two Sum

Optimal O(n) HashMap solution. Works on both LeetCode and GeeksforGeeks.

---

## Java

```java
import java.util.*;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int current = nums[i];
            int required = target - current;
            if (map.containsKey(required)) {
                return new int[] {map.get(required), i};
            }
            map.put(current, i);
        }
        return new int[] {};
    }
}
```

---

## Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {}
        for i, current in enumerate(nums):
            required = target - current
            if required in seen:
                return [seen[required], i]
            seen[current] = i
        return []
```

---

## C++

```cpp
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> seen;
        for (int i = 0; i < nums.size(); i++) {
            int current = nums[i];
            int required = target - current;
            if (seen.count(required)) {
                return {seen[required], i};
            }
            seen[current] = i;
        }
        return {};
    }
};
```

---

## C

```c
#include <stdlib.h>

typedef struct Node {
    int key;
    int value;
    struct Node* next;
} Node;

typedef struct {
    Node* buckets[10007];
} HashMap;

static unsigned int hashKey(int key) {
    return ((unsigned int)key % 10007 + 10007) % 10007;
}

static void putMap(HashMap* m, int key, int value) {
    unsigned int h = hashKey(key);
    Node* n = m->buckets[h];
    while (n) {
        if (n->key == key) { n->value = value; return; }
        n = n->next;
    }
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->key = key;
    newNode->value = value;
    newNode->next = m->buckets[h];
    m->buckets[h] = newNode;
}

static int getMap(HashMap* m, int key) {
    unsigned int h = hashKey(key);
    Node* n = m->buckets[h];
    while (n) {
        if (n->key == key) return n->value;
        n = n->next;
    }
    return -1;
}

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    HashMap* map = (HashMap*)calloc(1, sizeof(HashMap));
    int* result = (int*)malloc(2 * sizeof(int));
    *returnSize = 2;
    for (int i = 0; i < numsSize; i++) {
        int current = nums[i];
        int required = target - current;
        if (getMap(map, required) != -1) {
            result[0] = getMap(map, required);
            result[1] = i;
            return result;
        }
        putMap(map, current, i);
    }
    return result;
}
```
