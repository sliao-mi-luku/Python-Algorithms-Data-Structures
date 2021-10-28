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
