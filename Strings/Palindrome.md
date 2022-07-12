# Problem 

link: https://leetcode.com/problems/valid-palindrome/

```
125. Valid Palindrome
Easy

4135

5534

Add to List

Share
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

 

Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
Example 3:

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

## Solutions


```py
class Solution:
    def isPalindrome(self, s: str) -> bool:
#         two pointer left and right, going towards center. lowercase each string and compare. If a pointer find an empty space, it moves again until it find a letter. They move of by +1 and -1 
        if len(s) == 1:
            return True
        L,R = 0, len(s)-1
        
#     we move the pointers from outside towards middle 
        while L<R:
#         we check if the pointers is at a alphabetic or numer, if not we move by 1 
            if s[L].isalnum() == False:
                L += 1
                continue
            if s[R].isalnum() == False:
                R -= 1
                continue
#         check if letters match when lowercase, if they don't is not palindrome
            if L<R and s[L].lower() != s[R].lower():
                return False
#        move L and R by 1
            L +=1 
            R -= 1
        
        
        return True


```