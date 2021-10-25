## 781. (33%)
```python
def solution(answers):
    d = dict()

    for x in answers:
        d[x] = d.get(x, 0) + 1

    res = 0

    for k, v in d.items():
        res += (k+1)*(v // (k+1))
        if v % (k+1) != 0:
            res += (k+1)

    return res
```
