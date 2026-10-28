# LeetCode 3882 - Minimum XOR Path in a Grid

Video walkthrough: [YOUR_YOUTUBE_VIDEO_LINK]
Code (Java/Python/C++/C): https://github.com/Shaanworkspace/YOUTUBE-DRIVE/blob/main/Leetcode_Daily/LC_3882_Minimum_XOR_Path_in_a_Grid_All_Languages.md
Community: Telegram https://t.me/opentech_shaanlabs | WhatsApp https://chat.whatsapp.com/CvlyO3ZBBoTBiPLDXpEJME?mode=gi_t

---

## Java
```java
class Solution {
    int[][][] dp;

    public int minCost(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        dp = new int[m][n][1024];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                Arrays.fill(dp[i][j], -1);
            }
        }
        return solve(grid, 0, 0, 0);
    }

    int solve(int[][] grid, int row, int col, int xor) {
        int m = grid.length;
        int n = grid[0].length;

        // Invalid path
        if (row >= m || col >= n) {
            return Integer.MAX_VALUE;
        }

        // Current cell ka XOR
        xor ^= grid[row][col];

        // Destination
        if (row == m - 1 && col == n - 1) {
            return xor;
        }

        if (dp[row][col][xor] != -1) {
            return dp[row][col][xor];
        }

        // Dono directions explore karo
        int right = solve(grid, row, col + 1, xor);
        int down = solve(grid, row + 1, col, xor);

        return dp[row][col][xor] = Math.min(right, down);
    }
}
```

---

## Python
```python
class Solution:
    def minCost(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        memo = {}

        def solve(r, c, curr_xor):
            if r >= m or c >= n:
                return float('inf')
            
            curr_xor ^= grid[r][c]
            
            if r == m - 1 and c == n - 1:
                return curr_xor
            
            state = (r, c, curr_xor)
            if state in memo:
                return memo[state]
            
            res = min(solve(r + 1, c, curr_xor), solve(r, c + 1, curr_xor))
            memo[state] = res
            return res

        return solve(0, 0, 0)
```

---

## C++
```cpp
class Solution {
public:
    int dp[10][10][1024];
    int m, n;

    int solve(vector<vector<int>>& grid, int r, int c, int currXor) {
        if (r >= m || c >= n) return 1e9;
        
        currXor ^= grid[r][c];
        if (r == m - 1 && c == n - 1) return currXor;
        
        if (dp[r][c][currXor] != -1) return dp[r][c][currXor];
        
        return dp[r][c][currXor] = min(solve(grid, r + 1, c, currXor), 
                                       solve(grid, r, c + 1, currXor));
    }

    int minCost(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();
        memset(dp, -1, sizeof(dp));
        return solve(grid, 0, 0, 0);
    }
};
```

---

## C
```c
#include <string.h>
#include <limits.h>

int dp_table[10][10][1024];

int solve_xor(int** grid, int m, int n, int r, int c, int currXor) {
    if (r >= m || c >= n) return 1000000;
    
    currXor ^= grid[r][c];
    if (r == m - 1 && c == n - 1) return currXor;
    
    if (dp_table[r][c][currXor] != -1) return dp_table[r][c][currXor];
    
    int down = solve_xor(grid, m, n, r + 1, c, currXor);
    int right = solve_xor(grid, m, n, r, c + 1, currXor);
    
    return dp_table[r][c][currXor] = (down < right) ? down : right;
}

int minCost(int** grid, int gridSize, int* gridColSize) {
    int m = gridSize;
    int n = gridColSize[0];
    memset(dp_table, -1, sizeof(dp_table));
    return solve_xor(grid, m, n, 0, 0, 0);
}
```
