## 101. (66%)
```python
def solution(root):
    # nodes of the 1st level (root)
    cur_nodes = [root]
    # while there are nodes in the current level
    while cur_nodes:
        # list to store the existing nodes in the next level
        next_nodes = []
        # list to store the values in the next level
        next_vals = []
        # iterate over the nodes in the current layer
        for node in cur_nodes:
            if node.left:
                next_nodes.append(node.left)
                next_vals.append(node.left.val)
            else:
                next_vals.append(200) # -100 < node.val < 100

            if node.right:
                next_nodes.append(node.right)
                next_vals.append(node.right.val)
            else:
                next_vals.append(200)
        # check if the next_vals is the same as its reversal
        reversal = list(next_vals)
        reversal.reverse()
        if next_vals != reversal:
            return False
        # move on the the next level
        cur_nodes = next_nodes
    # finish the whole tree, return True
    return True
```

## 109. (30%)
```python
def solution(head):

    def recursion(vals):
        if vals:
            n = len(vals)
            mid_idx = n//2
            root = TreeNode(val=vals[mid_idx])
            if mid_idx != 0:
                root.left = recursion(vals[:mid_idx])
            if mid_idx != n-1:
                root.right = recursion(vals[mid_idx+1:])
            return root

    # convert the linked list to a List
    vals = []
    cur = head
    while cur:
        vals.append(cur.val)
        cur = cur.next

    # recursively build the tree from the middle node
    return recursion(vals)
```

## 113. (24%)
```python
class Solution:
    def pathSum(self, root, targetSum):
        self.res = []
        self.recursion(root, [], targetSum)
        return self.res

    def recursion(node, history, target):
        if node:
            target -= node.val
            # if node is a leaf and the target is 0 (i.e. targetSum is reached)
            if not node.left and not node.right and (target == 0):
                self.res.append(history + [node.val])

            # go to the left child
            recursion(node.left, history + [node.val], target)
            # go to the right child
            recursion(node.right, history + [node.val], target)
```

## 114. (85%)
```python
def solution(root):

    if not root:
        return []

    def preorder(node, traversal=[]):
        if node:
            traversal.append(node)
            if node.left:
                traversal = preorder(node.left, traversal)
            if node.right:
                traversal = preorder(node.right, traversal)
            return traversal

    traversal = preorder(root, [])

    for i in range(len(traversal)-1):
        traversal[i].left = None
        traversal[i].right = traversal[i+1]

    traversal[-1].left = None
    traversal[-1].right = None
```

## 118. (20%)
```python
def solution(numRows):
    if numRows == 1:
        return [[1]]
    if numRows == 2:
        return [[1], [1, 1]]
    res = [[1], [1, 1]]
    for i in range(3, numRows+1):
        new_row = [1]
        for j in range(i-2):
            new_row.append(res[-1][j]+res[-1][j+1])
        new_row.append(1)
        res.append(new_row)
    return res
```

## 119. (67%)
```python
def solution(rowIndex):
    if rowIndex == 0:
        return [1]
    if rowIndex == 1:
        return [1, 1]
    prev_row = [1, 1]
    for i in range(2, rowIndex+1):
        cur_row = [1]
        for j in range(len(prev_row)-1):
            cur_row.append(prev_row[j]+prev_row[j+1])
        cur_row.append(1)
        prev_row = list(cur_row)
    return cur_row
```

## 120. (14%)
```python
def solution(triangle):
    n_layers = len(triangle)
    if n_layers == 1:
        return triangle[0][0]

    dp = list(triangle)

    for i in range(1, n_layers):
        n_elements = len(dp[i])
        for j in range(n_elements):
            if j == 0:
                dp[i][j] = dp[i-1][0] + triangle[i][j]
            elif j == n_elements-1:
                dp[i][j] = dp[i-1][-1] + triangle[i][j]
            else:
                dp[i][j] = min(dp[i-1][j-1], dp[i-1][j]) + triangle[i][j]

    return min(dp[-1])
```

## 121. (31%)
```python
def solution(prices):
    res = 0
    min_cost = float('inf')

    for i in range(len(prices)):
        res = max(res, prices[i]-min_cost)
        min_cost = min(min_cost, prices[i])

    return res
```

## 122. (51%)
```python
def solution(prices):
    # hold[i]: maximum profit if holding the stock at prices[i]
    # empty[i]: maximum profit if not holding the stock at prices[i]
    n = len(prices)
    hold = [0 for _ in range(n)]
    empty = [0 for _ in range(n)]
    hold[0] = -prices[0]

    for i in range(1, n):
        hold[i] = max(hold[i-1], empty[i-1] - prices[i])
        empty[i] = max(hold[i-1] + prices[i], empty[i-1])

    return max(hold[-1], empty[-1])
```

