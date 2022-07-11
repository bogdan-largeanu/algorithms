
## Problem 
Link:
https://leetcode.com/problems/valid-anagram/submissions/

```
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:

Input: s = "anagram", t = "nagaram"
Output: true
Example 2:

Input: s = "rat", t = "car"
Output: false
 

Constraints:

1 <= s.length, t.length <= 5 * 104
s and t consist of lowercase English letters.
 

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?
```

## Solution

```py
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
#         generate hashmap with each characterc counted
        hmap = Counter(s)
        
#         iterate over second word 
        for char in t:
#         if we find the char is missing from hmap or is value is less then 0, then we know is an extra character compare to first world and return false right away
            if hmap.get(char) == None or hmap.get(char) <=0 :
                return False
#         we reduce the count by 1 for each character found, expecting all charac to have reach eventually value 0 for an anagram
            hmap[char] -= 1
        
#      we check if the hmap has any extra characters left, if we find any it means second word was missing characters that first world had so we return false right away
        for char in hmap:
            if hmap.get(char) != 0:
                return False
        
        return True 
```