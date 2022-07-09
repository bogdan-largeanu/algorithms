Link: 
https://leetcode.com/problems/longest-substring-without-repeating-characters/submissions/



## Solution 

```py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
#         will use a technique similar to sliding window to keep track of substirngs, except we only use 1 pointer and use hmap to determine the left pointer when we hit a duplication
#        we start tracking one pointer R represending the right post pointer of the subarray  
        R = 0
        hmap = {}
        maxCount = 0
        while R <= len(s)-1:
            # we increase R by 1 every time and check if is in hashmap for duplicate.
# when we find a duplicate we update the maximum value if needed and We reset R to be from the index of duplicate value + 1
            if s[R] in hmap:    
                R = hmap[s[R]] + 1
                hmap = {}
#             We store every value and pointer in a hashmap
            hmap[s[R]] = R
            # we update maxCount if the substring in hmap is bigger the current maxCount
            maxCount = max(maxCount,len(hmap))
            R += 1
        return maxCount



```