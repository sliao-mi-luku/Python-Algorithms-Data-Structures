## 2085.
```python
def solution(words1, words2):
    d1 = dict()
    d2 = dict()

    for x in words1:
        d1[x] = d1.get(x, 0) + 1

    for x in words2:
        d2[x] = d2.get(x, 0) + 1

    s = set()
    for x in d1:
        if d1[x] == 1:
            s.add(x)

    res = 0
    for x in d2:
        if d2[x] == 1 and x in s:
            res += 1

    return res
```

## 2086.
```python
def minimumBuckets(street):
    n = len(street)

    if street == "H":
        return -1

    if street[:2] == "HH" or street[-2:] == "HH":
        return -1

    if "HHH" in street:
        return -1

    return street.count("H") - street.count("H.H")
```

## 2087.
```python
def solution(startPos, homePos, rowCosts, colCosts):
    n = len(rowCosts)
    m = len(colCosts)

    if startPos == homePos:
        return 0

    res = 0

    if startPos[0] < homePos[0]:
        for i in range(homePos[0], startPos[0], -1):
            res += rowCosts[i]
    else:
        for i in range(homePos[0], startPos[0]):
            res += rowCosts[i]

    if startPos[1] < homePos[1]:
        for i in range(homePos[1], startPos[1], -1):
            res += colCosts[i]
    else:
        for i in range(homePos[1], startPos[1]):
            res += colCosts[i]

    return res
```

## 2088.
```python
def solution(grid):
    n = len(grid)
    m = len(grid[0])

    left = [[0 for _ in range(m)] for _ in range(n)]
    right = [[0 for _ in range(m)] for _ in range(n)]

    for i in range(n):
        for j in range(m):
            if grid[i][j] == 0:
                continue
            if j == 0:
                left[i][j] = 1
            else:
                left[i][j] = left[i][j-1] + 1

    for i in range(n):
        for j in range(m-1, -1, -1):
            if grid[i][j] == 0:
                continue
            if j == m-1:
                right[i][j] = 1
            else:
                right[i][j] = right[i][j+1] + 1

    res = 0
    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1:
                # pyramidal
                w = 1
                for k in range(i+1, n):
                    w += 1
                    if left[k][j] >= w and right[k][j] >= w:
                        res += 1
                    else:
                        break
                # inverse pyramidal
                w = 1
                for k in range(i-1, -1, -1):
                    w += 1
                    if left[k][j] >= w and right[k][j] >= w:
                        res += 1
                    else:
                        break
    return res
```

## 2089
```python
def solution(nums, target):
    nums.sort()
    res = []
    for i, x in enumerate(nums):
        if x == target:
            res.append(i)
        if x > target:
            break
    return res
```

## 2090
```python
def solution(nums, k):
    n = len(nums)

    if k == 0:
        return nums

    if n == 1:
        return [-1]

    res = [-1 for _ in range(n)]
    cum = [nums[0]]

    for x in nums[1:]:
        cum.append(cum[-1] + x)

    for i, x in enumerate(nums):
        if (i-k) < 0 or (i+k) > (n-1):
            continue
        res[i] = int((cum[i+k] - cum[i-k] + nums[i-k])/(2*k+1))

    return res
```
