## Problems 
link: https://leetcode.com/problems/top-k-frequent-elements/

```MD
Medium

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.


Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:

Input: nums = [1], k = 1
Output: [1]

Constraints:

    1 <= nums.length <= 105
    -104 <= nums[i] <= 104
    k is in the range [1, the number of unique elements in the array].
    It is guaranteed that the answer is unique.

 

Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
```

## Solutions

- Will use a hashmap to count the number for each element  
- Then will use Bucket Sort, with the key indicated how many elements and value the element itself. Bucket sort will be between 0 and length of the array (given a element can't count more then array length)  
- Result We return back the last K element from end to start  

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
#       Generate the length of the arr. Avoid using []* len(nums) because that creates a pointer to the same array for each index. So a change on index 1 applies to all index at the same time
        topK = [ [] for i in range(len(nums)+1)]
        hMap = defaultdict(int)
#         count the values for each element
        for elem in nums:
            hMap[elem] += 1
#       map the counts to a sorted bucket using the value as index
        print('hmap',hMap)
        for key in hMap.keys():
            topK[hMap[key]].append(key)
        
        
#        Iterate over the sort bucket from end. For each value added decrese K
#        Once K is 0 return right away
        result = []
        for i in range(len(topK)-1,0,-1):
            for elem in topK[i]:
                result.append(elem)
                k -= 1
                if k == 0:
                    return result
                
        return result
        
        
            
```
