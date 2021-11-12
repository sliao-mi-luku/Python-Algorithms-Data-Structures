## 503. (83%)
```python
def solution(nums):
    n = len(nums)
    nums2 = list(nums) + list(nums)
    stack = []
    res = [-1 for _ in range(n)]

    for i in range(2*n):
        x = nums[i%n]
        while stack and nums[stack[-1]] < x:
            res[stack.pop()] = x
        if i < n:
            stack.append(i)
    return res        
```

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
