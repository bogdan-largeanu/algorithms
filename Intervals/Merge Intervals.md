# Problem

link: https://leetcode.com/problems/merge-intervals/

```
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

 

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

Example 2:

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.

 

Constraints:

    1 <= intervals.length <= 104
    intervals[i].length == 2
    0 <= starti <= endi <= 104

Accepted
1,580,368
Submissions
3,472,509
```

## Solution

```python

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
# we can see if intervals are continues is pretty easy to merge adiacent intervals
        #     problem dose not state if intervals are in increase order    
#     So we will sort by first key, since that's the key we will compare a current interval to determine if it get's merge or not 
#  pick a interval, and iterate through the rest of intervals until their first key is  bigger then our last key

        intervals.sort(key= lambda x: x[0])
        
# add first pair to result 
        results = [intervals[0]]
        for start,end in intervals[1:]:
            lastEnd = results[-1][1]
#             if first pointer is always smaller or equal since we sorted.
# if start is equal or smaller then our lastEnd, we save the higher values between lastEnd and (newInterval) End
            if start <= lastEnd :
                results[-1][1] = max( end, lastEnd)
            else:
              results.append([start,end])
            
        return results
            

```