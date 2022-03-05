## 2. (38%)
```python
def solution(l1, l2):
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
```

## 5. (50%)
```python
def solution(s):
    n = len(s)
    if n == 1:
        return s
    if n == 2:
        return s if s[0]==s[1] else s[0]

    res = s[0]
    for i in range(n-1):
        if s[i] == s[i+1]:
            res = s[i:i+2]

    # odd palidrome
    for i in range(1, n-1):
        left = i-1
        right = i+1
        while s[left] == s[right]:
            if (right-left+1) > len(res):
                res = s[left:right+1]
            left -= 1
            right += 1
            if left < 0 or right >= n:
                break

    # even palindrome
    for i in range(1, n-2):
        if s[i] == s[i+1]:
            left = i-1
            right = i+2
            while s[left] == s[right]:
                if (right-left+1) > len(res):
                    res = s[left:right+1]
                left -= 1
                right += 1
                if left < 0 or right >= n:
                    break

    return res
```

## 15.
```python
def solution(nums):
    res = []
    nums.sort()
    searched = set()

    def twoSum(nums, start_idx, target):
        ans = []
        s = set()
        for i in range(start_idx, len(nums)):
            if nums[i] in s:
                ans.append([nums[i], target-nums[i]])
            s.add(target-nums[i])
        return ans                
    
    for i in range(len(nums)-2):
        if nums[i] > 0:
            break
        target = -nums[i]
        if target in searched:
            continue
        searched.add(target)
        ans = twoSum(nums, i+1, target)
        if ans:
            for y, z in ans:
                sorted_xyz = sorted([nums[i], y, z])
                res.append(tuple(sorted_xyz))

    res = set(res)
    return [[x[0], x[1], x[2]] for x in res]        
```

## 20. (75%)
```python
def solution(s):
    stack = []
    for x in s:
        if x in ["(", "[", "{"]:
            stack.append(x)
        else:
            if not stack:
                return False
            y = stack.pop()
            if y+x not in ["()", "[]", "{}"]:
                return False
    return not stack
```

## 22. (17%)
```python
def solution(n):
    if n == 1:
        return ["()"]

    s = set(["()"])

    for i in range(2, n+1):
        new = set()
        for x in s:
            for i in range(len(x)):
                if x[i] == "(":
                    new.add(x[:i+1] + "()" + x[i+1:])
            new.add("()"+x)

        s = new

    return list(s)
```

## 45. (52%)
```python
def jump(nums):
    n = len(nums)
    last_idx = 0
    cur_idx = 0
    res = 0
    for i in range(n-1):
        cur_idx = max(cur_idx, i+nums[i])
        if i == last_idx:
            res += 1
            last_idx = cur_idx
            if cur_idx > n-1:
                break
    return res
```

## 53. (40%)
```python
def solution(nums):
    res = nums[0]
    cur = nums[0]
    for x in nums[1:]:
        cur = max(cur+x, x)
        res = max(res, cur)
    return res
```

## 55. (51%)
```python
def solution(nums):
    n = len(nums)
    max_idx = 0
    for i in range(n):
        if i > max_idx:
            return False
        max_idx = max(max_idx, i + nums[i])
        if max_idx >= n-1:
            return True
    return False
```

## 56.
```python
def solution(intervals):
    intervals.sort(key=lambda x: (x[0], x[1]))
    stack = []
    for x in intervals:
        if not stack:
            stack.append(x)
        else:
            if stack[-1][1] < x[0]:
                stack.append(x)
            else:
                y = stack.pop()
                if y[1] < x[1]:
                    stack.append([y[0], x[1]])
                else:
                    stack.append([y[0], y[1]])
    return stack
```

## 57. (58%)
```python
def solution(intervals, newInterval):
    res = []

    if not intervals:
        return [newInterval]

    a, b = newInterval

    if a > intervals[-1][-1]:
        return intervals + [newInterval]

    if b < intervals[0][0]:
        return [newInterval] + intervals

    while intervals:
        x, y = intervals.pop(0)

        if b < x:
            return res + [[a, b], [x, y]] + intervals

        if a > y:
            res.append([x, y])
            continue

        if a >= x and b <= y:
            return res + [[x, y]] + intervals

        if a >= x:
            a = x

        if b <= y:
            b = y

    return res + [[a, b]]
```
## 59. (76%)
```python
def solution(n):

    grid = [[0 for _ in range(n)] for _ in range(n)]

    left = 0
    right = n-1
    top = 0
    bottom = n-1
    x = 1

    while left <= right and top <= bottom:

        for i in range(left, right+1):
            grid[top][i] = x
            x += 1

        top += 1

        for i in range(top, bottom+1):
            grid[i][right] = x
            x += 1

        right -= 1

        for i in range(right, left-1, -1):
            grid[bottom][i] = x
            x += 1

        bottom -= 1

        for i in range(bottom, top-1, -1):
            grid[i][left] = x
            x += 1

        left += 1

    return grid
```

## 62. (73%)
```python
def solution(m, n):
    dp = [[1]*m]*n
    for i in range(1, n):
        for j in range(1, m):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    return dp[-1][-1]
```

