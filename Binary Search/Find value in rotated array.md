
## Problem
link: https://leetcode.com/problems/search-in-rotated-sorted-array/

```
There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1

Example 3:

Input: nums = [1], target = 0
Output: -1

 

Constraints:

    1 <= nums.length <= 5000
    -104 <= nums[i] <= 104
    All values of nums are unique.
    nums is an ascending array that is possibly rotated.
    -104 <= target <= 104

Accepted
1,654,093
Submissions
4,314,264
```


## Solution

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        def binarySearch(left,right):
            mid = (left+right)//2
            valueL = nums[left]
            valueR = nums[right]
            valueM = nums[mid]
            print(valueL,valueM,valueR)
            if valueL == target:
                return left
            if valueR == target:
                return right
            if valueM == target:
                return mid
            
            if (right-left)<2:
                return -1
            
#        need to draw on a paper and write down every rule for going left or right. 
            if valueL<valueM:
#         if target is not between mid and left, then is on the right side
                if target > valueM or target< valueL:
                    return binarySearch(mid+1,right)
                else:
                    return binarySearch(left,mid-1)
#                 if right is bigger then mid value
            else:
#         if target is not betwen mid and right then is on the left side 
                if target < valueM or target>valueR:
                    return binarySearch(left,mid-1)
                else:
                    return binarySearch(mid+1,right)
            
        return binarySearch(0,len(nums)-1)
```

Complexity:

    Time complexity:
    O(Log N) - because we just do a binary search
    
    Space complexity : 
    If converted to use a while loop it will be O(1)
    With recursion it will be O(log N)

