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

## 145 (72%)
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