## 131. (26%)
```python
def solution(s):
    n = len(s)
    dp = [[False for _ in range(n)] for _ in range(n)]
    # dp[i][j]: s[i], ..., s[j] is palindrome
    for i in range(n):
        dp[i][i] = True

    for i in range(n-1):
        if s[i] == s[i+1]:
            dp[i][i+1] = True

    for k in range(3, n+1): # substring of length k
        for i in range(n-k+1):
            j = i + k - 1
            # check s[i], ..., s[j] is a palindrome or not
            if s[i] != s[j]:
                continue
            dp[i][j] = dp[i+1][j-1]

    def recursion(start):
        if start > n-1:
            return [[]]
        res = []
        for end in range(start, n):
            if dp[start][end]:
                right = recursion(end+1) # ex. [["a", "a"], ["aa"]]
                for R in right:
                    res.append([s[start:end+1]] + R)
        return res

    return recursion(0)
```

## 139. (65%)
```python
def solution(s, wordDict):
    # dp[i]: s[0], ..., s[i] can be segmented into words in wordDict
    wordDict = set(wordDict)
    n = len(s)
    dp = [False for _ in range(n)]

    if n == 1:
        return (s[0] in wordDict)

    if s[0] in wordDict:
        dp[0] = True

    for i in range(1, n):
        if s[:i+1] in wordDict:
            dp[i] = True
            continue
        for j in range(i):
            dp[i] = dp[j] and s[j+1:i+1] in wordDict
            if dp[i]:
                break

    return dp[-1]
```

## 143. (79%)
```python
def solution(head):
    forward = []
    cur = head

    while cur:
        forward.append(cur)
        cur = cur.next

    i, j = 0, len(forward)-1

    while i < j:
        forward[i].next = forward[j]
        if i+1 == j:
            forward[j].next = None
        else:
            forward[j].next = forward[i+1]
        i += 1
        j -= 1

        if i == j:
            forward[j].next = None
```

## 144. (89%)
```python
def solution(root):

    def recursion(node, traversal):
        if node:
            traversal.append(node.val)
            if node.left:
                traversal = recursion(node.left, traversal)
            if node.right:
                traversal = recursion(node.right, traversal)
            return traversal

    return recursion(root, [])
```

## 145. (72%)
```python
def solution(root):

    def recursion(node, traversal):
        if node:
            if node.left:
                traversal = recursion(node.left, traversal)
            if node.right:
                traversal = recursion(node.right, traversal)
            traversal.append(node.val)
            return traversal

    return recursion(root, [])
```

## 150. (96%)
```python
def solution(tokens):
    cache = []

    for x in tokens:
        if x in ["+", "-", "*", "/"]:
            b = cache.pop()
            a = cache.pop()
            if x == "+":
                cache.append(a+b)
            elif x == "-":
                cache.append(a-b)
            elif x == "*":
                cache.append(a*b)
            else:
                cache.append(int(a/b))
        else:
            cache.append(int(x))

    return cache[0]
```

## 152. (5%)
```python
def solution(nums):
    n = len(nums)

    if n == 1:
        return nums[0]

    mmax = [0 for _ in range(n)]
    mmin = [0 for _ in range(n)]

    mmax[0] = nums[0]
    mmin[0] = nums[0]
    res = nums[0]

    for i in range(1, n):
        mmax[i] = max(nums[i], mmax[i-1]*nums[i], mmin[i-1]*nums[i])
        mmin[i] = min(nums[i], mmax[i-1]*nums[i], mmin[i-1]*nums[i])
        res = max(res, mmax[i])

    return res
```

## 173. (84%)
```python
class solution:
    def __init__(self, root):
        self.traversal = self.inorder(root, [])
        self.i = -1

    def next(self):
        self.i += 1
        return self.traversal[self.i]

    def hasNext(self):
        return self.i < len(self.traversal)-1

    def inorder(self, node, traversal):
        if node:
            if node.left:
                traversal = self.inorder(node.left, traversal)
            traversal.append(node.val)
            if node.right:
                traversal = self.inorder(node.right, traversal)
            return traversal
```

## 198. (68%)
```python
def solution(nums):
    # dp[i]: maximum money we can get given houses nums[0], ..., nums[i]
    n = len(nums)

    if n == 1:
        return nums[0]

    dp = [0 for _ in range(n)]
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])

    for i in range(2, n):
        dp[i] = max(dp[i-1], dp[i-2]+nums[i])

    return dp[-1]
```
