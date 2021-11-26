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

## 509. (30%)
```python
def solution(n):
    if n <= 1:
        return n

    f = [0, 1]
    for i in range(2, n+1):
        f.append(f[-1]+f[-2])
    return f[-1]
```

## 581. (95%)
```python
def solution(nums):
    n = len(nums)
    if n == 1:
        return 0

    sorted_nums = list(nums)
    sorted_nums.sort()

    for i in range(n):
        if nums[i] != sorted_nums[i]:
            break
        if i == n-1:
            return 0

    for j in range(n-1, -1, -1):
        if nums[j] != sorted_nums[j]:
            break

    return j-i+1
```

## 583. (56%)
```python
def solution(word1, word2):
    n1 = len(word1)
    n2 = len(word2)
    dp = [[0 for _ in range(n2+1)] for _ in range(n1+1)]

    for i in range(1, n1+1):
        dp[i][0] = i

    for j in range(1, n2+1):
        dp[0][j] = j

    for i in range(1, n1+1):
        for j in range(1, n2+1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = min(dp[i-1][j]+1, dp[i][j-1]+1)

    return dp[-1][-1]
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
