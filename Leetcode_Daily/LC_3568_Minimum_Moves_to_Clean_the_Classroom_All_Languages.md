# LeetCode 3568 - Minimum Moves to Clean the Classroom

## Problem Link
https://leetcode.com/problems/minimum-moves-to-clean-the-classroom/

## Approach
BFS with Bitmask DP. Track state as (row, col, energy, mask) where mask = bitmask of collected litter. BFS explores all valid moves; energy resets on 'R' cells; litter collected on 'L' cells via bitmask update. Return moves when mask == 0 (all collected), or -1 if impossible.

## Complexity
- Time: O(m × n × energy × 2^L) where L = number of litter cells
- Space: O(m × n × energy × 2^L)

---

## Java (Original)

```java
class Solution {

    static class State {
        int row;
        int col;
        int energy;
        int mask;

        State(int row, int col, int energy, int mask) {
            this.row = row;
            this.col = col;
            this.energy = energy;
            this.mask = mask;
        }
    }

    public int minMoves(String[] classroom, int energy) {

        int m = classroom.length;
        int n = classroom[0].length();

        int startRow = 0;
        int startCol = 0;
        int totalLitter = 0;

        int[][] litterNumber = new int[m][n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                litterNumber[i][j] = -1;
            }
        }

        // Find S and give every L a number
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                char cell = classroom[i].charAt(j);

                if (cell == 'S') {
                    startRow = i;
                    startCol = j;
                }

                if (cell == 'L') {
                    litterNumber[i][j] = totalLitter;
                    totalLitter++;
                }
            }
        }

        int allCollected = (1 << totalLitter) - 1;

        Queue<State> queue = new LinkedList<>();

        queue.offer(new State(startRow, startCol, energy, 0));

        boolean[][][][] visited =
            new boolean[m][n][energy + 1][1 << totalLitter];

        visited[startRow][startCol][energy][0] = true;

        int[][] directions = {
            {1, 0},
            {-1, 0},
            {0, 1},
            {0, -1}
        };

        int moves = 0;

        while (!queue.isEmpty()) {

            int size = queue.size();

            while (size-- > 0) {

                State current = queue.poll();

                if (current.mask == allCollected) {
                    return moves;
                }

                if (current.energy == 0) {
                    continue;
                }

                for (int[] direction : directions) {

                    int newRow = current.row + direction[0];
                    int newCol = current.col + direction[1];

                    if (newRow < 0 || newRow >= m ||
                        newCol < 0 || newCol >= n) {
                        continue;
                    }

                    if (classroom[newRow].charAt(newCol) == 'X') {
                        continue;
                    }

                    int newEnergy = current.energy - 1;
                    int newMask = current.mask;

                    char cell = classroom[newRow].charAt(newCol);

                    // Litter collected
                    if (cell == 'L') {
                        int litterNumberAtCell =
                            litterNumber[newRow][newCol];

                        newMask |= (1 << litterNumberAtCell);
                    }

                    // Energy reset
                    if (cell == 'R') {
                        newEnergy = energy;
                    }

                    if (visited[newRow][newCol][newEnergy][newMask]) {
                        continue;
                    }

                    visited[newRow][newCol][newEnergy][newMask] = true;

                    queue.offer(
                        new State(
                            newRow,
                            newCol,
                            newEnergy,
                            newMask
                        )
                    );
                }
            }

            moves++;
        }

        return -1;
    }
}
```

---

## Python

```python
from collections import deque
from typing import List

class Solution:
    def minMoves(self, classroom: List[str], energy: int) -> int:
        m, n = len(classroom), len(classroom[0])

        start_row = start_col = total_litter = 0
        litter_number = [[-1] * n for _ in range(m)]

        for i in range(m):
            for j in range(n):
                cell = classroom[i][j]
                if cell == 'S':
                    start_row, start_col = i, j
                elif cell == 'L':
                    litter_number[i][j] = total_litter
                    total_litter += 1

        all_collected = (1 << total_litter) - 1
        visited = [[[[False] * (1 << total_litter)
                      for _ in range(energy + 1)]
                      for _ in range(n)]
                      for _ in range(m)]

        queue = deque([(start_row, start_col, energy, 0)])
        visited[start_row][start_col][energy][0] = True
        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
        moves = 0

        while queue:
            for _ in range(len(queue)):
                row, col, cur_energy, mask = queue.popleft()
                if mask == all_collected:
                    return moves
                if cur_energy == 0:
                    continue
                for dr, dc in directions:
                    nr, nc = row + dr, col + dc
                    if 0 <= nr < m and 0 <= nc < n and classroom[nr][nc] != 'X':
                        new_energy = cur_energy - 1
                        new_mask = mask
                        cell = classroom[nr][nc]
                        if cell == 'L':
                            new_mask |= (1 << litter_number[nr][nc])
                        if cell == 'R':
                            new_energy = energy
                        if not visited[nr][nc][new_energy][new_mask]:
                            visited[nr][nc][new_energy][new_mask] = True
                            queue.append((nr, nc, new_energy, new_mask))
            moves += 1
        return -1
```

