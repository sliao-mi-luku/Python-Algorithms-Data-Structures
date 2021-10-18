## 263. Ugly Number
```python
class Solution:
    def isUgly(self, n):

        if n <= 0:
            return False

        for x in [2, 3, 5]:
            while n % x == 0:
                n /= x

        return (n == 1)

"""
Runtime: 90%
"""
```

## 264. Ugly Number II
```python
class Solution:
    def nthUglyNumber(n):

        if n == 1:
            return 1

        a = [2]
        b = [3]
        c = [5]

        i, j, k = 0, 0, 0

        res = 1

        while n != 1:
            if a[i] == res:
                i += 1
            if b[j] == res:
                j += 1
            if c[k] == res:
                k += 1

            res = min(a[i], b[j], c[k])

            a.append(res*2)
            b.append(res*3)
            c.append(res*2)

            n -= 1

        return res

"""
Runtime: 66%
"""
```
