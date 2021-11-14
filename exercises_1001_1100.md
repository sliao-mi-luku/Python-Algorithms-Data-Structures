## 1003 (39%)
```python
def solution(s):
    n = len(s)
    if n < 3:
        return False

    stack = []
    for x in s[::-1]:
        stack.append(x)
        while (len(stack) >= 3) and stack[-1] == "a" and stack[-2] == "b" and stack[-3] == "c":
            stack.pop()
            stack.pop()
            stack.pop()
    return not stack
```

## 1006 (41%)
```python
def solution(n):

    if n == 1:
        return 1

    stack = [n]
    i = 0

    for x in range(n-1, 0, -1):
        # *
        if i % 4 == 0:
            stack.append(stack.pop()*x)
        # /
        elif i % 4 == 1:
            stack.append(stack.pop()//x)
        # +
        elif i % 4 == 2:
            stack.append("+")
            stack.append(x)
        # -
        else:
            stack.append("-")
            stack.append(x)
        i += 1

    stack.reverse()

    while len(stack) > 1:
        a = stack.pop()
        op = stack.pop()
        b = stack.pop()

        if op == "+":
            stack.append(a+b)
        else:
            stack.append(a-b)

    return stack[0]
```
