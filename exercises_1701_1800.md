## 1717 (80%)
```python
def solution(s, x, y):

    if len(s) == 1:
        return 0

    stack = ["x"]
    res = 0

    if x >= y:
        large_word, small_word = "ab", "ba"
        large_score, small_score = x, y

    else:
        large_word, small_word = "ba", "ab"
        large_score, small_score = y, x

    # remove large words
    for c in s:
        if c == large_word[1] and stack[-1] == large_word[0]:
            res += large_score
            stack.pop()
        else:
            stack.append(c)

    new_stack = ["x"]
    # remove small words
    for c in stack:
        if c == small_word[1] and new_stack[-1] == small_word[0]:
            res += small_score
            new_stack.pop()
        else:
            new_stack.append(c)

    return res
```

## 1762.
```python
def solution(heights):
    n = len(heights)
    res = [n-1]

    for i in range(n-2, -1, -1):
        if heights[i] > heights[res[-1]]:
            res.append(i)

    res.reverse()

    return res
```
