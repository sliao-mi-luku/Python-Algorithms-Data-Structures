## 856. (86%)
```python
def solution(s):
    stack = []
    for x in s:
        if x == "(":
            stack.append(x)
        else: # ")"
            if stack[-1] == "(":
                stack.pop()
                stack.append(1)
            else: # 1, 2, 3, ...
                y = 0
                while stack[-1] != "(":
                    y += stack.pop()
                stack.pop()
                stack.append(2*y)
    return sum(stack)
```
