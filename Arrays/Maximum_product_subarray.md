link: https://leetcode.com/problems/maximum-product-subarray/
```
Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

A subarray is a contiguous subsequence of the array.

 

Example 1:

Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
Example 2:

Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
 

Constraints:

1 <= nums.length <= 2 * 104
-10 <= nums[i] <= 10
The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
```

```py
# Solution: 
# 2 deal with negative numbers will iterate over the array and keey track of 2 more # products. a low one will deal with high negative values that might turn positive at some point, and high one is for always positive numbers scenario
# we keep track of current number, lower_bound and upper_bound. 
# iterating over the array we always calculate them, we reset only at 0
# lower_bound will be the min of (current, lower_bound*current, higher_bound*current)
# upper_bound will be the max of (current, lower_bound*current, higher_bound*current)

class Solution:
    def maxProduct(self, nums: List[int]) -> int:
#     we initialised all of them on first value since the code is replacing them if lower or upper numbers exist.
# Not using -math.inf on fattest or high because we don't do anything when arr has only one element 
        fattest, low,high = nums[0],nums[0],nums[0]
        print(-math.inf < -2)
        for curr in nums[1:]:
            print(curr, low, high, fattest)

            if curr == 0:
                low = 0
                high = 0
                
#           if we just calculate min and max dirrectly the new value of min will affect max and multiple twice : example curr*min will be curr*(currn*min)
            tmp_min = min(curr, curr*low, curr*high)
            high = max(curr, curr*low, high*curr)
            low = tmp_min
           # because even a high can be ruined later on by a negative number, we always want to save our highest value yet
             
            if max(high,low,curr)> fattest:
                fattest = max(low,high,curr)
        
        return fattest
```