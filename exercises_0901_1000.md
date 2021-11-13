## 901. (68%)
```python
class Solution:
    def __init__(self):
        self.array = [10**5+1]
        self.res = [1]

    def solution(self, price):
        i = len(self.array)-1
        res = 1
        while self.array[i] <= price:
            res += self.res[i]
            i -= self.res[i]
        self.res.append(res)
        self.array.append(price)
        return res
```

## 907. (32%)
```python
def solution(arr):
    n = len(arr)

    left = [1 for _ in range(n)]
    right = [1 for _ in range(n)]

    # right
    stack = []
    for j, y in enumerate(arr):
        while stack and stack[-1][1] >= y:
            i, x = stack.pop()
            right[i] = j-i
        stack.append((j, y))
    while stack:
        i, x = stack.pop()
        right[i] = n-i

    # left
    stack = []
    for j in range(n-1, -1, -1):
        y = arr[j]
        while stack and stack[-1][1] > y:
            i, x = stack.pop()
            left[i] = abs(j-i)
        stack.append((j, y))
    while stack:
        i, x = stack.pop()
        left[i] = i+1

    res = 0
    for i, x in enumerate(arr):
        res += left[i]*right[i]*x

    return res % (10**9 + 7)
```

## 921. (69%)
```python
def solution(s):
    score = 0
    res = 0
    for x in s:
        if x == "(":
            score += 1
        else:
            score -= 1
        if score == -1:
            res += 1
            score = 0
    return res + score
```

## 941. (68%)
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

## 946. (69%)
```python
def solution(pushed, popped):
    d = dict()

    for i, x in enumerate(pushed):
        d[x] = i

    visited = [False for _ in range(len(pushed))]
    prev_i = None

    for x in popped:
        cur_i = d[x]
        visited[cur_i] = True

        if not prev_i:
            prev_i = cur_i
            continue

        if cur_i < prev_i:
            for k in range(cur_i, prev_i):
                if not visited[k]:
                    return False

        visited[cur_i] = True
        prev_i = cur_i

    return True
```

## 958. (90%)
```python
def solution(root):
        cur_nodes = [root]
        vals = [root.val]

        while cur_nodes:
            next_nodes = [] # list to store the nodes in the next level
            for node in cur_nodes:
                if node.left:
                    if vals[-1] == -1:
                        return False
                    else:
                        next_nodes.append(node.left)
                        vals.append(node.val)
                else:
                    vals.append(-1)

                if node.right:
                    if vals[-1] == -1:
                        return False
                    else:
                        next_nodes.append(node.right)
                        vals.append(node.val)
                else:
                    vals.append(-1)

            cur_nodes = next_nodes

        return True
```


## 953. (76%)
```python
def solution(words, order):
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
