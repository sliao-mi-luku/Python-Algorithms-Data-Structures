## 636. (53%)
```python
def solution(n, logs):
    infos = []

    for log in logs:
        info = log.split(":")
        infos.append([int(info[0]), 0 if info[1]=='start' else 1, int(info[2])])

    infos.sort(key=lambda x: (x[2], x[1]), reverse=True)

    last_start = dict()
    res = [0 for _ in range(n)]
    func_waitline = []
    cur_func = -1

    while infos:
        (func_i, status, time) = infos.pop()

        if status == 0: # func start
            # conclude the previous func
            if cur_func != -1:
                res[cur_func] += (time - last_start[cur_func])
                func_waitline.append(cur_func)
            # switch to the new func
            cur_func = func_i
            last_start[func_i] = time

        else: # func end
            time += 1
            # conclude the cur_func
            res[cur_func] += (time - last_start[cur_func])
            # move on to process the last paused function
            if func_waitline:
                cur_func = func_waitline.pop()
                last_start[cur_func] = time
            else:
                cur_func = -1

    return res    
```

## 646.
```python
def solution(pairs):
    n = len(pairs)

    pairs.sort(key=lambda x: (x[1], x[0]))

    cur = -1001
    res = 0

    for x, y in pairs:
        if x > cur:
            res += 1
            cur = y

    return res
```


## 654. (81%)
```python
class Solution:
    def solution(self, nums):

        if not nums:
            return None

        max_val = max(nums)
        max_index = nums.index(max_val)

        root = TreeNode(max_val)
        root.left = self.solution(nums[:max_index])
        root.right = self.solution(nums[max_index+1:])

        return root
```

## 678. (97%)
```python
def solution(s):
    n = len(s)

    if s[-1] == "(" or s[0] == ")":
        return False

    stack_star = []
    stack_left = []

    for i, x in enumerate(s):
        if x == "*":
            stack_star.append(i)
        elif x == "(":
            stack_left.append(i)
        else: # ")"
            if not stack_star and not stack_left:
                return False
            if stack_left:
                stack_left.pop()
            else:
                stack_star.pop()

    while stack_left and stack_star:
        if stack_left.pop() >  stack_star.pop():
            return False

    return not stack_left
```

## 680.
```python
def solution(s):
    def check(s, deletion_used=False):
        left = 0
        right = len(s)-1

        while left < right:
            if s[left] == s[right]:
                left += 1
                right -= 1
            else:
                if deletion_used:
                    return False
                else:
                    return check(s[left:right], True) or check(s[left+1:right+1], True)
        return True

    return check(s, False)
```

## 687.
```python
def solution(root):
    if not root:
        return 0

    res = 0

    def recursion(node):
        nonlocal res
        if not node:
            return 0

        left = recursion(node.left)
        right = recursion(node.right)

        if node.left and node.left.val == node.val:
            left += 1
        else:
            left = 0

        if node.right and node.right.val == node.val:
            right += 1
        else:
            right = 0

        res = max(res, left+right)
        return max(left, right)    

    _ = recursion(root)
    return res
```

## 695. (55%)
```python
def solution(self, grid):

    n, m = len(grid), len(grid[0])
    res = 0

    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1:
                self.cur = 0
                self.dfs(grid, i, j, n, m)
                res = max(res, self.cur)
    return res

def dfs(self, grid, i, j, n, m):

    if any([i < 0, j < 0, i >= n, j >= m]):
        return

    if grid[i][j] == 0:
        return

    grid[i][j] = 0
    self.cur += 1

    self.dfs(grid, i-1, j, n, m)
    self.dfs(grid, i+1, j, n, m)
    self.dfs(grid, i, j-1, n, m)
    self.dfs(grid, i, j+1, n, m)
```
