

Link: https://leetcode.com/problems/maximum-subarray/
```
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

 

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Example 2:

Input: nums = [1]
Output: 1
Example 3:

Input: nums = [5,4,-1,7,8]
Output: 23
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
``` 



Solution 

```py
#  In order to find the highest sub-array  we need to find when is not worth extending the array anymore
# in this case is when the total value is 0 or lower.
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
#       initialise the values with the first value. 
        current,highest = nums[0], nums[0]
# will start to iterate from 1 and always update the highest if needed. If value is less then 0 we reset        
        for v in nums[1:]:
            if current <= 0:
                current  = 0
            
            current += v
            highest = max(current, highest)
            
        
        return highest 
```