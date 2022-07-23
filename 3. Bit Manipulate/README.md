# Bit Manipulation - Live Coding Solutions

Speaker: Mai Thanh Hiep

Lecture slide: https://docs.google.com/presentation/d/1xP_DApsIHGzGYmpoNDznCI5XDmp2f5AffLwelHsiv3Q/edit?usp=sharing 



## 1. Basic Bitwise Combination

```python
# Get kth bit of number x
def getBit(x, k):
    return (x >> k) & 1

# Turn kth bit of number x to 1
def setBit(x, k):
    return x | (1 << k)

# Set kth bit of number x to 0
def clearBit(x, k):
    return x & (~(1 << k))

# Toggle kth bit of number x
def toggleBit(x, k):
    return x ^ (1 << k)
```

Complexity:

- Time: `O(1)`
- Space: `O(1)`



## 2. Number of 1 Bits

Problem link: https://leetcode.com/problems/number-of-1-bits/

```python
class Solution:
    def hammingWeight(self, num: int) -> int:
        ans = 0
        for i in range(32):
            if (num >> i) & 1:  # if ith bit of num == 1
                ans += 1
        return ans
```

Complexity:

- Time: `O(1)`
- Space: `O(1)`

## 3. Reverse Bits

Problem link: https://leetcode.com/problems/reverse-bits/

```python
class Solution:
    def reverseBits(self, num: int) -> int:
        def getBit(x, k):
            return (x >> k) & 1
        
        def clearBit(x, k):
            return x & (~(1 << k))

        def setBit(x, k, v):
            if v == 0:
                return clearBit(x, k)
            return x | (1 << k)

        
        # def swapArr(arr, i, j):
        #     tmp = arr[i]
        #     arr[i] = arr[j]
        #     arr[j] = tmp
        
        def swapBit(num, i, j):
            bit = getBit(num, i)
            num = setBit(num, i, getBit(num, j))
            return setBit(num, j, bit)
        
        left = 0
        right = 31
        while left < right:
            num = swapBit(num, left, right)
            left += 1
            right -= 1
        return num
```

Complexity:

- Time: `O(1)`
- Space: `O(1)`



## 5. Single Number

Problem link: https://leetcode.com/problems/single-number/

Idea:

- We can see that:
  - `X ^ X = 0`
  - `X ^ 0 = X`
- Since there is one element appearing once, all other elements appearing twice, we can xor all elements in `nums` array together to get the single one.

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        ans = 0
        for num in nums:
            ans ^= num
        return ans
```

Complexity:

- Time: `O(N)`
- Space: `O(1)`



## 6. Subsets

Problem link: https://leetcode.com/problems/subsets/

Idea:

- Let `mask` represent the state of each subsets, that is:
  - `i_th` bit of `mask` represents the appearance of `nums[i]` in that subset
  - There are total `2^n` subsets, where `n` is length of `nums` array.
  - `mask` has states in range `[0..2^n-1]`
- For example: `nums = [1, 2, 3]`
  - There are total `2^3` subsets: `[], [1], [2], [3], [1, 2], [1, 3], [2, 3], [1, 2, 3]`
  - There are total `2^3` mask states in range `[0..7]`

| Mask Value | Binary Presentation | Subset |
| :-------------: | :-------------: | :-------------: |
| 0 | 000 | [] |
| 1 | 001 | [1] |
| 2 | 010 | [2] |
| 3 | 011 | [1, 2] |
| 4 | 100 | [3] |
| 5 | 101 | [1, 3] |
| 6 | 110 | [2, 3] |
| 7 | 111 | [1, 2, 3] |


```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        ans = []
        for mask in range(1 << n):
            arr = []
            for i in range(n):
                if (mask >> i) & 1:
                    arr.append(nums[i])
            ans.append(arr)
        return ans
```

Complexity:

- Time: `O(2^N * N)`, where `N` is number of elements in `nums` array.
- Space: `O(2^N)`



## 7. Valid Sudoku

Problem link: https://leetcode.com/problems/valid-sudoku/

Solution: https://leetcode.com/problems/valid-sudoku/discuss/1414911