## 1201. Ugly Number III
```python
class Solution:
    def nthUglyNumber(n, a, b, c):

        def find_gcd(x, y):
            while y:
                x, y = y, (x % y)
            return x

        def find_lcm(x, y):
            return x * y // find_gcd(x, y)

        def count_ugly(x):
            ans = x//a + x//b + x//c
            ans -= (x//lcm_ab + x//lcm_bc + x//lcm_ac)
            ans += (x//lcm_abc)
            return ans

        lcm_ab = find_lcm(a, b)
        lcm_bc = find_lcm(b, c)
        lcm_ac = find_lcm(a, c)
        lcm_abc = find_lcm(lcm_ab, c)

        ## binary search
        left, right = 1, int(2e9)+1

        while left < right:
            mid = left + (right-left)//2
            num_ugly = count_ugly(mid)
            if num_ugly < n:
                left = mid + 1
            else:
                right = mid

        return left

"""
Runtime: 90%
"""
```