## 63. (61%)
```python
def solution(obstacleGrid):
    m = len(obstacleGrid)
    n = len(obstacleGrid[0])
    dp = [[0 for _ in range(n)] for _ in range(m)]

    for i in range(m):
        if obstacleGrid[i][0] == 0:
            dp[i][0] = 1
        else:
            break

    for j in range(n):
        if obstacleGrid[0][j] == 0:
            dp[0][j] = 1
        else:
            break

    for i in range(1, m):
        for j in range(1, n):
            if obstacleGrid[i][j] == 1:
                continue
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[-1][-1]
```

## 64. (92%)
```python
def solution(grid):
    n = len(grid)
    m = len(grid[0])
    dp = [[0 for _ in range(m)] for _ in range(n)]
    dp[0][0] = grid[0][0]        

    for i in range(1, n):
        dp[i][0] = dp[i-1][0] + grid[i][0]

    for j in range(1, m):
        dp[0][j] = dp[0][j-1] + grid[0][j]

    for i in range(1, n):
        for j in range(1, m):
            dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j]

    return dp[-1][-1]
```

## 70. (95%)
```python
def solution(n):
    if n == 1:
        return 1
    if n == 2:
        return 2
    dp = [1] + [2] + [0 for _ in range(n-2)]
    for i in range(2, n):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[-1]
```

## 71. (98%)
```python
def solution(path):
    history = []
    path = path.split('/')

    for x in path:
        if not x or x == ".":
            continue

        if x == "..":
            if len(history) >= 1:
                history.pop()
        else:
            history.append(x)

    return "/" + "/".join(history)
```

## 91. (89%)
```python
def solution(s):
    n = len(s)
    dp = [0 for _ in range(n)]

    if s[0] != "0":
        dp[0] = 1
    else:
        return 0

    if n == 1:
        return dp[0]

    if int(s[:2]) in range(11, 20):
        dp[1] = 2
    elif int(s[:2]) in range(21, 27):
        dp[1] = 2
    elif s[1] == "0" and s[0] not in ["1", "2"]:
        dp[1] = 0
    else:
        dp[1] = dp[0]

    for i in range(2, n):
        if s[i-1] in ["0", "3", "4", "5", "6", "7", "8", "9"]:
            if s[i] == "0":
                dp[i] = 0
            else:
                dp[i] = dp[i-1]
        elif s[i-1] == "2":
            if s[i] == "0":
                dp[i] = dp[i-2]
            elif s[i] in ["1", "2", "3", "4", "5", "6"]:
                dp[i] = dp[i-2] + dp[i-1]
            else:
                dp[i] = dp[i-1]
        else: # "1"
            if s[i] == "0":
                dp[i] = dp[i-2]
            else:
                dp[i] = dp[i-2] + dp[i-1]

    return dp[-1]
```

## 94. (89%)
```python
def solution(root):

    def recursion(node, traversal=[]):
        if node:
            if node.left:
                traversal = recursion(node.left, traversal)
            traversal.append(node.val)
            if node.right:
                traversal = recursion(node.right, traversal)
            return traversal

    return recursion(root, [])
```

## 95. (80%)
```python
def solution(n):
    d = dict()

    def recursion(start, end):
        if (start, end) in d:
            return d[(start, end)]
        if start > end:
            return [None]

        res = []
        for x in range(start, end+1):
            left = recursion(start, x-1)
            right = recursion(x+1, end)
            for L in left:
                for R in right:
                    node = TreeNode(x)
                    node.left = L
                    node.right = R
                    res.append(node)
        d[(start, end)] = res
        return res

    return recursion(1, n)
```

## 96. (12%)
```python
def solution(n):
    dp = [0 for _ in range(n+1)]
    dp[0] = 1

    for i in range(1, n+1):
        for r in range(i):
            dp[i] += dp[r] * dp[i-r-1]

    return dp[-1]
```

## 97. (46%)
```python
def solution(s1, s2, s3):
    n1, n2, n3 = len(s1), len(s2), len(s3)

    if n1 + n2 != n3:
        return False

    if n1 == n2 == n3 == 0:
        return True

    # dp[i+1][j+1]: s3[0:i+j+1] is interleaved by s1[0:i+1] and s2[0:j+1]
    dp = [[False for _ in range(n2+1)] for _ in range(n1+1)]

    dp[0][0] = True
    for i in range(n1):
        if s1[i] == s3[i]:
            dp[i+1][0] = True
        else:
            break

    for j in range(n2):
        if s2[j] == s3[j]:
            dp[0][j+1] = True
        else:
            break

    for i in range(n1):
        for j in range(n2):
            # see if s1[0], ..., s1[i] and s2[0], ..., s2[j] combine to s3[0], ..., s3[i+j]
            if s1[i] == s3[i+j+1] and dp[i][j+1]:
                dp[i+1][j+1] = True
            elif s2[j] == s3[i+j+1] and dp[i+1][j]:
                dp[i+1][j+1] = True

    return dp[-1][-1]
```

## 98.
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
    for i in range(len(traversal)-1):
        if traversal[i+1] <= traversal[i]:
            return False
    return True
```

## 99. (82%)
```python
def solution(root):

    def inorder(node, traversal_vals, traversal_nodes):
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
```
