## Problem
link: https://leetcode.com/problems/non-overlapping-intervals/

```md

Given an array of intervals intervals where intervals[i] = [starti, endi], return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

 

Example 1:

Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.

Example 2:

Input: intervals = [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to make the rest of the intervals non-overlapping.

Example 3:

Input: intervals = [[1,2],[2,3]]
Output: 0
Explanation: You don't need to remove any of the intervals since they're already non-overlapping.

 

Constraints:

    1 <= intervals.length <= 105
    intervals[i].length == 2
    -5 * 104 <= starti < endi <= 5 * 104

Accepted
294,784
Submissions
596,224
```

## Solution


```python

class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
#         sort the intervals by first pointer
#         compare the end of a pointer with the head of the next. if is equal or more we continue to next pointer 
#         if not we drop the period with a higher ending value 

        intervals.sort(key=lambda x: x[0])
        lastStart, lastEnd = intervals[0]
        skipCount = 0
        for i in range(1,len(intervals)):
            currStart, currEnd = intervals[i]
        
#             if is not overlapping we continue our iteration and mark the current one for next comparison
            if lastEnd <= currStart:
                lastStart, lastEnd = intervals[i]
                continue
#            else there's overlap, we compare to known which pointer we hold. We eliminate the one extending more (meaning with a higher END) as that minimisez the number of periods we need to eliminate to avoid overlaping 
            else:
                skipCount +=1
                if  lastEnd < currEnd:
                    continue
                else:
                    lastEnd = currEnd
                    
        
        return skipCount
                
```