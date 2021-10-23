## 2. (38%)
```python
def solution(l1, l2):
    def decode(node):
        res = 0
        i = 1
        while node:
            res += i * node.val
            node = node.next
            i *= 10
        return res

    def encode(val):
        if val == 0:
            return ListNode(0)

        res = ListNode()
        cur = res
        while val != 0:
            cur.val = val % 10
            val = val // 10

            if val == 0:
                return res
            else:
                cur.next = ListNode()
                cur = cur.next

    v1 = decode(l1)
    v2 = decode(l2)
    return encode(v1 + v2)
```

## 57. (58%)
```python
def solution(intervals, newInterval):
    res = []

    if not intervals:
        return [newInterval]

    a, b = newInterval

    if a > intervals[-1][-1]:
        return intervals + [newInterval]

    if b < intervals[0][0]:
        return [newInterval] + intervals

    while intervals:
        x, y = intervals.pop(0)

        if b < x:
            return res + [[a, b], [x, y]] + intervals

        if a > y:
            res.append([x, y])
            continue

        if a >= x and b <= y:
            return res + [[x, y]] + intervals

        if a >= x:
            a = x

        if b <= y:
            b = y

    return res + [[a, b]]
```
## 59. (37%)
```python
def solution(n):

    grid = [[0 for _ in range(n+2)] for _ in range(n+2)]

    for i in range(n+2):
        grid[i][0] = -1
        grid[i][-1] = -1

    for j in range(n+2):
        grid[0][j] = -1
        grid[-1][j] = -1

    i, j = 1, 1

    grid[1][1] = 1

    for x in range(2, n**2+1):

        # move right if possible
        if grid[i-1][j] != 0 and grid[i][j+1] == 0:
            j += 1

        # move down if possible
        elif grid[i][j+1] != 0 and grid[i+1][j] == 0:
            i += 1

        # move left if possible
        elif grid[i+1][j] != 0 and grid[i][j-1] == 0:
            j -= 1

        # move up if possible
        else:
            i -= 1

        grid[i][j] = x

    res = [[0 for _ in range(n)] for _ in range(n)]

    for i in range(n):
        for j in range(n):
            res[i][j] = grid[i+1][j+1]

    return res
```

## 62. (73%)
```python
def solution(m, n):

    dp = [[1]*m]*n

    for i in range(1, n):
        for j in range(1, m):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[-1][-1]
```

## 99. (82%)
```python
def solution(root):

    def inorder(node, traversal_vals, traversal_nodes):
        if node:
            # recursively traverse the left subtree
            if node.left:
                traversal_vals, traversal_nodes = inorder(node.left, traversal_vals, traversal_nodes)
            # current node
            traversal_vals.append(node.val)
            traversal_nodes.append(node)
            # recursively traverse the right subtree
            if node.right:
                traversal_vals, traversal_nodes = inorder(node.right, traversal_vals, traversal_nodes)
        return traversal_vals, traversal_nodes

    # make an in-order traversal
    traversal_vals, traversal_nodes = inorder(root, [], [])
    # sort the values
    traversal_vals.sort()
    # assign updated values to each node
    for val, node in zip(traversal_vals, traversal_nodes):
        node.val = val
```
