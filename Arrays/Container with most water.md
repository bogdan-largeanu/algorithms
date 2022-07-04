
Link: https://leetcode.com/problems/container-with-most-water/

# Solution
```py
class Solution:
    def maxArea(self, height: List[int]) -> int:
#         Summary:
#         we move L and R pointer closer to center
#           check the volume (distance time min height ), update container volume 
#           we can't know all potential value that will come but we can reason that 
#         1. because the volume is distance * shorter height[value]
#           2. distance will always go down 
#           volume is always dependent on the min height, 
#           we don't know what will be in futures moves 
#           so we optimise my keeping the long height, and always moving the pointer for the small one, in case we find later a value with a very high hight, then we already keept a high value for the other pointer to maximise it.
        def calVol(L,R):
            if L>=R:
                return -1
            if R==0:
                return -1
            return (R-L)*min(height[L],height[R])
        
        L,R = 0, len(height)-1
        mostWater = 0
#         we iterate until we move the pointers in the middle
        while L<R:
#         we calculate the current volume and update if is higher then our known max
            mostWater = max(mostWater,calVol(L,R))
#  we move by 1 the pointer with smaller height value
            if height[L]<= height[R]:
                L +=1
            else:
                R -=1
        return mostWater
            
        
        
```