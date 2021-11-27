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
def minCost(startPos, homePos, rowCosts, colCosts):
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
