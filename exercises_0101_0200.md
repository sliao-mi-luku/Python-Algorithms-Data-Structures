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

## 139. (55%)
```python
def solution(s, wordDict):

    n = len(s)

    wordDict = set(wordDict)

    dp = [0 for _ in range(n+1)]

    dp[0] = True

    for i in range(1, n+1):
        for j in range(i):
            dp[i] = (dp[j] and (s[j:i] in wordDict))
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
