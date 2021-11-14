## 1143 (61%)
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

## 1190 (71%)
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
