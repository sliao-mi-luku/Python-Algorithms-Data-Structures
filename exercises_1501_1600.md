## 1598 (87%)
```python
def solution(logs):

    cur = 0

    for x in logs:
        if x == "../":
            cur = max(0, cur-1)

        elif x != "./":
            cur += 1

    return cur
```
