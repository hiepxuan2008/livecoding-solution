# Dynamic Programming 2 - Live Coding Solutions

Speaker: Mai Thanh Hiep

## 1. Longest Increasing Subsequence

Problem link: https://leetcode.com/problems/longest-increasing-subsequence/

**✔️ Solution 1: Dynamic Programming**

- Let `dp[i]` is the longest increase subsequence of `nums[0..i]` which has `nums[i]` as the end element of the subsequence.

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [1] * n
        for i in range(n):
            for j in range(i):
                if nums[i] > nums[j] and dp[i] < dp[j] + 1:
                    dp[i] = dp[j] + 1
        return max(dp)
```

**BONUS: Backtrack to find the Longest Increasing Subsequence**

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        
        dp = [1] * n
        trace = [-1] * n
        
        resLen = 0
        resIdx = -1 
        for i in range(n):
            for j in range(i):
                if nums[i] > nums[j] and dp[i] < dp[j] + 1:
                    dp[i] = dp[j] + 1
                    trace[i] = j  # i point to j
                    
            if resLen < dp[i]:
                resLen = dp[i]
                resIdx = i
            
        lcs = []
        t = resIdx
        while t != -1:
            lcs.append(nums[t])
            t = trace[t]
        print("Path: ", lcs[::-1]) 
        
        return max(dp)
```



**✔️ Solution 2: Geedy + Binary Search, BIT** độ phức tạp O(NlogN)

- Xem tại: https://leetcode.com/problems/longest-increasing-subsequence/discuss/1326308



## 2. Longest Common Subsequence

Problem link: https://leetcode.com/problems/longest-common-subsequence/

Ý tưởng:

- Gọi `dp[i][j]` độ dài Longest Common Subsequence của string `string s1[0..i-1]` và string `s2[0..j-1]`.

```python
class Solution:
    def longestCommonSubsequence(self, s1: str, s2: str) -> int:
        m, n = len(s1), len(s2)
        dp = [[0] * (n+1) for _ in range(m+1)]
        for i in range(m+1):
            for j in range(n+1):
                if i == 0 or j == 0:
                    dp[i][j] = 0
                elif s1[i-1] == s2[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
                    
        return dp[m][n]
```

**BONUS: Backtrack to find the Longest Common Subsequence**

```python
class Solution:
    def longestCommonSubsequence(self, s1: str, s2: str) -> int:
        m, n = len(s1), len(s2)
        dp = [[0] * (n+1) for _ in range(m+1)]
        for i in range(m+1):
            for j in range(n+1):
                if i == 0 or j == 0:
                    dp[i][j] = 0
                elif s1[i-1] == s2[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
                    
        i, j = m, n
        lcs = []
        while i > 0 and j > 0:
            if s1[i-1] == s2[j-1]:
                lcs.append(s1[i-1])
                i -= 1
                j -= 1
            elif dp[i][j] == dp[i-1][j]:
                i -= 1
            else:
                j -= 1
        
        print("LCS: ", lcs[::-1])

        return dp[m][n]
                    
```



## 3. Edit Distance

Problem link: https://leetcode.com/problems/edit-distance/

Solution: https://leetcode.com/problems/edit-distance/discuss/1475220



## 4. Campus Bikes II

Problem link: https://leetcode.com/problems/campus-bikes-ii/

- Let define:
  - `m` is number of bikes
  - `n` is number of workers
- Let `dp(workerId, mask)` the minimum possible sum of Manhattan distances between each worker and their assigned bike, after assigning bikes to `[workerId..n-1]` workers, such that:
  - `mask` represent the state that if `i_th` bit of mask is:
    - == 1 then `i_th` bike is unused
    - == 0 then `i_th` bike is used
- `dp(0, (1 << m) - 1)` is our result, where `(1 << m) - 1` means we create a mask with `m` 1-bit, it means all the bikes are available to use.

```python
class Solution:
    def assignBikes(self, workers: List[List[int]], bikes: List[List[int]]) -> int:
        m, n = len(bikes), len(workers)
        
        def manhattanDist(p1, p2):
            return abs(p1[0] - p2[0]) + abs(p1[1] - p2[1])
        
        @lru_cache(None)
        def dp(workerId, mask):
            if workerId == n:
                return 0
            
            ans = math.inf
            for bikeId in range(m):
                if (mask >> bikeId) & 1:
                    newMask = mask ^ (1 << bikeId)
                    ans = min(ans, manhattanDist(workers[workerId], bikes[bikeId]) + dp(workerId+1, newMask))
            return ans
        
        return dp(0, (1 << m) - 1)
```



