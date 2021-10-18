### 1404.
40%
```python
def numSteps(s):

    def divide_by_two(num_str):
        ans = ""
        carry = 0
        for x in num_str:
            ans += str((int(x) + 10*carry) // 2)
            carry = (int(x) + 10*carry) % 2
        ans = ans.lstrip("0")
        return ans

    def convert_to_binary(num_str):
        ans = ""
        while num_str:
            if num_str[-1] in ["1", "3", "5", "7", "9"]: # odd
                ans = "1" + ans # update binary
                num_str = num_str[:-1] + str(int(num_str[-1])-1) # minus 1
            else: # even
                ans = "0" + ans # update binary
            # divide by 2
            num_str = divide_by_two(num_str)
        return ans

    res = 0

    while len(s) != 1:
        if s[-1] == "0": # even
            res += 1
            s = s[:-1]
        else: # odd -> +1
            m = len(s)
            i = m-2
            while s[i] == "1":
                i -= 1
                if i == -1:
                    return res + m + 1
            res += (m-i)
            s = s[:i] + "1"

    return res
```