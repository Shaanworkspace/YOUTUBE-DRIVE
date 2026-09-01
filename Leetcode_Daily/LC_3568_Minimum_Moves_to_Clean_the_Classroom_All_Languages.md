# LeetCode 3568 - Minimum Moves to Clean the Classroom

Problem: https://leetcode.com/problems/minimum-moves-to-clean-the-classroom/description/
Companies that ask this: Bloomberg.

## Intuition
Each cell is 'S' (start), 'L' (litter to collect), 'R' (energy reset), 'X' (obstacle), or '.' (empty).
Starting from 'S' with a fixed energy budget, every move costs 1 energy. Landing on 'R' restores
energy to full. We must collect all 'L' cells and return the minimum moves, or -1 if impossible.
Because there are at most 10 litter cells, we can represent the set of collected litter as a bitmask
and run a BFS over the state (row, col, energy, mask). The first time the mask becomes all-ones
(all litter collected) is the answer.

## Approach
1. Scan the grid: locate 'S', assign each 'L' a distinct bit index, compute `allCollected = (1 << totalLitter) - 1`.
2. BFS with state (row, col, energy, mask). `visited[row][col][energy][mask]` avoids revisiting.
3. From a state, try all four directions:
   - Out of bounds or 'X' → skip.
   - New energy = current energy - 1. If landing on 'R', reset to full `energy`.
   - New mask: if landing on 'L', set its bit.
   - If the new state is unvisited, push it.
4. Process level-by-level so `moves` equals the current BFS depth. Return `moves` when mask == allCollected.
5. If the queue empties, return -1.

Time: O(m * n * energy * 2^litter). Space: O(m * n * energy * 2^litter).

---

## Java

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
from typing import List
from collections import deque

class Solution:
    def minMoves(self, classroom: List[str], energy: int) -> int:
        m, n = len(classroom), len(classroom[0])
        start_row = start_col = total_litter = 0
        litter_number = [[-1] * n for _ in range(m)]
        for i in range(m):
            for j in range(n):
                if classroom[i][j] == 'S':
                    start_row, start_col = i, j
                elif classroom[i][j] == 'L':
                    litter_number[i][j] = total_litter
                    total_litter += 1
        all_collected = (1 << total_litter) - 1
        queue = deque([(start_row, start_col, energy, 0)])
        visited = [
            [[
                [False] * (1 << total_litter)
                for _ in range(energy + 1)
            ] for _ in range(n)]
            for _ in range(m)
        ]
        visited[start_row][start_col][energy][0] = True
        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
        moves = 0
        while queue:
            for _ in range(len(queue)):
                r, c, e, mask = queue.popleft()
                if mask == all_collected:
                    return moves
                if e == 0:
                    continue
                for dr, dc in directions:
                    nr, nc = r + dr, c + dc
                    if 0 <= nr < m and 0 <= nc < n and classroom[nr][nc] != 'X':
                        ne = e - 1
                        nm = mask
                        if classroom[nr][nc] == 'L':
                            nm |= (1 << litter_number[nr][nc])
                        if classroom[nr][nc] == 'R':
                            ne = energy
                        if not visited[nr][nc][ne][nm]:
                            visited[nr][nc][ne][nm] = True
                            queue.append((nr, nc, ne, nm))
            moves += 1
        return -1
```

---

## C++

```cpp
class Solution {
public:
    int minMoves(vector<string>& classroom, int energy) {
        int m = classroom.size(), n = classroom[0].size();
        int startRow = 0, startCol = 0, totalLitter = 0;
        vector<vector<int>> litterNumber(m, vector<int>(n, -1));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (classroom[i][j] == 'S') { startRow = i; startCol = j; }
                else if (classroom[i][j] == 'L') { litterNumber[i][j] = totalLitter++; }
            }
        }
        int allCollected = (1 << totalLitter) - 1;
        queue<tuple<int,int,int,int>> q;
        q.push({startRow, startCol, energy, 0});
        vector<vector<vector<vector<bool>>>> visited(
            m, vector<vector<vector<bool>>>(
                n, vector<vector<bool>>(
                    energy + 1, vector<bool>(1 << totalLitter, false)
                )
            )
        );
        visited[startRow][startCol][energy][0] = true;
        vector<pair<int,int>> dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        int moves = 0;
        while (!q.empty()) {
            int sz = q.size();
            while (sz--) {
                auto [row, col, e, mask] = q.front(); q.pop();
                if (mask == allCollected) return moves;
                if (e == 0) continue;
                for (auto& d : dirs) {
                    int nr = row + d.first, nc = col + d.second;
                    if (nr < 0 || nr >= m || nc < 0 || nc >= n || classroom[nr][nc] == 'X')
                        continue;
                    int ne = e - 1, nm = mask;
                    if (classroom[nr][nc] == 'L')
                        nm |= (1 << litterNumber[nr][nc]);
                    if (classroom[nr][nc] == 'R') ne = energy;
                    if (!visited[nr][nc][ne][nm]) {
                        visited[nr][nc][ne][nm] = true;
                        q.push({nr, nc, ne, nm});
                    }
                }
            }
            moves++;
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

typedef struct {
    int row, col, energy, mask;
} State;

int minMoves(char** classroom, int classroomSize, int* classroomColSize, int energy) {
    int m = classroomSize, n = classroomColSize[0];
    int startRow = 0, startCol = 0, totalLitter = 0;
    int litterNumber[20][20];
    memset(litterNumber, -1, sizeof(litterNumber));
    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++) {
            if (classroom[i][j] == 'S') { startRow = i; startCol = j; }
            else if (classroom[i][j] == 'L') { litterNumber[i][j] = totalLitter++; }
        }
    int allCollected = (1 << totalLitter) - 1;
    if (allCollected == 0) return 0;
    int f1 = n * (energy + 1) * (1 << totalLitter);
    int f2 = (energy + 1) * (1 << totalLitter);
    int f3 = (1 << totalLitter);
    int cap = m * n * (energy + 1) * (1 << totalLitter);
    State* queue = (State*)malloc(sizeof(State) * cap);
    bool* visited = (bool*)calloc(m * n * (energy + 1) * (1 << totalLitter), sizeof(bool));
    int dirs[4][2] = {{1,0},{-1,0},{0,1},{0,-1}};
    int front = 0, back = 0;
    queue[back++] = (State){startRow, startCol, energy, 0};
    visited[startRow * f1 + startCol * f2 + energy * f3 + 0] = true;
    int moves = 0;
    while (front < back) {
        int sz = back - front;
        for (int k = 0; k < sz; k++) {
            State cur = queue[front++];
            if (cur.mask == allCollected) { free(queue); free(visited); return moves; }
            if (cur.energy == 0) continue;
            for (int d = 0; d < 4; d++) {
                int nr = cur.row + dirs[d][0];
                int nc = cur.col + dirs[d][1];
                if (nr < 0 || nr >= m || nc < 0 || nc >= n || classroom[nr][nc] == 'X')
                    continue;
                int ne = cur.energy - 1, nm = cur.mask;
                if (classroom[nr][nc] == 'L') nm |= (1 << litterNumber[nr][nc]);
                if (classroom[nr][nc] == 'R') ne = energy;
                int idx = nr * f1 + nc * f2 + ne * f3 + nm;
                if (!visited[idx]) {
                    visited[idx] = true;
                    queue[back++] = (State){nr, nc, ne, nm};
                }
            }
        }
        moves++;
    }
    free(queue); free(visited);
    return -1;
}
```
