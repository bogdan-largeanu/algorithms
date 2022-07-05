


# Problem

Link:  https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

```
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.

 

Example 1:

Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
Example 2:

Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].
Example 3:

Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].
 

Constraints:

2 <= numbers.length <= 3 * 104
-1000 <= numbers[i] <= 1000
numbers is sorted in non-decreasing order.
-1000 <= target <= 1000
The tests are generated such that there is exactly one solution.
```

# Solution

```py
class Solution:
#     since the array is organise we can take 2 points from and converge to middle
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        L,R = 0, len(numbers)-1
        
        print(numbers[1])
#         until we found result we move towards middle
        while L<R:
            # print(L,R)
            total = numbers[L] + numbers[R]
            print(L,R,total)
#             if we found 2 values that match, we return the result since the problem is explicit there is only one solution
            if total == target:
                return [L+1,R+1]
            
#             the hard part is figuring out when to move one pointer or the other. A logical argument to use is to say, since we know numbers are ordered, then taking a left R will give an equal or lower total sum, and taking a right L, will give equal or higher number. 
# Thus we can use the total comparisong agains target to guide where to take our pointers 
            if total >target:
                R -= 1
            else:
                L += 1
        return None
            
```