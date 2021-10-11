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
