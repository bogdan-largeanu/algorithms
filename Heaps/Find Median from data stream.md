## Problem
link: https://leetcode.com/problems/find-median-from-data-stream/

```md
Hard

8370

152

Add to List

Share
The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

For example, for arr = [2,3,4], the median is 3.
For example, for arr = [2,3], the median is (2 + 3) / 2 = 2.5.
Implement the MedianFinder class:

MedianFinder() initializes the MedianFinder object.
void addNum(int num) adds the integer num from the data stream to the data structure.
double findMedian() returns the median of all elements so far. Answers within 10-5 of the actual answer will be accepted.
 

Example 1:

Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]

Explanation
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
 

Constraints:

-105 <= num <= 105
There will be at least one element in the data structure before calling findMedian.
At most 5 * 104 calls will be made to addNum and findMedian.
 

Follow up:

If all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?
If 99% of all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?
Accepted
533,120
Submissions
1,044,237
```


## Solution

Summary: We create two heaps. Imagine a left and right heap containing the values ordered. 
Left is a maxHeap, so we can extract max value easy
Right is a minHeap to extract smallest value easy.
When we insert we make sure the heaps are even (equal length +1 )
and we make sure left elements are smaller then right heap elements

For Mean we just take the top element from left and right (min and max heaps)

```python

class MedianFinder:

    def __init__(self):
        
#       two heaps, large (with a minheap) and small (with a maxHeap)
#       heaps should be equal size

        self.small,self.large = [],[]
    

    def addNum(self, num: int) -> None:


#       because python only has min Heaps, will use -1 to have this acting as a maxHeap
        heapq.heappush(self.small, -1 * num)
        
#       1. make sure every num in small is <= every num in large
        if(self.small and self.large):
            maxValueFromSmall = -1* self.small[0] 
            minValueFromLarge = self.large[0]
#             if small has bigger element , we move it to large
            if (maxValueFromSmall > minValueFromLarge):
                popedMaxValueFromSmall = -1 * heapq.heappop(self.small)
                heapq.heappush(self.large,popedMaxValueFromSmall)
#     2. Make heaps be even size
        if len(self.small) > len(self.large) +1:
            maxValueFromSmall = -1 * heapq.heappop(self.small)
            heapq.heappush(self.large,maxValueFromSmall)
        
        if len(self.large) > len(self.small):
            minValueFromLarge = heapq.heappop(self.large)
            heapq.heappush(self.small,-1 * minValueFromLarge)

    def findMedian(self) -> float:
#         if small or large is bigger by 1, we return that 1
        if len(self.small) > len(self.large):
            return -1 * self.small[0]
        if len(self.large) > len(self.small):
            return self.large[0]
        # otherwise we return the avg of the small max-value and large min-value

        return ((-1 * self.small[0]) + self.large[0])/2
        


        


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```