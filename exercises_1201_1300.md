## 1201. (90%)
```python
def solution(n, a, b, c):

    def find_gcd(x, y):
        while y:
            x, y = y, (x % y)
        return x

    def find_lcm(x, y):
        return x * y // find_gcd(x, y)

    def count_ugly(x):
        ans = x//a + x//b + x//c
        ans -= (x//lcm_ab + x//lcm_bc + x//lcm_ac)
        ans += (x//lcm_abc)
        return ans

    lcm_ab = find_lcm(a, b)
    lcm_bc = find_lcm(b, c)
    lcm_ac = find_lcm(a, c)
    lcm_abc = find_lcm(lcm_ab, c)

    ## binary search
    left, right = 1, int(2e9)+1

    while left < right:
        mid = left + (right-left)//2
        num_ugly = count_ugly(mid)
        if num_ugly < n:
            left = mid + 1
        else:
            right = mid

    return left
```

## 1209. (94%)
```python
def solution(s, k):
    stack = [["#", 0]]
    for x in s:
        if x == stack[-1][0]:
            stack[-1][1] += 1
            if stack[-1][1] == k:
                stack.pop()
        else:
            stack.append([x, 1])

    res = ""
    for (x, a) in stack[1:]:
        res += a*x
    return res
```

## 1254. (55%)
```python
def solution(self, grid):
    n, m = len(grid), len(grid[0])
    res = 0

    for i in range(n):
        for j in range(m):
            if grid[i][j] == 0:
                self.is_closed = True
                self.dfs(grid, i, j, n, m)
                if self.is_closed:
                    res += 1
    return res

def dfs(self, grid, i, j, n, m):

    if any([i < 0, j < 0, i > (n-1), j > (m-1)]):
        return

    if grid[i][j] == 1:
        return

    grid[i][j] = 1

    if any([i == 0, j == 0, i == (n-1), j == (m-1)]):
        self.is_closed = False

    self.dfs(grid, i-1, j, n, m)
    self.dfs(grid, i+1, j, n, m)
    self.dfs(grid, i, j-1, n, m)
    self.dfs(grid, i, j+1, n, m)
```
