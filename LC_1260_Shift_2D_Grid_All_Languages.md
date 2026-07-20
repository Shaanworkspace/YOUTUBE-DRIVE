# LeetCode 1260 - Shift 2D Grid

## Java

```java
import java.util.*;

class Solution {

    private void rotate(int[] arr, int k) {

        int n = arr.length;
        k %= n;

        reverse(arr, 0, n - 1);
        reverse(arr, 0, k - 1);
        reverse(arr, k, n - 1);
    }

    private void reverse(int[] arr, int left, int right) {

        while (left < right) {

            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }
    }

    public List<List<Integer>> shiftGrid(int[][] grid, int k) {

        int m = grid.length;
        int n = grid[0].length;

        int[] arr = new int[m * n];

        int idx = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                arr[idx++] = grid[i][j];
            }
        }

        rotate(arr, k);

        idx = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = arr[idx++];
            }
        }

        List<List<Integer>> ans = new ArrayList<>();

        for (int i = 0; i < m; i++) {

            ans.add(new ArrayList<>());

            for (int j = 0; j < n; j++) {
                ans.get(i).add(grid[i][j]);
            }
        }

        return ans;
    }
}
```

---

## Python

```python
class Solution:

    def rotate(self, arr, k):

        n = len(arr)
        k %= n

        arr.reverse()
        arr[:k] = reversed(arr[:k])
        arr[k:] = reversed(arr[k:])

    def shiftGrid(self, grid: list[list[int]], k: int) -> list[list[int]]:

        m = len(grid)
        n = len(grid[0])

        arr = []

        for row in grid:
            arr.extend(row)

        self.rotate(arr, k)

        idx = 0

        for i in range(m):
            for j in range(n):
                grid[i][j] = arr[idx]
                idx += 1

        return grid
```

---

## C++

```cpp
class Solution {
public:

    void reverse(vector<int>& arr, int left, int right) {

        while (left < right) {

            swap(arr[left], arr[right]);

            left++;
            right--;
        }
    }

    void rotate(vector<int>& arr, int k) {

        int n = arr.size();
        k %= n;

        reverse(arr, 0, n - 1);
        reverse(arr, 0, k - 1);
        reverse(arr, k, n - 1);
    }

    vector<vector<int>> shiftGrid(vector<vector<int>>& grid, int k) {

        int m = grid.size();
        int n = grid[0].size();

        vector<int> arr;

        for (auto& row : grid)
            for (int num : row)
                arr.push_back(num);

        rotate(arr, k);

        int idx = 0;

        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                grid[i][j] = arr[idx++];

        return grid;
    }
};
```

---

## C

```c
#include <stdlib.h>

void reverse(int* arr, int left, int right) {

    while (left < right) {

        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        left++;
        right--;
    }
}

void rotate(int* arr, int size, int k) {

    k %= size;

    reverse(arr, 0, size - 1);
    reverse(arr, 0, k - 1);
    reverse(arr, k, size - 1);
}

int** shiftGrid(int** grid, int gridSize, int* gridColSize, int k,
                int* returnSize, int** returnColumnSizes) {

    int m = gridSize;
    int n = gridColSize[0];

    int size = m * n;

    int* arr = (int*)malloc(sizeof(int) * size);

    int idx = 0;

    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            arr[idx++] = grid[i][j];

    rotate(arr, size, k);

    int** ans = (int**)malloc(sizeof(int*) * m);
    *returnColumnSizes = (int*)malloc(sizeof(int) * m);

    idx = 0;

    for (int i = 0; i < m; i++) {

        ans[i] = (int*)malloc(sizeof(int) * n);
        (*returnColumnSizes)[i] = n;

        for (int j = 0; j < n; j++) {
            ans[i][j] = arr[idx++];
        }
    }

    *returnSize = m;

    free(arr);

    return ans;
}
```