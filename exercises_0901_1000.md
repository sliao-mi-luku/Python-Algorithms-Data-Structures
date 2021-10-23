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
