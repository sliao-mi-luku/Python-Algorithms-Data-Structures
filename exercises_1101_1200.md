## 1124. (91%)
```python
def solution(hours):
    n = len(hours)
    for i in range(n):
        if hours[i] > 8:
            hours[i] = 1
        else:
            hours[i] = -1
    res = 0
    cur = 0
    d = dict()
    for i, x in enumerate(hours):
        cur += x
        if cur >= 1:
            res = max(res, i+1)
        elif cur-1 in d:
            res = max(res, i-d[cur-1])
        if cur not in d:
            d[cur] = i
    return res
```

## 1130. (82%)
```python
def solution(arr):
    res = 0
    while len(arr) != 1:
        i = arr.index(min(arr))
        if i == 0:
            res += arr[0]*arr[1]
            arr.pop(0)
        elif i == len(arr)-1:
            res += arr[-2]*arr[-1]
            arr.pop()
        else:
            if arr[i-1] >= arr[i+1]:
                res += arr[i]*arr[i+1]
            else:
                res += arr[i]*arr[i-1]
            arr.pop(i)
    return res
```

## 1143. (61%)
```python
def solution(text1, text2):

    n = len(text1)
    m = len(text2)

    dp = [[0 for _ in range(m+1)] for _ in range(n+1)]

    for i in range(1, n+1):
        for j in range(1, m+1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1]+1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[n][m]
```

## 1190. (71%)
```python
def solution(s):
    stack = []
    for x in s:
        if x == ")":
            word = []
            while stack[-1] != "(":
                word.append(stack.pop())
            stack.pop()
            stack += word
        else:
            stack.append(x)

    return "".join(stack)
```
