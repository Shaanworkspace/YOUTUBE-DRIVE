# LeetCode 2058 - Find the Minimum and Maximum Number of Nodes Between Critical Points

**Problem:** [LeetCode 2058](https://leetcode.com/problems/find-the-minimum-and-maximum-number-of-nodes-between-critical-points/)
**Difficulty:** Medium
**Topics:** Linked List

## Solution 1 — O(1) Space (Optimal)

Single-pass approach tracking first and previous critical points without storing all indices.

**Time Complexity:** O(n)
**Space Complexity:** O(1)

---

## Java (Verbatim)

```java
class Solution {
    public int[] nodesBetweenCriticalPoints(ListNode head) {
        int firstCriticalIndex = -1;
        int previousCriticalIndex = -1;

        int minDistance = Integer.MAX_VALUE;

        int index = 1;

        ListNode previous = head;
        ListNode current = head.next;

        while (current.next != null) {

            ListNode next = current.next;

            boolean isMaximum =
                current.val > previous.val &&
                current.val > next.val;

            boolean isMinimum =
                current.val < previous.val &&
                current.val < next.val;

            if (isMaximum || isMinimum) {

                if (firstCriticalIndex == -1) {

                    firstCriticalIndex = index;

                } else {

                    int distance = index - previousCriticalIndex;

                    minDistance = Math.min(minDistance, distance);
                }

                previousCriticalIndex = index;
            }

            previous = current;
            current = next;
            index++;
        }

        if (firstCriticalIndex == previousCriticalIndex) {
            return new int[]{-1, -1};
        }

        int maxDistance =
            previousCriticalIndex - firstCriticalIndex;


        return new int[]{minDistance, maxDistance};
    }
}
```

---

## Python

```python
class Solution:
    def nodesBetweenCriticalPoints(self, head: Optional[ListNode]) -> List[int]:
        first_critical = -1
        prev_critical = -1
        min_dist = float("inf")

        idx = 1
        prev = head
        curr = head.next

        while curr.next:
            nxt = curr.next

            is_max = curr.val > prev.val and curr.val > nxt.val
            is_min = curr.val < prev.val and curr.val < nxt.val

            if is_max or is_min:
                if first_critical == -1:
                    first_critical = idx
                else:
                    min_dist = min(min_dist, idx - prev_critical)
                prev_critical = idx

            prev = curr
            curr = nxt
            idx += 1

        if first_critical == prev_critical:
            return [-1, -1]

        max_dist = prev_critical - first_critical
        return [min_dist, max_dist]
```

---

## C++

```cpp
class Solution {
public:
    vector<int> nodesBetweenCriticalPoints(ListNode* head) {
        int firstCritical = -1;
        int prevCritical = -1;
        int minDist = INT_MAX;

        int idx = 1;
        ListNode* prev = head;
        ListNode* curr = head->next;

        while (curr->next) {
            ListNode* nxt = curr->next;

            bool isMax = curr->val > prev->val && curr->val > nxt->val;
            bool isMin = curr->val < prev->val && curr->val < nxt->val;

            if (isMax || isMin) {
                if (firstCritical == -1) {
                    firstCritical = idx;
                } else {
                    minDist = min(minDist, idx - prevCritical);
                }
                prevCritical = idx;
            }

            prev = curr;
            curr = nxt;
            idx++;
        }

        if (firstCritical == prevCritical) {
            return {-1, -1};
        }

        int maxDist = prevCritical - firstCritical;
        return {minDist, maxDist};
    }
};
```

---

## C

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
int* nodesBetweenCriticalPoints(struct ListNode* head, int* returnSize) {
    *returnSize = 2;
    int* result = (int*)malloc(2 * sizeof(int));

    int firstCritical = -1;
    int prevCritical = -1;
    int minDist = INT_MAX;

    int idx = 1;
    struct ListNode* prev = head;
    struct ListNode* curr = head->next;

    while (curr->next) {
        struct ListNode* nxt = curr->next;

        int isMax = (curr->val > prev->val && curr->val > nxt->val);
        int isMin = (curr->val < prev->val && curr->val < nxt->val);

        if (isMax || isMin) {
            if (firstCritical == -1) {
                firstCritical = idx;
            } else {
                int dist = idx - prevCritical;
                if (dist < minDist) minDist = dist;
            }
            prevCritical = idx;
        }

        prev = curr;
        curr = nxt;
        idx++;
    }

    if (firstCritical == prevCritical) {
        result[0] = -1;
        result[1] = -1;
    } else {
        result[0] = minDist;
        result[1] = prevCritical - firstCritical;
    }

    return result;
}
```

---
