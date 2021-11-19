## 1003 (39%)
```python
def solution(s):
    n = len(s)
    if n < 3:
        return False

    stack = []
    for x in s[::-1]:
        stack.append(x)
        while (len(stack) >= 3) and stack[-1] == "a" and stack[-2] == "b" and stack[-3] == "c":
            stack.pop()
            stack.pop()
            stack.pop()
    return not stack
```

## 1006 (41%)
```python
def solution(n):

    if n == 1:
        return 1

    stack = [n]
    i = 0

    for x in range(n-1, 0, -1):
        # *
        if i % 4 == 0:
            stack.append(stack.pop()*x)
        # /
        elif i % 4 == 1:
            stack.append(stack.pop()//x)
        # +
        elif i % 4 == 2:
            stack.append("+")
            stack.append(x)
        # -
        else:
            stack.append("-")
            stack.append(x)
        i += 1

    stack.reverse()

    while len(stack) > 1:
        a = stack.pop()
        op = stack.pop()
        b = stack.pop()

        if op == "+":
            stack.append(a+b)
        else:
            stack.append(a-b)

    return stack[0]
```

## 1008. (71%)
```python
def solution(preorder):

    if not preorder:
        return None

    val = preorder[0]
    n = len(preorder)
    root = TreeNode(val)

    i = 1
    while i < n and preorder[i] < val:
        i += 1


    if i != 1:
        root.left = solution(preorder[1:i])
    if i != n:
        root.right = solution(preorder[i:])

    return root
```

## 1019. (91%)
```python
def solution(head):
    res = []
    stack = []
    cur = head
    i = -1

    while cur:
        i += 1
        res.append(0)
        while stack and stack[-1][1] < cur.val:
            j, _ = stack.pop()
            res[j] = cur.val
        stack.append((i, cur.val))
        cur = cur.next

    return res
```

## 1021. (82%)
```python
def solution(s):
    score = 0
    res = ""
    for x in s:
        if x == "(":
            score += 1
            if score != 1:
                res += x
        else: # ")"
            score -= 1
            if score != 0:
                res += x
    return res
```

## 1081. (93%)
```python
def solution(s):
    d = dict()
    placed = dict()

    for x in s:
        d[x] = d.get(x, 0) + 1

    for x in d.keys():
        placed[x] = False

    stack = []
    for x in s:
        d[x] -= 1

        if not placed[x]:            
            while stack and (ord(stack[-1]) > ord(x) and d[stack[-1]] > 0):
                y = stack.pop()
                placed[y] = False

            placed[x] = True
            stack.append(x)


    return "".join(stack)
```
