## 316. (97%)
```python
def solution(s):
    counts = dict()
    for x in s:
        counts[x] = counts.get(x, 0) + 1

    is_placed = dict()
    for x in counts.keys():
        is_placed[x] = False    

    res = []
    for x in s:
        counts[x] -= 1

        if is_placed[x]:
            continue

        if not res:
            res.append(x)
            is_placed[x] = True

        else:
            while ord(res[-1]) > ord(x) and counts[res[-1]] != 0:
                is_placed[res[-1]] = False
                res.pop()
                if not res:
                    break
            res.append(x)
            is_placed[x] = True

    return "".join(res)
```
