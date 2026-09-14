# LeetCode 836 - Rectangle Overlap

**Problem Link:** https://leetcode.com/problems/rectangle-overlap/

**Companies:** Amazon, Adobe, Meta (Facebook), Docusign

**Approach:** Common width and height method — two rectangles overlap if and only if their projections overlap on both axes with positive length. Common width = min(r1[2], r2[2]) - max(r1[0], r2[0]), common height = min(r1[3], r2[3]) - max(r1[1], r2[1]). Return true only when both width > 0 and height > 0. Touching edges or separate rectangles give non-positive width or height.
Time: O(1) | Space: O(1)

---

## Java

```java
class Solution {
    public boolean isRectangleOverlap(int[] rec1, int[] rec2) {
        int width = Math.min(rec1[2], rec2[2]) - Math.max(rec1[0], rec2[0]);
        int height = Math.min(rec1[3], rec2[3]) - Math.max(rec1[1], rec2[1]);
        return width > 0 && height > 0;
    }
}
```

---

## Python

```python
class Solution:
    def isRectangleOverlap(self, rec1: list[int], rec2: list[int]) -> bool:
        width = min(rec1[2], rec2[2]) - max(rec1[0], rec2[0])
        height = min(rec1[3], rec2[3]) - max(rec1[1], rec2[1])
        return width > 0 and height > 0
```

---

## C++

```cpp
class Solution {
public:
    bool isRectangleOverlap(vector<int>& rec1, vector<int>& rec2) {
        int width = min(rec1[2], rec2[2]) - max(rec1[0], rec2[0]);
        int height = min(rec1[3], rec2[3]) - max(rec1[1], rec2[1]);
        return width > 0 && height > 0;
    }
};
```

---

## C

```c
bool isRectangleOverlap(int* rec1, int rec1Size, int* rec2, int rec2Size) {
    int width = (rec1[2] < rec2[2] ? rec1[2] : rec2[2]) - (rec1[0] > rec2[0] ? rec1[0] : rec2[0]);
    int height = (rec1[3] < rec2[3] ? rec1[3] : rec2[3]) - (rec1[1] > rec2[1] ? rec1[1] : rec2[1]);
    return width > 0 && height > 0;
}
```
