## 735. (79%)
```python
def solution(asteroids):
    stack = []

    for x in asteroids:
        if not stack:
            stack.append(x)
        else:
            if x < 0:
                while stack and stack[-1] > 0:
                    if stack[-1] > abs(x):
                        x = 0
                        break
                    elif stack[-1] == abs(x):
                        stack.pop()
                        x = 0
                        break
                    else:
                        stack.pop()
                if x != 0:
                    stack.append(x)
            else:        
                stack.append(x)

    return stack
```

## 739. (55%)
```python
def solution(temperatures):
    stack = []
    res = [0 for _ in range(len(temperatures))]

    for i in range(len(temperatures)):
        x = temperatures[i]
        while stack and stack[-1][1] < x:
            res[stack[-1][0]] = i-stack[-1][0]
            stack.pop()
        stack.append((i, x))
    return res
```

## 746. (93%)
```python
def solution(cost):
    n = len(cost)

    dp = [0 for _ in range(n)]
    dp[0] = cost[0]
    dp[1] = cost[1]

    for i in range(2, n):
        dp[i] = min(dp[i-1], dp[i-2]) + cost[i]

    return min(dp[-1], dp[-2])
```

## 769. (64%)
```python
def solution(arr):
    n = len(arr)
    d = dict()
    for i in range(n):
        d[i] = i
    for i, x in enumerate(arr):
        if i == x:
            continue
        x_max = max(i, x)
        x_min = min(i, x)
        for j in range(x_min+1, x_max+1):
            d[j] = d[x_min]

    return len(set(d.values()))
```

## 781. (69%)
```python
def solution(answers):
    d = dict()
    res = 0
    for x in answers:
        d[x] = d.get(x, 0)

        if d[x] == 0:
            res += (x+1)
            d[x] = x
        else:
            d[x] -= 1

    return res
```
