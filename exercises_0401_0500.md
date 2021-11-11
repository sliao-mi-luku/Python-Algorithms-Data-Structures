## 402. (96%)
```python
def solution(num, k):
    stack = []

    for i, x in enumerate(num):
        if not stack:
            stack.append(x)
        else:
            while k and stack[-1] > x:
                stack.pop()
                k -= 1
                if not stack:
                    break
            stack.append(x)

        if k == 0:
            res = "".join(stack) + num[i+1:]
            res = res.lstrip("0")
            if not res:
                return "0"
            else:
                return res

    if k != 0:
        res = "".join(stack[:-k]).lstrip("0")
        if not res:
            return "0"
        else:
            return res
```

## 472. (70%)
```python
def solution(words):

    if len(words) < 2:
        return []

    words.sort(key=lambda x: len(x))

    wordDict = set(words)

    res = []

    def check(s):
        n = len(s)
        dp = [False for _ in range(n+1)]
        dp[0] = True

        for i in range(1, n+1):
            for j in range(i):
                if (dp[j] and (s[j:i] in wordDict)):
                    dp[i] = True
                    break
        return dp[-1]

    while words:
        s = words.pop()
        wordDict.remove(s)
        if s and check(s):
            res.append(s)

    return res
```
