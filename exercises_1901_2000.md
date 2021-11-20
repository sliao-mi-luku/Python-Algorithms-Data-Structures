## 1963. (53%)
```python
def solution(s):
    stack = []
    for x in s:
        if stack and stack[-1] == "[" and x == "]":
            stack.pop()
        else:
            stack.append(x)
    return (len(stack)//2 + 1)//2
```

## 1996. (57%)
```python
def solution(properties):
    properties.sort(key = lambda x: (-x[0], x[1]))

    res = 0
    maxdef = 0
    for _, y in properties:
        if y < maxdef:
            res += 1
        maxdef = max(maxdef, y)

    return res
```
