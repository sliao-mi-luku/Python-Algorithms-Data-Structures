## 1614 (96%)
```python
def solution(s):

    res = 0
    cur = 0

    for x in s:
        if x == "(":
            cur += 1

        elif x == ")":
            res = max(res, cur)
            cur -= 1

    return res
```
