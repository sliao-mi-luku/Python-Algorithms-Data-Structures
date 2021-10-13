### 2. Add Two Numbers
```python
class Solution:
    def addTwoNumbers(self, l1, l2):

        cur1 = l1
        cur2 = l2
        carry = 0

        while cur1 and cur2:
            # do sum
            val_sum = cur1.val + cur2.val + carry
            # update node values in-place
            cur1.val = val_sum % 10
            cur2.val = val_sum % 10
            # update carry
            carry = val_sum // 10

            # advance
            if cur1.next and cur2.next:
                cur1, cur2 = cur1.next, cur2.next

            elif not cur1.next and not cur2.next:
                if carry != 0:
                    cur1.next = ListNode(carry)
                return l1

            elif cur1.next:
                while cur1.next:
                    cur1 = cur1.next
                    val_sum = cur1.val + carry
                    cur1.val = val_sum % 10
                    carry = val_sum // 10
                if carry != 0:
                    cur1.next = ListNode(carry)
                return l1

            else:
                while cur2.next:
                    cur2 = cur2.next
                    val_sum = cur2.val + carry
                    cur2.val = val_sum % 10
                    carry = val_sum // 10
                if carry != 0:
                    cur2.next = ListNode(carry)
                return l2

"""
Runtime: 87 ms, 29%
"""
```
```python
class Solution:
    def addTwoNumbers(self, l1, l2):

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
"""
Runtime: 78 ms, 38%
"""
```

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
