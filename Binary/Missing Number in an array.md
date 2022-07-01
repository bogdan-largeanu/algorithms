
# Problem
link: https://leetcode.com/problems/missing-number/

```
Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.


Example 1:

Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
Example 2:

Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
Example 3:

Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
 

Constraints:

n == nums.length
1 <= n <= 104
0 <= nums[i] <= n
All the numbers of nums are unique.
 

Follow up: Could you implement a solution using only O(1) extra space complexity and O(n) runtime complexity?
```

# Solution
```py

class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        result = 0
#         Xor any number with itself will be 0
#  since the array is 0 to n, and we know only one number is missing
# we iterate over the array and use the index to xor every value

        for index,value in enumerate(nums):
            print(index,value)
            xor = index ^ value
            result ^= xor
#  given we are missing one number, we add an extra XOR agains what the last element in array would have been if the number was missing. This means now every number present has been xor to 0, and we are left with the missing number           
        result ^= len(nums)
            
        return result

```
# Explanation
```
Explanation 

symbol ^ means  bit operation XOR
numbers are consecutive from 0 to N. 

Any positive number Xor with itself is 0
Example:
A ^ A = 0
101 ^ 101 = 000

Also XOR is associative and commutative i.e( a^(b^c) = (a^b)^c , a^b = b^c) respectively;

Thus if we have an array with one number from 0 to n missing
e.g.
0,2,3.
 and we multiple each with the index + one extra index at the end to cover the missing element
0,1,2, 3
 then it will be the only number left as everything else becomes 0
If we take the indexes times the values in array
0,1,2,3 
XOR
0,2,3.
=> we get in binary the following 
(00 ^ 00) ^ (10 ^ 10) ^ (11 ^10 ) ^ 01 =
0 ^ 0 ^ 0 ^ 1 =
1

```