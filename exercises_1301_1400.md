## 1395.
```python
def solution(rating):
    n = len(rating)
    res = 0

    for j in range(1, n-1):
        left_small = 0
        left_large = 0
        for i in range(j):
            if rating[i] < rating[j]:
                left_small += 1
            elif rating[i] > rating[j]:
                left_large += 1

        right_small = 0
        right_large = 0
        for i in range(j+1, n):
            if rating[i] < rating[j]:
                right_small += 1
            elif rating[i] > rating[j]:
                right_large += 1

        res += left_small*right_large + left_large*right_small

    return res
```
