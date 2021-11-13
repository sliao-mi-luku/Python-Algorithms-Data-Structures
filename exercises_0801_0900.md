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

## 880. (63%)
```python
def solution(s, k):
    n = len(s)
    d = dict()
    stack = []
    last_chr = None
    q = 0

    for i, x in enumerate(s):
        if not x.isnumeric():
            q += 1
            if q == k:
                return x
            d[q] = x
            last_chr = x
        else:
            stack.append((q, last_chr))
            q *= int(x)
            if q == k:
                return last_chr

        if q >= k:
            break

    while stack and k not in d:
        q, last_chr = stack.pop()
        k %= q
        if k == 0:
            return last_chr

    return d[k]
```
