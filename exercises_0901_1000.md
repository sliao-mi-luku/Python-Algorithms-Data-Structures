## 953. Verifying an Alien Dictionary
```python
class Solution:
    def isAlienSorted(words, order):

        n = len(words)
        d = dict()

        for i, a in enumerate(order):
            d[a] = i

        for i in range(n-1):
            x, y = words[i], words[i+1]

            while x and y:
                s1 = x[0]
                s2 = y[0]

                if d[s1] < d[s2]:
                    break
                elif d[s1] > d[s2]:
                    return False
                else:
                    x = x[1:]
                    y = y[1:]

            if x and not y:
                return False

        return True
"""
Runtime: 76%
"""
```
