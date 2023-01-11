## Problem 

```md
Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.


Example 1:

Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:

Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9

 

Constraints:

    0 <= nums.length <= 105
    -109 <= nums[i] <= 109


```


## Solution
Summary: Convert the code to a set. Iterate over each number and look if there's anything smaller. When nothing is smaller iterate to the right and count the total length

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        # convert to set 
        # iterate over each
        # check left side, if is null then look to the right with a while loop and count

        numset = set(nums)
        longest = 0

        for n in nums:
            if (n-1) not in numset:
                currLength = 0
                while (n+currLength) in numset:
                    currLength +=1
                longest = max(currLength,longest)
        
        return longest
```