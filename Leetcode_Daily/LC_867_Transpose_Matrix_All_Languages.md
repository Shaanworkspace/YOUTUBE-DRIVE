# LeetCode 867 - Transpose Matrix

**Problem Link:** https://leetcode.com/problems/transpose-matrix/

**Approach:** Create a new matrix where rows become columns and columns become rows. For an `r x c` matrix, the transpose is a `c x r` matrix where `result[j][i] = matrix[i][j]`.

**Complexity:**
- Time: O(r * c) — single pass through all elements
- Space: O(r * c) — new matrix for the result

---

## Java

```java
class Solution {
    public int[][] transpose(int[][] matrix) {
        int r = matrix.length;
        int c = matrix[0].length;
        int[][] result = new int[c][r];

        for(int i = 0; i < r; i++){
            for(int j = 0; j < c; j++){
                result[j][i] = matrix[i][j];
            }
        }

        return result;
    }
}
```

---

## Python

```python
class Solution:
    def transpose(self, matrix: list[list[int]]) -> list[list[int]]:
        r, c = len(matrix), len(matrix[0])
        return [[matrix[i][j] for i in range(r)] for j in range(c)]
```

---

## C++

```cpp
class Solution {
public:
    vector<vector<int>> transpose(vector<vector<int>>& matrix) {
        int r = matrix.size();
        int c = matrix[0].size();
        vector<vector<int>> result(c, vector<int>(r));

        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                result[j][i] = matrix[i][j];
            }
        }

        return result;
    }
};
```

---

## C

```c
/**
 * Return an array of arrays of size *returnSize.
 * The returned array must be malloced, assume caller calls free().
 */
int** transpose(int** matrix, int matrixSize, int* matrixColSize, int* returnSize, int** returnColumnSizes) {
    int r = matrixSize;
    int c = matrixColSize[0];
    *returnSize = c;
    *returnColumnSizes = (int*)malloc(c * sizeof(int));

    int** result = (int**)malloc(c * sizeof(int*));
    for (int j = 0; j < c; j++) {
        result[j] = (int*)malloc(r * sizeof(int));
        (*returnColumnSizes)[j] = r;
        for (int i = 0; i < r; i++) {
            result[j][i] = matrix[i][j];
        }
    }

    return result;
}
```
