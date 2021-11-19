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

## 1541. (89%)
```python
def solution(s):
    res = 0

    s = s.replace("))", ">")

    for x in s:
        if x == ")":
            res += 1

    s = s.replace(")", ">")

    score = 0
    for x in s:
        if x == "(":
            score += 1
        else:
            score -= 1
            if score == -1:
                res += 1
                score = 0

    res += 2*score

    return res
```

## 1574 (88%)
```python
def solution(arr):
    n = len(arr)
    j = n-1
    while j != 0 and arr[j-1] <= arr[j]:
        j -= 1
    # arr[j], ..., arr[n-1] are non-decreasing
    if j == 0:
        return 0

    res = j
    for i in range(n):
        while j != n and arr[i] > arr[j]:
            j += 1
        res = min(res, j-i-1)
        if arr[i+1] < arr[i]:
            break

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
