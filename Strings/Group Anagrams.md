## Problem

Link: https://leetcode.com/problems/group-anagrams/

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

Accepted
1,450,310
Submissions
2,235,402
```


## Solution 
```py
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
# we will create a group array that consists of hashmaps anagrams to validate if and where an anagram should go
        groups = []
#     will create a "shaddow" wordGroups array, that will have the same index as groups for subarrays of words matching an anagram. Will store here all the results matching
        wordGroups = []
        
#         Maping every word to a hashmap . using this over Counter because it has better performance to allow passing the tests
        
        def mapWordToHashMap(word):
            hmap = {}
            for v in word:
                if hmap.get(v) == None:
                    hmap[v] = 1
                else:
                    hmap[v] += 1
            return hmap
        
# iterate over every word in the string array 
        for word in strs:
            added = False
            hmap = mapWordToHashMap(word)

            # after we added some anagrams to groups, we check current one to see if it matches an existent anagram. The group only has 1 anagram for each position, for list of word is only maintained in wordGroups         
            for i in range(0,len(groups)):
                if hmap == groups[i]:
#                     if is already one example in group, don't need a dict for every word
                    # groups[i].append(hmap)
                    wordGroups[i].append(word)
                    added = True
#        on words that don't have an anagram already in groups we add them here
            if added == False:
                groups.append(hmap)
                wordGroups.append([word])
                
        
        return wordGroups
                    
                    
            
            
        

```