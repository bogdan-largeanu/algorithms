## Problem: Longest Substring Without Repeating Characters


Link: 
https://leetcode.com/problems/longest-substring-without-repeating-characters/

```
Given a string s, find the length of the longest substring without repeating characters.

 

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

 

Constraints:

    0 <= s.length <= 5 * 104
    s consists of English letters, digits, symbols and spaces.


```


## Solution 

```python

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left = 0
        counter = defaultdict(int)
        maxLength = 0
        for right in range(len(s)):
#          count every letter 
            counter[s[right]] +=1
#     Check and make sure is a valid string first
#             if there's repeated character we move left till there is none
            while counter[s[right]]>1:
                counter[s[left]] -=1
                left +=1
            maxLength = max(maxLength, right-left+1 )
            
        return maxLength
            

```