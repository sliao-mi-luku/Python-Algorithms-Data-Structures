## 2103.
```python
def solution(rings):
    n = len(rings)//2
    s = [set() for _ in range(10)]

    for i in range(n):
        color, idx = rings[2*i], int(rings[2*i+1])
        s[idx].add(color)

    res = 0
    for i in range(10):
        if len(s[i]) == 3:
            res += 1

    return res
```

## 2119.
``` python
def solution(num):
    if num == 0:
        return True

    if str(num)[-1] == "0":
        return False
    else:
        return True
```

## 2120.
```python
def solution(n, startPos, s):
    m = len(s)
    res = [0 for _ in range(m)]
    # read from s[i], initial position at startPos
    for i in range(m):
        row = startPos[0]
        col = startPos[1]
        cur = 0
        for j in range(i, m):
            if row == 0 and s[j] == "U":
                break
            elif row == n-1 and s[j] == "D":
                break
            elif col == 0 and s[j] == "L":
                break
            elif col == n-1 and s[j] == "R":
                break
            else:
                cur += 1
                if s[j] == "U":
                    row -= 1
                elif s[j] == "D":
                    row += 1
                elif s[j] == "L":
                    col -= 1
                else:
                    col += 1
        res[i] = cur

    return res
```
