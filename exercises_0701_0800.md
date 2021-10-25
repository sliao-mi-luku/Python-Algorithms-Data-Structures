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
