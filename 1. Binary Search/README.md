# Binary Search (BASIC) - Live Coding Solutions

Speaker: Mai Thanh Hiep

## 1. Binary Search - Basic

Link problem: https://leetcode.com/problems/binary-search/

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:  # Found target -> Return index
                return mid
            elif nums[mid] > target:  # Target are in the left side
                right = mid - 1
            else:
                left = mid + 1  # Target are in the right side
        return -1
```

Complexity:

- Time: `O(logN)`, where `N` is length of `nums` array.
- Space: `O(1)`



## 2. Binary Search - lower_bound

```python
def lowerBound(nums, target):
    left = 0
    right = len(nums) - 1
    ans = len(nums)
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] >= target:
            ans = mid  # update the best result so far
            right = mid - 1  # search better result on the left side
        else:
            left = mid + 1  # search result on the right side
    return ans
```

Complexity:

- Time: `O(logN)`, where `N` is length of `nums` array.
- Space: `O(1)`



## 3. Binary Search - upper_bound

```python
def upperBound(nums, target):
    left = 0
    right = len(nums) - 1
    ans = len(nums)
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] > target:  
            ans = mid  # update the best result so far
            right = mid - 1  # search better result on the left side
        else:
            left = mid + 1  # search result on the right side
    return ans
```

Complexity:

- Time: `O(logN)`, where `N` is length of `nums` array.
- Space: `O(1)`



## 4. Find First and Last Position of Element in Sorted Array

Problem link: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        # 1 2 4 4 7, target = 4
        # bisect_left(arr, 4) = 2
        # bisect_left(arr, 3) = 2
        # bisect_left(arr, 0) = 0
        # bisect_left(arr, 8) = 5
        idxLeft = bisect_left(nums, target)
        if idxLeft == len(nums) or nums[idxLeft] != target:
            return [-1, -1]
        
        
        # 1 2 4 4 7, target = 4
        # bisect_right(arr, 4) = 4
        # bisect_right(arr, 3) = 2
        # bisect_right(arr, 0) = 0
        # bisect_right(arr, 8) = 5
        idxRight = bisect_right(nums, target)
        return [idxLeft, idxRight - 1]
```

Complexity:

- Time: `O(logN)`, where `N` is length of `nums` array.
- Space: `O(1)`


## 5. Compute the Square Root of x, Sqrt(x), return truncated integer

Problem link: https://leetcode.com/problems/sqrtx/

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        # Comment:
        # - Search Range: [0, 46340]
        # - Co tinh chat dong bien
        #   + mid tang -> mid * mid se tang
        #   + mid giam -> mid * mid se giam
        ans = 0
        left = 0
        right = 46340
        ans = 0
        while left <= right:
            mid = (left + right) // 2
            if mid * mid <= x:
                ans = mid
                left = mid + 1  # Search the larger ans in the right side
            else:
                right = mid - 1
        return ans
```

Complexity:

- Time: `O(log(46340))`
- Space: `O(1)`


## 6. Compute real Square Root of x, Sqrt(x), return double value

```python
class Solution:
    def mySqrt(self, x: int) -> float:
        left = 0
        right = 46340.95
        EPSILON = 1e-12

        while right - left > EPSILON:
            mid = (left + right) / 2
            if mid * mid == x:
                return mid
            if mid * mid < x:
                left = mid
            else:
                right = mid

        return left
```

Complexity:

- Time: `O(log(46340 / s))`, where `s = 10^-12` is the tolerance.
- Space: `O(1)`



## 7. First Bad Version

Problem link: https://leetcode.com/problems/first-bad-version/

```python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        left = 1
        right = n
        ans = -1
        while left <= right:
            mid = left + (right - left) // 2
            if isBadVersion(mid):
                ans = mid  # update best result so far
                right = mid - 1
            else:
                left = mid + 1
        return ans
```

Complexity:

- Time: `O(logN)`
- Space: `O(1)`


## 8. Find Minimum in Rotated Sorted Array

Problem link: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if (mid == left or nums[mid-1] > nums[mid]) and (mid == right or nums[mid] < nums[mid+1]):
                return nums[mid]
            if nums[mid] > nums[right]:
                left = mid + 1
            else:
                right = mid - 1
```

Complexity:

- Time: `O(logN)`, where `N` is length of `nums` array.
- Space: `O(1)`
