##Problem 
424. Longest Repeating Character Replacement

link: https://leetcode.com/problems/longest-repeating-character-replacement/

```
You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

 

Example 1:

Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.

Example 2:

Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.

 

Constraints:

    1 <= s.length <= 105
    s consists of only uppercase English letters.
    0 <= k <= s.length


```


## Solution

To calculate longest repeating character replacement we calculate length of the window - most popular characters <= K
Example:
"AABCDA" k = 2

Window is AABC = 4   
Most counted character = 2  
4 -2 <= k(2) : TRUE | This is true. So length of window is the highest length atm. We reach this state expanding from window "A" all the way to here, as the condition was always true

But If we extend the window right now, the statement will become false   

Window is AABCD
5 - 2("AA") <= k (2): FALSE | We need to move left pointer 
Window is ABCD
4 - 1("A") <= k(2): False | Move Left pointer until condition is true again. Only then we can expand right pointer more

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
# Sliding windows, move left pointer when window length - mostCounted character >= k
        counter = defaultdict(int)
        left = 0
        maxLength = 0
        
        for right in range(len(s)):
            counter[s[right]] +=1
#             while the length - couter is bigger then k, we move left the pointer
            while (right-left - max(counter.values()) )>=k:
                counter[s[left]] -= 1
                left += 1
            
            maxLength = max(maxLength, right-left+1)
            
        return maxLength
            
            
        


```