## 1856 (28%)
```python
def solution(nums):
    n = len(nums)
    if n == 1:
        return (nums[0]*nums[0]) % (10**9+7)

    left = [-1 for _ in range(n)]
    right = [-1 for _ in range(n)]

    stack = []
    for (i, x) in enumerate(nums):
        while stack and stack[-1][1] > x:
            j, y = stack.pop()
            right[j] = i
        stack.append((i, x))

    stack = []
    for i in range(n-1, -1, -1):
        x = nums[i]
        while stack and stack[-1][1] > x:
            j, y = stack.pop()
            left[j] = i
        stack.append((i, x))

    res = 0

    run_sum = [nums[0]]
    for x in nums[1:]:
        run_sum.append(run_sum[-1]+x)

    for i, x in enumerate(nums):
        left_bound = left[i] + 1 if left[i] != -1 else 0
        right_bound = right[i] - 1 if right[i] != -1 else n-1
        res = max(res, x*(run_sum[right_bound] - run_sum[left_bound] + nums[left_bound]))

    return res % (10**9+7)
```
