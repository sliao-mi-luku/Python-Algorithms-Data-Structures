## 101. Symmetric Tree
```python
def isSymmetric(root):
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

"""
Runtime: 36 ms (66%)
"""
```

## 109. Convert Sorted List to Binary Search Tree
```python
def sortedListToBST(head):
    """
    Given a singly linked list head (values are sorted in ascending order),
    Convert it into a balanced BST
    Arguments
        head: linked list node
    """

    # helper function    
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

"""
Runtime: 384 ms (30%)
"""
```

## 113. Path Sum II
```python
class Solution:
    def pathSum(self, root, targetSum):
        """
        Given a binary tree node, return a list of root-to-leaf paths that sum up to targetSum
        Arguments:
            root: the root node of the tree
            targetSum: the target sum
        Output:
            a list of lists. Each list is a path from the root the a leaf
        """
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
"""
Runtime: 64 ms (24%)
"""
```
