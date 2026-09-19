# LeetCode 1401 - Circle and Rectangle Overlapping

**Problem Links:**
- LeetCode: https://leetcode.com/problems/circle-and-rectangle-overlapping/description/

**Companies:** Google, Amazon
**Tags:** Geometry, Math
**Difficulty:** Medium
**Source:** Biweekly Contest 23 Q3

---

## Approach: Nearest Point Clamping (O(1))

Find the closest point on the rectangle to the circle's center by clamping.
If the squared distance from that point to the center is <= radius², they overlap.
Time: O(1) | Space: O(1)

---

## Java

```java
class Solution {    public boolean checkOverlap(int radius, int xCenter, int yCenter,
                                int x1, int y1, int x2, int y2) {

        // nearest point
        int xn;
        int yn;


        if (x1 > xCenter) {
            xn = x1;
        } else if (x2 < xCenter) {
            xn = x2;
        } else {
            xn = xCenter;
        }


        if (y1 > yCenter) {
            yn = y1;
        } else if (y2 < yCenter) {
            yn = y2;
        } else {
            yn = yCenter;
        }


        return (xn - xCenter) * (xn - xCenter)
             + (yn - yCenter) * (yn - yCenter)
             <= radius * radius;
    }
}
```

---

## Python

```python
class Solution:
    def checkOverlap(self, radius: int, xCenter: int, yCenter: int,
                     x1: int, y1: int, x2: int, y2: int) -> bool:
        # Find closest point on rectangle to circle center
        closestX = max(x1, min(x2, xCenter))
        closestY = max(y1, min(y2, yCenter))
        # Check squared distance vs radius squared
        distSq = (closestX - xCenter) ** 2 + (closestY - yCenter) ** 2
        return distSq <= radius * radius
```

---

## C++

```cpp
class Solution {
public:
    bool checkOverlap(int radius, int xCenter, int yCenter,
                      int x1, int y1, int x2, int y2) {
        // Find closest point on rectangle to circle center
        int closestX = max(x1, min(x2, xCenter));
        int closestY = max(y1, min(y2, yCenter));
        // Check squared distance vs radius squared
        long distSq = (long)(closestX - xCenter) * (closestX - xCenter)
                    + (long)(closestY - yCenter) * (closestY - yCenter);
        return distSq <= (long)radius * radius;
    }
};
```

---

## C

```c
bool checkOverlap(int radius, int xCenter, int yCenter,
                  int x1, int y1, int x2, int y2) {
    // Find closest point on rectangle to circle center
    int closestX = (x1 > xCenter) ? x1 : ((x2 < xCenter) ? x2 : xCenter);
    int closestY = (y1 > yCenter) ? y1 : ((y2 < yCenter) ? y2 : yCenter);
    // Check squared distance vs radius squared
    long distSq = (long)(closestX - xCenter) * (closestX - xCenter)
                + (long)(closestY - yCenter) * (closestY - yCenter);
    return distSq <= (long)radius * radius;
}
```
