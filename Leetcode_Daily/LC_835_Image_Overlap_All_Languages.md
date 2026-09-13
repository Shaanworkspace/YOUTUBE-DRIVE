# LeetCode 835 - Image Overlap

**Problem Link:** https://leetcode.com/problems/image-overlap/

**Companies:** Google, Microsoft

**Approach:** Brute force — try all possible shifts (horizontal + vertical) and count overlapping 1s.
Time: O(n^4) | Space: O(1)

---

## Java

```java
class Solution {
    public int largestOverlap(int[][] img1, int[][] img2) {
        int n = img1.length;
        int answer = 0;

        for (int down = -(n - 1); down <= n - 1; down++) {
            for (int right = -(n - 1); right <= n - 1; right++) {
                int count = 0;

                for (int row = 0; row < n; row++) {
                    for (int col = 0; col < n; col++) {
                        if (img1[row][col] == 1) {
                            int newRow = row + down;
                            int newCol = col + right;

                            if (newRow >= 0 && newRow < n &&
                                newCol >= 0 && newCol < n &&
                                img2[newRow][newCol] == 1) {
                                count++;
                            }
                        }
                    }
                }

                answer = Math.max(answer, count);
            }
        }

        return answer;
    }
}
```

---

## Python

```python
class Solution:
    def largestOverlap(self, img1: list[list[int]], img2: list[list[int]]) -> int:
        n = len(img1)
        answer = 0

        for down in range(-(n - 1), n):
            for right in range(-(n - 1), n):
                count = 0

                for row in range(n):
                    for col in range(n):
                        if img1[row][col] == 1:
                            new_row = row + down
                            new_col = col + right

                            if 0 <= new_row < n and 0 <= new_col < n and img2[new_row][new_col] == 1:
                                count += 1

                answer = max(answer, count)

        return answer
```

---

## C++

```cpp
class Solution {
public:
    int largestOverlap(vector<vector<int>>& img1, vector<vector<int>>& img2) {
        int n = img1.size();
        int answer = 0;

        for (int down = -(n - 1); down <= n - 1; down++) {
            for (int right = -(n - 1); right <= n - 1; right++) {
                int count = 0;

                for (int row = 0; row < n; row++) {
                    for (int col = 0; col < n; col++) {
                        if (img1[row][col] == 1) {
                            int newRow = row + down;
                            int newCol = col + right;

                            if (newRow >= 0 && newRow < n &&
                                newCol >= 0 && newCol < n &&
                                img2[newRow][newCol] == 1) {
                                count++;
                            }
                        }
                    }
                }

                answer = max(answer, count);
            }
        }

        return answer;
    }
};
```

---

## C

```c
int largestOverlap(int** img1, int img1Size, int* img1ColSize, int** img2, int img2Size, int* img2ColSize) {
    int n = img1Size;
    int answer = 0;

    for (int down = -(n - 1); down <= n - 1; down++) {
        for (int right = -(n - 1); right <= n - 1; right++) {
            int count = 0;

            for (int row = 0; row < n; row++) {
                for (int col = 0; col < n; col++) {
                    if (img1[row][col] == 1) {
                        int newRow = row + down;
                        int newCol = col + right;

                        if (newRow >= 0 && newRow < n &&
                            newCol >= 0 && newCol < n &&
                            img2[newRow][newCol] == 1) {
                            count++;
                        }
                    }
                }
            }

            if (count > answer) answer = count;
        }
    }

    return answer;
}
```
