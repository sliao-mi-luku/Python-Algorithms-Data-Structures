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

## 5. (50%)
```python
def solution(s):
    n = len(s)
    if n == 1:
        return s
    if n == 2:
        return s if s[0]==s[1] else s[0]

    res = s[0]
    for i in range(n-1):
        if s[i] == s[i+1]:
            res = s[i:i+2]

    # odd palidrome
    for i in range(1, n-1):
        left = i-1
        right = i+1
        while s[left] == s[right]:
            if (right-left+1) > len(res):
                res = s[left:right+1]
            left -= 1
            right += 1
            if left < 0 or right >= n:
                break

    # even palindrome
    for i in range(1, n-2):
        if s[i] == s[i+1]:
            left = i-1
            right = i+2
            while s[left] == s[right]:
                if (right-left+1) > len(res):
                    res = s[left:right+1]
                left -= 1
                right += 1
                if left < 0 or right >= n:
                    break

    return res
```

## 20. (75%)
```python
def solution(s):
    stack = []
    for x in s:
        if x in ["(", "[", "{"]:
            stack.append(x)
        else:
            if not stack:
                return False
            y = stack.pop()
            if y+x not in ["()", "[]", "{}"]:
                return False
    return not stack
```

## 53. (40%)
```python
def solution(nums):
    res = nums[0]
    cur = nums[0]
    for x in nums[1:]:
        cur = max(cur+x, x)
        res = max(res, cur)
    return res
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
## 59. (76%)
```python
def solution(n):

    grid = [[0 for _ in range(n)] for _ in range(n)]

    left = 0
    right = n-1
    top = 0
    bottom = n-1
    x = 1

    while left <= right and top <= bottom:

        for i in range(left, right+1):
            grid[top][i] = x
            x += 1

        top += 1

        for i in range(top, bottom+1):
            grid[i][right] = x
            x += 1

        right -= 1

        for i in range(right, left-1, -1):
            grid[bottom][i] = x
            x += 1

        bottom -= 1

        for i in range(bottom, top-1, -1):
            grid[i][left] = x
            x += 1

        left += 1

    return grid
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

## 70. (95%)
```python
def solution(n):
    if n == 1:
        return 1
    if n == 2:
        return 2
    dp = [1] + [2] + [0 for _ in range(n-2)]
    for i in range(2, n):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[-1]
```

## 71. (98%)
```python
def solution(path):
    history = []
    path = path.split('/')

    for x in path:
        if not x or x == ".":
            continue

        if x == "..":
            if len(history) >= 1:
                history.pop()
        else:
            history.append(x)

    return "/" + "/".join(history)
```

## 94. (89%)
```python
def solution(root):

    def recursion(node, traversal=[]):
        if node:
            if node.left:
                traversal = recursion(node.left, traversal)
            traversal.append(node.val)
            if node.right:
                traversal = recursion(node.right, traversal)
            return traversal

    return recursion(root, [])
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
