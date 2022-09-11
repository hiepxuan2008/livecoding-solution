# Two Pointers - Sliding Window - Live Coding Solutions

Speaker: Mai Thanh Hiep


## 1. Two Sum II - Input Array Is Sorted

Link problem: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        left = 0
        right = len(nums) - 1
        while left < right:
            if nums[left] + nums[right] == target:
                return [left + 1, right + 1]
            
            if nums[left] + nums[right] > target:
                right -= 1
            else:
                left += 1
```

Complexity:

- Time: `O(N)`, where `N` is length of `nums` array.
- Space: `O(1)`



## 2. 3Sum

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        
        n = len(nums)
        ans = set()
        for i in range(n-2):
            left = i + 1
            right = n - 1
            target = -nums[i]
            while left < right:
                if nums[left] + nums[right] == target:
                    ans.add((nums[i], nums[left], nums[right]))
                    left += 1
                    right -= 1
                elif nums[left] + nums[right] > target:
                    right -= 1
                else:
                    left += 1
        return ans
```

Complexity:

- Time: `O(N^2)`, where `N` is length of `nums` array.
- Extra Space (without counting output as space): `O(sorting)`



## 3. 3Sum Smaller

Problem link: https://leetcode.com/problems/3sum-smaller/

Solution: https://leetcode.com/problems/3sum-smaller/discuss/1340687/



## 4. Minimum Size Subarray Sum

Problem link: https://leetcode.com/problems/minimum-size-subarray-sum/

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l = 0
        curSum = 0
        ans = math.inf
        for r, num in enumerate(nums):
            curSum += num
            while curSum >= target:
                ans = min(ans, r - l + 1)
                curSum -= nums[l]
                l += 1
        return 0 if ans == math.inf else ans
```

Complexity:

- Time: `O(N)`, where `N` is length of `nums` array.
- Space: `O(1)`



## 5. Longest Substring Without Repeating Characters

Problem link: https://leetcode.com/problems/longest-substring-without-repeating-characters/

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l = 0
        lastIndex = [-1] * 128
        ans = 0
        for r, c in enumerate(s):
            if lastIndex[ord(c)] >= l:
                l = lastIndex[ord(c)] + 1
            ans = max(ans, r - l + 1)
            lastIndex[ord(c)] = r
        return ans
```

Complexity:

- Time: `O(N)`, where `N` is length of string `s`
- Space: `O(1)`



## 6. Find All Anagrams in a String

Problem link: https://leetcode.com/problems/find-all-anagrams-in-a-string/

Solution: https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/639309



## 7. Longest Substring with At Most K Distinct Characters

Problem link: https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/

```python
class Solution:
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        l = 0
        cnt = Counter()
        ans = 0
        for r, c in enumerate(s):
            cnt[c] += 1
            
            while len(cnt) > k:
                cnt[s[l]] -= 1
                if cnt[s[l]] == 0:
                    cnt.pop(s[l])
                l += 1
            
            ans = max(ans, r - l + 1)
        return ans
            
```

Complexity:

- Time: `O(N)`, where `N` is length of string `s`.
- Space: `O(1)`



