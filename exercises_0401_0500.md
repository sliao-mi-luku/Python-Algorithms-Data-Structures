## 402. (96%)
```python
def solution(num, k):
    stack = []

    for i, x in enumerate(num):
        if not stack:
            stack.append(x)
        else:
            while k and stack[-1] > x:
                stack.pop()
                k -= 1
                if not stack:
                    break
            stack.append(x)

        if k == 0:
            res = "".join(stack) + num[i+1:]
            res = res.lstrip("0")
            if not res:
                return "0"
            else:
                return res

    if k != 0:
        res = "".join(stack[:-k]).lstrip("0")
        if not res:
            return "0"
        else:
            return res
```

## 445. (56%)
```python
class Solution:
    def solution(self, l1, l2):
        s1 = self.decode(l1)
        s2 = self.decode(l2)
        res_str = self.add_two_strings(s1, s2)
        return self.encode(res_str)

    def encode(self, s):
        root = ListNode(int(s[0]))
        cur = root
        for x in s[1:]:
            cur.next = ListNode(int(x))
            cur = cur.next
        return root

    def decode(self, node):
        res = ""
        cur = node
        while cur:
            res += str(cur.val)
            cur = cur.next
        return res

    def add_two_strings(self, s1, s2):
        if len(s2) > len(s1):
            s1, s2 = s2, s1
        if s2 == "0":
            return s1
        res = ""
        i, j = len(s1)-1, len(s2)-1
        leftover = 0
        while j >= 0:
            summation = int(s1[i]) + int(s2[j]) + leftover
            res = str(summation % 10) + res
            leftover = summation // 10
            i -= 1
            j -= 1

        while i >= 0:
            summation = int(s1[i]) + leftover
            res = str(summation % 10) + res
            leftover = summation // 10
            i -= 1

        if leftover:
            res = str(leftover) + res
        return res
```

## 472. (70%)
```python
def solution(words):

    if len(words) < 2:
        return []

    words.sort(key=lambda x: len(x))

    wordDict = set(words)

    res = []

    def check(s):
        n = len(s)
        dp = [False for _ in range(n+1)]
        dp[0] = True

        for i in range(1, n+1):
            for j in range(i):
                if (dp[j] and (s[j:i] in wordDict)):
                    dp[i] = True
                    break
        return dp[-1]

    while words:
        s = words.pop()
        wordDict.remove(s)
        if s and check(s):
            res.append(s)

    return res
```
