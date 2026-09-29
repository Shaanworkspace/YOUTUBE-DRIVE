# LeetCode 2267 - Check if There Is a Valid Parentheses String Path

**Problem Link:**
- LeetCode: https://leetcode.com/problems/check-if-there-is-a-valid-parentheses-string-path/description

**Companies:** Google, Amazon, Meta

**Approach:** BFS with balance state (No Recursion, No DP table recursion). Track (row, col, balance) in a queue. Prune negative balance, odd path length, wrong start/end brackets. Visited 3D array stops repeated states.

**Complexity:** Time O(m * n * (m + n)), Space O(m * n * (m + n))

---

## Java

```java
import java.util.*;

class Solution {
    public boolean hasValidPath(char[][] grid) {


        int m = grid.length;
        int n = grid[0].length;


        // Total path length must be even
        if ((m + n - 1) % 2 != 0) {
            return false;
        }


        // First character must be '('
        if (grid[0][0] == ')') {
            return false;
        }


        Queue<int[]> queue = new LinkedList<>();


        // {row, col, balance}
        queue.offer(new int[]{0, 0, 1});


        // visited[row][col][balance]
        boolean[][][] visited = new boolean[m][n][m + n];


        visited[0][0][1] = true;


        int[][] directions = {
            {1, 0},  // down
            {0, 1}   // right
        };


        while (!queue.isEmpty()) {


            int[] current = queue.poll();


            int row = current[0];
            int col = current[1];
            int balance = current[2];


            // Reached destination
            if (row == m - 1 && col == n - 1) {
                if (balance == 0) {
                    return true;
                }
            }


            for (int[] dir : directions) {


                int newRow = row + dir[0];
                int newCol = col + dir[1];


                // Out of bounds
                if (newRow >= m || newCol >= n) {
                    continue;
                }


                int newBalance = balance;


                if (grid[newRow][newCol] == '(') {
                    newBalance++;
                } else {
                    newBalance--;
                }


                // Invalid prefix
                if (newBalance < 0) {
                    continue;
                }


                // Already visited same state
                if (visited[newRow][newCol][newBalance]) {
                    continue;
                }


                visited[newRow][newCol][newBalance] = true;


                queue.offer(new int[]{
                    newRow,
                    newCol,
                    newBalance
                });
            }
        }


        return false;
    }
}
```

---

## Python

```python
from collections import deque

class Solution:
    def hasValidPath(self, grid: list[list[str]]) -> bool:
        m, n = len(grid), len(grid[0])

        # Total path length must be even
        if (m + n - 1) % 2 != 0:
            return False

        # First character must be '('
        if grid[0][0] == ')':
            return False

        # queue stores (row, col, balance)
        queue = deque()
        queue.append((0, 0, 1))

        # visited[row][col][balance]
        visited = [[[False] * (m + n) for _ in range(n)] for _ in range(m)]
        visited[0][0][1] = True

        directions = [(1, 0), (0, 1)]  # down, right

        while queue:
            row, col, balance = queue.popleft()

            # Reached destination
            if row == m - 1 and col == n - 1:
                if balance == 0:
                    return True

            for dr, dc in directions:
                newRow, newCol = row + dr, col + dc

                # Out of bounds
                if newRow >= m or newCol >= n:
                    continue

                newBalance = balance + 1 if grid[newRow][newCol] == '(' else balance - 1

                # Invalid prefix
                if newBalance < 0:
                    continue

                # Already visited same state
                if visited[newRow][newCol][newBalance]:
                    continue

                visited[newRow][newCol][newBalance] = True
                queue.append((newRow, newCol, newBalance))

        return False
```

---

## C++

```cpp
#include <vector>
#include <queue>
#include <tuple>
using namespace std;

class Solution {
public:
    bool hasValidPath(vector<vector<char>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        // Total path length must be even
        if ((m + n - 1) % 2 != 0) return false;

        // First character must be '('
        if (grid[0][0] == ')') return false;

        // queue stores {row, col, balance}
        queue<tuple<int, int, int>> q;
        q.push({0, 0, 1});

        // visited[row][col][balance]
        vector<vector<vector<bool>>> visited(
            m, vector<vector<bool>>(n, vector<bool>(m + n, false)));
        visited[0][0][1] = true;

        int dirs[2][2] = {{1, 0}, {0, 1}};  // down, right

        while (!q.empty()) {
            auto [row, col, balance] = q.front();
            q.pop();

            // Reached destination
            if (row == m - 1 && col == n - 1) {
                if (balance == 0) return true;
            }

            for (auto& d : dirs) {
                int newRow = row + d[0];
                int newCol = col + d[1];

                // Out of bounds
                if (newRow >= m || newCol >= n) continue;

                int newBalance = balance + (grid[newRow][newCol] == '(' ? 1 : -1);

                // Invalid prefix
                if (newBalance < 0) continue;

                // Already visited same state
                if (visited[newRow][newCol][newBalance]) continue;

                visited[newRow][newCol][newBalance] = true;
                q.push({newRow, newCol, newBalance});
            }
        }

        return false;
    }
};
```

---

## C

```c
#include <stdbool.h>
#include <stdlib.h>

bool hasValidPath(char** grid, int gridSize, int* gridColSize) {
    int m = gridSize;
    int n = gridColSize[0];

    // Total path length must be even
    if ((m + n - 1) % 2 != 0) return false;

    // First character must be '('
    if (grid[0][0] == ')') return false;

    int maxBal = m + n;

    // visited[m][n][maxBal] flattened
    bool* visited = (bool*)calloc(m * n * maxBal, sizeof(bool));

    // Simple array queue: stores row, col, balance
    int cap = m * n * maxBal + 5;
    int* qr = (int*)malloc(cap * sizeof(int));
    int* qc = (int*)malloc(cap * sizeof(int));
    int* qb = (int*)malloc(cap * sizeof(int));
    int front = 0, back = 0;

    qr[back] = 0; qc[back] = 0; qb[back] = 1; back++;
    visited[(0 * n + 0) * maxBal + 1] = true;

    int dirs[2][2] = {{1, 0}, {0, 1}};  // down, right

    while (front < back) {
        int row = qr[front], col = qc[front], balance = qb[front];
        front++;

        // Reached destination
        if (row == m - 1 && col == n - 1) {
            if (balance == 0) {
                free(visited); free(qr); free(qc); free(qb);
                return true;
            }
        }

        for (int d = 0; d < 2; d++) {
            int newRow = row + dirs[d][0];
            int newCol = col + dirs[d][1];

            // Out of bounds
            if (newRow >= m || newCol >= n) continue;

            int newBalance = balance + (grid[newRow][newCol] == '(' ? 1 : -1);

            // Invalid prefix
            if (newBalance < 0) continue;

            int idx = (newRow * n + newCol) * maxBal + newBalance;
            if (visited[idx]) continue;

            visited[idx] = true;
            qr[back] = newRow; qc[back] = newCol; qb[back] = newBalance;
            back++;
        }
    }

    free(visited); free(qr); free(qc); free(qb);
    return false;
}
```
