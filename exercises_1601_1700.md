## 1614 (96%)
```python
def solution(s):

    res = 0
    cur = 0

    for x in s:
        if x == "(":
            cur += 1

        elif x == ")":
            res = max(res, cur)
            cur -= 1

    return res
```

## 1653. (84%)
```python
def solution(s):
    res = 0
    b_counts = 0
    for x in s:
        if x == "a":
            res = min(b_counts, res + 1)
        else:
            b_counts += 1

    return res
```

## 1673. (46%)
```python
def solution(nums, k):
    n = len(nums)
    stack = []
    n_futures = n

    for i, x in enumerate(nums):
        n_futures -= 1
        while stack and (len(stack) + n_futures >= k) and (x < stack[-1]):
            stack.pop()
        if len(stack) < k:
            stack.append(x)

    return stack
```

## 1700. (65%)
```python
def countStudents(students, sandwiches):

    while True:
        if sandwiches[0] not in set(students):
            return len(students)

        j = 0 #sandwich

        for i, x in enumerate(students):
            if x == sandwiches[j]:
                j += 1
                if j == len(sandwiches):
                    return 0
            else:
                students = students[i+1:] + [x]
                sandwiches = sandwiches[j:]
                break
```
