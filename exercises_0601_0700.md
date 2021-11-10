## 695. (55%)
```python
def solution(self, grid):

    n, m = len(grid), len(grid[0])
    res = 0

    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1:
                self.cur = 0
                self.dfs(grid, i, j, n, m)
                res = max(res, self.cur)
    return res

def dfs(self, grid, i, j, n, m):

    if any([i < 0, j < 0, i >= n, j >= m]):
        return

    if grid[i][j] == 0:
        return

    grid[i][j] = 0
    self.cur += 1

    self.dfs(grid, i-1, j, n, m)
    self.dfs(grid, i+1, j, n, m)
    self.dfs(grid, i, j-1, n, m)
    self.dfs(grid, i, j+1, n, m)
```
