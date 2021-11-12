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
