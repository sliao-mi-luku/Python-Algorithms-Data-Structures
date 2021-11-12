## 636. (53%)
```python
def solution(n, logs):
    infos = []

    for log in logs:
        info = log.split(":")
        infos.append([int(info[0]), 0 if info[1]=='start' else 1, int(info[2])])

    infos.sort(key=lambda x: (x[2], x[1]), reverse=True)

    last_start = dict()
    res = [0 for _ in range(n)]
    func_waitline = []
    cur_func = -1

    while infos:
        (func_i, status, time) = infos.pop()

        if status == 0: # func start
            # conclude the previous func
            if cur_func != -1:
                res[cur_func] += (time - last_start[cur_func])
                func_waitline.append(cur_func)
            # switch to the new func
            cur_func = func_i
            last_start[func_i] = time

        else: # func end
            time += 1
            # conclude the cur_func
            res[cur_func] += (time - last_start[cur_func])
            # move on to process the last paused function
            if func_waitline:
                cur_func = func_waitline.pop()
                last_start[cur_func] = time
            else:
                cur_func = -1

    return res    
```

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
