## 844. (66%)
```python
def solution(s, t):
    A = process(s)
    B = process(t)
    n = len(A)
    if len(B) != n:
        return False
    for i in range(n):
        if A[i] != B[i]:
            return False
    return True

def process(s):
    arr = []
    for x in s:
        if x == "#":
            if arr:
                arr.pop()
        else:
            arr.append(x)
    return arr
```

## 856. (86%)
```python
def solution(s):
    stack = []
    for x in s:
        if x == "(":
            stack.append(x)
        else: # ")"
            if stack[-1] == "(":
                stack.pop()
                stack.append(1)
            else: # 1, 2, 3, ...
                y = 0
                while stack[-1] != "(":
                    y += stack.pop()
                stack.pop()
                stack.append(2*y)
    return sum(stack)
```

## 880. (63%)
```python
def solution(s, k):
    n = len(s)
    d = dict()
    stack = []
    last_chr = None
    q = 0

    for i, x in enumerate(s):
        if not x.isnumeric():
            q += 1
            if q == k:
                return x
            d[q] = x
            last_chr = x
        else:
            stack.append((q, last_chr))
            q *= int(x)
            if q == k:
                return last_chr

        if q >= k:
            break

    while stack and k not in d:
        q, last_chr = stack.pop()
        k %= q
        if k == 0:
            return last_chr

    return d[k]
```

## 897. (69%)
```python
def solution(root):
    def inorder(node, traversal):
        if node:
            if node.left:
                traversal = inorder(node.left, traversal)
            traversal.append(node.val)
            if node.right:
                traversal = inorder(node.right, traversal)
            return traversal

    traversal = inorder(root, [])
    root = TreeNode(traversal[0])
    cur = root
    for val in traversal[1:]:
        cur.right = TreeNode(val)
        cur = cur.right
    return root
```
