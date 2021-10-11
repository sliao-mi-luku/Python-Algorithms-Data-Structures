


### 99. Recover Binary Search Tree

```python
class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        """
        Recover the binary search tree in-place
        """

        def inorder(node, traversal_vals, traversal_nodes):
            """
            In-order traversal from TreeNode node
            Arguments:
                traversal_vals: in-order traversal of nodes' values
                traversal_nodes: in-order traversal of nodes
            Outputs:
                traversal_vals: in-order traversal of nodes' values
                traversal_nodes: in-order traversal of nodes
            """
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

"""
Runtime: 72 ms (82%)
"""
```
