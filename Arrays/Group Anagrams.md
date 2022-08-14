## Problem

```
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Example 2:

Input: strs = [""]
Output: [[""]]

Example 3:

Input: strs = ["a"]
Output: [["a"]]

 

Constraints:

    1 <= strs.length <= 104
    0 <= strs[i].length <= 100
    strs[i] consists of lowercase English letters.


```



## Solution
```python
class Solution:

    
#    we map the word an array using index for each letter value
# we return back a tuple to be used as key(since they are hashable. We could also generate a string but the hashing could cause conflict which did happen when I tried  `signatureString+= str(arr[i])+str(i)` adding an `a` fixed it but that's just luck until tests include a value non hashable correctly  )
    def generateArrayASCI(self,word):
        arr = [0]*26
        for char in word:
            arr[ord(char) -ord('a')] += 1
 
        return tuple(arr)
        
    
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        #     this is where we keep all anagrams. The key is the count of words as tuples. as that's uniq to anagram
        signatureHmap = {}
        
    
        for word in strs:
#             signature is a tuple generate by the anagram values. => so is the same for any anagram 
            signature = self.generateArrayASCI(word)
            
            if signatureHmap.get(signature):
                signatureHmap.get(signature).append(word)
            else:
                signatureHmap[signature] = [word]

        
        return signatureHmap.values()
        
```

Complexity 

    Time complexity: O(N * S). 
    N for parsing every word.  
    S average length of a string(as we parse each to convert it to an array)
    M - parsing the arr S to convert to touple. since we know this is a constant 26, we can drop it 

    Space Complexity: ( N * A)
    A = the number of anagram generated <= number of words
    N = maximum number of words generated for each anagram
    There's also the 26 arr, but is a constant so we drop it 
