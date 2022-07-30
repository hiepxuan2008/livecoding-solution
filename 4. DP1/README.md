# Dynamic Programming 1 - Live Coding Solutions

Speaker: Mai Thanh Hiep

## 1. Fibonacci Number

Problem link: https://leetcode.com/problems/fibonacci-number/



**✔️ Solution 1: Recursion**

```python
class Solution:
    def fib(self, n: int) -> int:
        if n <= 1: return n
        return self.fib(n-1) + self.fib(n-2)
```

Complexity:

- Time: `O(2^n)`
- Space: `O(n)`, it's the stack memory depth



**✔️ Solution 2: Recursion + Memoization (Top down DP)**

```python
memo = {}

class Solution:
    def fib(self, n: int) -> int:
        if n <= 1: return n
        if n in memo: return memo[n]
        memo[n] = self.fib(n-1) + self.fib(n-2)
        return memo[n]
```

or

```python
class Solution:
    @lru_cache(None)  # Least recently usage cache
    def fib(self, n: int) -> int:
        if n <= 1: return n
        return self.fib(n-1) + self.fib(n-2)
```

Complexity:

- Time: `O(n)`
- Space: `O(n)`, it's the stack memory depth or memo cache



**✔️ Solution 3: Tabulation (Bottom up DP)**

```python
class Solution:
    def fib(self, n: int) -> int:
        if n <= 1: return n
        dp = [0] * (n+1)
        dp[0] = 0
        dp[1] = 1
        for i in range(2, n+1):
            dp[i] = dp[i-1] + dp[i-2]
            
        return dp[n]
```

Complexity:

- Time: `O(n)`
- Space: `O(n)`

**✔️ Solution 4: Tabulation (Bottom up DP) & Space Optimized**

```python
class Solution:
    def fib(self, n: int) -> int:
        if n <= 1: return n
        dpPrev2 = 0
        dpPrev1 = 1
        dpCur = 0
        
        for i in range(2, n+1):
            dpCur = dpPrev1 + dpPrev2
            dpPrev2 = dpPrev1
            dpPrev1 = dpCur
            
        return dpCur
```

Complexity:

- Time: `O(n)`
- Space: `O(1)`



## 2. Decode Ways

Problem link: https://leetcode.com/problems/decode-ways/

Solution: https://leetcode.com/problems/decode-ways/discuss/1410794



## 3. Unique Paths

Problem link: https://leetcode.com/problems/unique-paths/

Solution: https://leetcode.com/problems/unique-paths/discuss/254228



## 4. Word Break

Problem link: https://leetcode.com/problems/word-break/

Solution: https://leetcode.com/problems/word-break/discuss/1455100



## 5. Coin Change

Problem link: https://leetcode.com/problems/coin-change/

Solution: https://leetcode.com/problems/coin-change/discuss/1475250



## 6. Longest Palindromic Substring

Problem link: https://leetcode.com/problems/longest-palindromic-substring/

Solution: https://leetcode.com/problems/longest-palindromic-substring/discuss/1024769



