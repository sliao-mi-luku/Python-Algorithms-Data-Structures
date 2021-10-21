## 941. 68%
```python
def solution(arr):

    n = len(arr)

    if n < 3:
        return False

    ascending = True

    for i in range(n-1):
        if arr[i+1] == arr[i]:
            return False

        if ascending:
            if arr[i+1] < arr[i]:
                if i == 0:
                    return False
                ascending = False
        else:
            if arr[i+1] > arr[i]:
                return False

    return (ascending is False)
```

## 953. 76%
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
```
