## 309. (81%)
```python
def solution(prices):
    n = len(prices)

    if n == 1:
        return 0

    hold = [0 for _ in range(n)]
    empty = [0 for _ in range(n)]

    hold[0] = -prices[0]

    for i in range(1, n):
        hold[i] = max(empty[i-2]-prices[i], hold[i-1])
        empty[i] = max(hold[i-1]+prices[i], empty[i-1])

    return max(hold[-1], empty[-1])
```

## 314.
```python
def solution(root):

    if not root:
        return []

    H_dict = dict()

    root.h = 0

    nodes_cur_level = [root]

    while nodes_cur_level:
        nodes_next_level = []

        for node in nodes_cur_level:
            H_dict[node.h] = H_dict.get(node.h, []) + [node.val]

            if node.left:
                node.left.h = node.h - 1
                nodes_next_level.append(node.left)

            if node.right:
                node.right.h = node.h + 1
                nodes_next_level.append(node.right)

        nodes_cur_level = list(nodes_next_level)

    res = []
    for h in sorted(H_dict.keys()):
        res.append(H_dict[h])

    return res
```

## 316. (97%)
```python
def solution(s):
    counts = dict()
    for x in s:
        counts[x] = counts.get(x, 0) + 1

    is_placed = dict()
    for x in counts.keys():
        is_placed[x] = False    

    res = []
    for x in s:
        counts[x] -= 1

        if is_placed[x]:
            continue

        if not res:
            res.append(x)
            is_placed[x] = True

        else:
            while ord(res[-1]) > ord(x) and counts[res[-1]] != 0:
                is_placed[res[-1]] = False
                res.pop()
                if not res:
                    break
            res.append(x)
            is_placed[x] = True

    return "".join(res)
```

## 331. (95%)
```python
def solution(preorder):

    preorder = preorder.split(",")

    to_fill = 1
    for x in preorder:
        if to_fill <= 0:
            return False
        if x == "#":
            to_fill -= 1
        else:
            to_fill += 1

    return to_fill == 0
```

## 337. (31%)
```python
def solution(root):

    def dfs(node):
        if not node:
            return [0, 0]
        rob_left, not_rob_left = dfs(node.left)
        rob_right, not_rob_right = dfs(node.right)

        rob_node = node.val + not_rob_left + not_rob_right
        not_rob_node = max(rob_left, not_rob_left) + max(rob_right, not_rob_right)

        return [rob_node, not_rob_node]

    return max(dfs(root))
```

## 338. (82%)
```python
def solution(num):
    if num == 0:
        return [0]
    if num == 1:
        return [0, 1]
    res = [0, 1]
    for x in range(2, num+1):
        if x % 2 == 0:
            res.append(res[x//2])
        else:
            res.append(res[x//2]+1)
    return res
```

## 339.
```python
def solution(nestedList):
    res = 0

    def decode(arr, depth):
        for x in arr:
            if x.isInteger():
                res += x.getInteger() * depth
            else:
                decode(x.getList(), depth+1)

    decode(nestedList, 1)

    return res
```

## 341.
```python
class NestedIterator:
    def __init__(self, nestedList: [NestedInteger]):
        self.nestedList = nestedList
        self.arr = []
        # decode
        self.decode(nestedList)
        self.n = len(self.arr)
        self.i = 0

    def decode(self, nestedList):
        """
        Decode a nestedList
        """
        for x in nestedList:
            if x.isInteger():
                self.arr.append(x.getInteger())
            else:
                self.decode(x.getList())

    def next(self) -> int:
        """
        Return the next integer
        """
        ans = self.arr[self.i]
        self.i += 1
        return ans

    def hasNext(self) -> bool:
        """
        Return True if there is an following element
        """
        return self.i < self.n
```

## 343. (76%)
```python
def solution(n):
    if n == 2:
        return 1
    if n == 3:
        return 2

    res = 1
    while n > 4:
        n -= 3
        res *=3
    return res*n
```

