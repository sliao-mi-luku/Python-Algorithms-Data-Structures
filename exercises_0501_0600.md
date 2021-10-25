## 594. (77%)
```python
def solution(nums):

    d = dict()

    for x in nums:
        d[x] = d.get(x, 0) + 1

    res = 0

    for k, v in d.items():
        if k+1 in d:
            res = max(res, v + d[k+1])

    return res
```