---

## C++

```cpp
#include <vector>
#include <string>
#include <queue>
#include <tuple>
using namespace std;

class Solution {
public:
    int minMoves(vector<string>& classroom, int energy) {
        int m = classroom.size(), n = classroom[0].size();
        vector<vector<int>> d(m, vector<int>(n, 0));
        int x = 0, y = 0, cnt = 0;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                char c = classroom[i][j];
                if (c == 'S') { x = i; y = j; }
                else if (c == 'L') { d[i][j] = cnt++; }
            }
        }
        if (cnt == 0) return 0;
        vector<vector<vector<vector<bool>>>> vis(
            m, vector<vector<vector<bool>>>(
                n, vector<vector<bool>>(
                    energy + 1, vector<bool>(1 << cnt, false))));
        queue<tuple<int,int,int,int>> q;
        q.emplace(x, y, energy, (1 << cnt) - 1);
        vis[x][y][energy][(1 << cnt) - 1] = true;
        vector<int> dirs = {-1, 0, 1, 0, -1};
        int ans = 0;
        while (!q.empty()) {
            int sz = q.size();
            while (sz--) {
                auto [i, j, cur_energy, mask] = q.front(); q.pop();
                if (mask == 0) return ans;
                if (cur_energy <= 0) continue;
                for (int k = 0; k < 4; ++k) {
                    int nx = i + dirs[k], ny = j + dirs[k+1];
                    if (nx >= 0 && nx < m && ny >= 0 && ny < n && classroom[nx][ny] != 'X') {
                        int nxt_energy = classroom[nx][ny] == 'R' ? energy : cur_energy - 1;
                        int nxt_mask = mask;
                        if (classroom[nx][ny] == 'L')
                            nxt_mask &= ~(1 << d[nx][ny]);
                        if (!vis[nx][ny][nxt_energy][nxt_mask]) {
                            vis[nx][ny][nxt_energy][nxt_mask] = true;
                            q.emplace(nx, ny, nxt_energy, nxt_mask);
                        }
                    }
                }
            }
            ans++;
        }
        return -1;
    }
};
```

---

## C

```c
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

typedef struct { int row, col, energy, mask; } State;

int minMoves(char** classroom, int classroomSize, int energy) {
    int m = classroomSize, n = strlen(classroom[0]);
    int** d = malloc(m * sizeof(int*));
    int x = 0, y = 0, cnt = 0;
    for (int i = 0; i < m; i++) {
        d[i] = calloc(n, sizeof(int));
        for (int j = 0; j < n; j++) {
            d[i][j] = -1;
            if (classroom[i][j] == 'S') { x = i; y = j; }
            else if (classroom[i][j] == 'L') { d[i][j] = cnt++; }
        }
    }
    if (cnt == 0) { for (int i = 0; i < m; i++) free(d[i]); free(d); return 0; }

    bool**** vis = malloc(m * sizeof(bool***));
    for (int i = 0; i < m; i++) {
        vis[i] = malloc(n * sizeof(bool**));
        for (int j = 0; j < n; j++) {
            vis[i][j] = malloc((energy + 1) * sizeof(bool*));
            for (int e = 0; e <= energy; e++) {
                vis[i][j][e] = calloc(1 << cnt, sizeof(bool));
            }
        }
    }

    int capacity = m * n * energy * (1 << cnt);
    State* q = malloc(capacity * sizeof(State));
    int head = 0, tail = 0;
    int allCollected = (1 << cnt) - 1;
    q[tail++] = (State){x, y, energy, 0};
    vis[x][y][energy][0] = true;
    int dirs[] = {-1, 0, 1, 0, -1};
    int moves = 0;

    while (head < tail) {
        int size = tail - head;
        while (size-- > 0) {
            State cur = q[head++];
            if (cur.mask == allCollected) goto done;
            if (cur.energy == 0) continue;
            for (int k = 0; k < 4; k++) {
                int nr = cur.row + dirs[k], nc = cur.col + dirs[k + 1];
                if (nr < 0 || nr >= m || nc < 0 || nc >= n) continue;
                if (classroom[nr][nc] == 'X') continue;
                int ne = cur.energy - 1, nm = cur.mask;
                if (classroom[nr][nc] == 'L') nm |= (1 << d[nr][nc]);
                if (classroom[nr][nc] == 'R') ne = energy;
                if (!vis[nr][nc][ne][nm]) {
                    vis[nr][nc][ne][nm] = true;
                    q[tail++] = (State){nr, nc, ne, nm};
                }
            }
        }
        moves++;
    }
    moves = -1;
done:
    free(q);
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            for (int e = 0; e <= energy; e++) free(vis[i][j][e]);
            free(vis[i][j]);
        }
        free(vis[i]); free(d[i]);
    }
    free(vis); free(d);
    return moves;
}
```