## 357. (99%)
```python
def solution(n):
    d = dict({0: 1, 1: 10})

    def factorial(n):
        if n in d:
            return d[n]
        res = 1
        for x in range(2, n+1):
            res *= x
        d[n] = res
        return res

    if n == 0:
        return 1
    if n == 1:
        return 10
    res = 1
    for i in range(1, n+1):
        res += (factorial(10)-factorial(9))//factorial(10-i)
    return res
```

## 366.
```python
def solution(root):
        nodes_cur_level = [root]
        while nodes_cur_level:
            nodes_next_level = []
            for node in nodes_cur_level:
                if not node.left and not node.right:
                    node.is_leaf = True
                else:
                    node.is_leaf = False
                if node.left:
                    nodes_next_level.append(node.left)
                if node.right:
                    nodes_next_level.append(node.right)
            nodes_cur_level = nodes_next_level

        res = []
        while not root.is_leaf:
            nodes_cur_level = [root]
            new_leaves = []
            while nodes_cur_level:
                nodes_next_level = []
                for node in nodes_cur_level:
                    if node.left:
                        if node.left.is_leaf:
                            new_leaves.append(node.left.val)
                            node.left = None
                        else:
                            nodes_next_level.append(node.left)
                    if node.right:
                        if node.right.is_leaf:
                            new_leaves.append(node.right.val)
                            node.right = None
                        else:
                            nodes_next_level.append(node.right)
                    if not node.left and not node.right:
                        node.is_leaf = True
                nodes_cur_level = nodes_next_level
            res.append(new_leaves)

        res.append([root.val])
        return res
```

## 376.
```python
def solution(nums):

    n = len(nums)

    if n == 1:
        return 1

    res = 1

    dp_p = [1 for _ in range(n)]
    dp_n = [1 for _ in range(n)]

    for i in range(1, n):
        for j in range(i):
            if nums[i] > nums[j]:
                dp_p[i] = max(dp_p[i], dp_n[j]+1)
            if nums[i] < nums[j]:
                dp_n[i] = max(dp_n[i], dp_p[j]+1)

    return max(max(dp_p), max(dp_n))
```

## 388. (60%)
```python
def solution(input):

    def process_element(s):
        is_file = False
        n = len(s)
        level = 0
        for x in s:
            if x == '\t':
                level += 1

            if x == ".":
                is_file = True
        n -= level
        processed_s = s[-n:]
        return processed_s, n, level, is_file

    res = 0
    element_list = input.split("\n")
    path_stack = []
    n_stack = []
    cur_level = -1

    for s in element_list:
        processed_s, n, level, is_file = process_element(s)
        if level == cur_level + 1:
            cur_level += 1
        else:
            num_levels_to_pop = (cur_level - level) + 1
            for _ in range(num_levels_to_pop):
                if path_stack:
                    path_stack.pop()
                    n_stack.pop()
            cur_level = level

        path_stack.append(processed_s)
        n_stack.append(n)

        if is_file:
            path_length = sum(len(x) for x in path_stack) + cur_level
            res = max(res, path_length)

    return res
```

## 392. (31%)
```python
def solution(s, t):
    if len(s) == 0:
        return True

    if len(t) == 0:
        return False

    i = 0
    for x in t:
        if s[i] == x:
            i += 1
        if i == len(s):
            return True

    return False
```

## 394. (63%)
```python
def solution(s):
    stack = []
    numeric_set = set(["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"])
    num_cache = ""

    for x in s:
        if x == "]":
            str_to_repeat = ""
            while True:
                c = stack.pop()
                if c == "[":
                    n_repeats = int(stack.pop())
                    stack.append(n_repeats*str_to_repeat)
                    break
                else:
                    str_to_repeat = c + str_to_repeat
        elif x in numeric_set:
            num_cache += x
        elif x == "[":
            stack.append(num_cache)
            stack.append(x)
            num_cache = ""
        else:
            stack.append(x)

    return "".join(stack)
```
