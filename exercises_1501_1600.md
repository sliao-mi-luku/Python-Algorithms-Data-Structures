## 1504 (44%)
```python
def solution(mat):
    n, m = len(mat), len(mat[0])
    dp = [[0 for _ in range(m)] for _ in range(n)]
    res = 0

    for i in range(n):
        for j in range(m):
            if mat[i][j] == 0:
                continue

            if j == 0:
                dp[i][j] = 1
            else:
                dp[i][j] = dp[i][j-1]+1
            res += dp[i][j]
            cur_width = dp[i][j]
            for k in range(i-1, -1, -1):
                if mat[k][j] == 0:
                    break
                cur_width = min(cur_width, dp[k][j])
                res += cur_width

    return res
```

## 1598 (87%)
```python
def solution(logs):
    cur = 0
    for x in logs:
        if x == "../":
            cur = max(0, cur-1)
        elif x != "./":
            cur += 1
    return cur
```
