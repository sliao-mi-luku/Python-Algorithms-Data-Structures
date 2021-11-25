## 213. (69%)
```python
def solution(nums):
    def dynamic(arr):
        n = len(arr)
        if n == 1:
            return arr[0]
        dp = [0 for _ in range(n)]
        dp[0] = arr[0]
        dp[1] = max(arr[0], arr[1])
        for i in range(2, n):
            dp[i] = max(dp[i-1], dp[i-2]+arr[i])
        return dp[-1]

    n = len(nums)
    if n == 1:
        return nums[0]
    if n == 2:
        return max(nums)
    return max(dynamic(nums[1:]), dynamic(nums[:-1]))
```

## 214. (62%)
```python
def solution(s):

    if len(s) in [0, 1]:
        return s

    def build_nxt(s):
        """
        KMP
        """
        nxt = [0, 0]
        j = 0
        for i in range(1, len(s)):
            while j > 0 and s[i] != s[j]:
                j = nxt[j]
            if s[i] == s[j]:
                j += 1
            nxt.append(j)
        return nxt

    q = s + "#" + s[::-1]

    nxt = build_nxt(q)

    prefix = s[nxt[-1]:][::-1]

    return prefix + s
```

## 227. (54%)
```python
def solution(s):
    stack = []
    cur = ""
    for x in s:
        if x == " ":
            continue
        elif x in ["+", "-", "*", "/"]:
            stack.append(int(cur))
            stack.append(x)
            cur = ""
        else:
            cur += x
    if cur:
        stack.append(int(cur))

    new_stack = []
    i = 0

    while i < len(stack):
        if stack[i] == "+":
            i += 1
            continue
        elif stack[i] == "-":
            new_stack.append(-stack[i+1])
            i += 2
        elif stack[i] == "*":
            new_stack.append(new_stack.pop()*stack[i+1])
            i += 2
        elif stack[i] == "/":
            new_stack.append(int(new_stack.pop()/stack[i+1]))
            i += 2
        else:
            new_stack.append(stack[i])
            i += 1

    return sum(new_stack)            
```

## 234. (60%)
```python
def solution(head):
    arr = []
    cur = head
    while cur:
        arr.append(cur.val)
        cur = cur.next
    i = 0
    j = len(arr)-1
    while i < j:
        if arr[i] != arr[j]:
            return False
        i += 1
        j -= 1
    return True
```

## 263. (90%)
```python
def solution(n):
    if n <= 0:
        return False

    for x in [2, 3, 5]:
        while n % x == 0:
            n /= x

    return (n == 1)
```

## 264. (66%)
```python
def solution(n):

    if n == 1:
        return 1

    a = [2]
    b = [3]
    c = [5]

    i, j, k = 0, 0, 0

    res = 1

    while n != 1:
        if a[i] == res:
            i += 1
        if b[j] == res:
            j += 1
        if c[k] == res:
            k += 1

        res = min(a[i], b[j], c[k])

        a.append(res*2)
        b.append(res*3)
        c.append(res*2)

        n -= 1

    return res
```
