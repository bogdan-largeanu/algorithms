
## Problem

link: https://leetcode.com/problems/design-add-and-search-words-data-structure/

```
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

    WordDictionary() Initializes the object.
    void addWord(word) Adds word to the data structure, it can be matched later.
    bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

 

Example:

Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]

Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True

 

Constraints:

    1 <= word.length <= 25
    word in addWord consists of lowercase English letters.
    word in search consist of '.' or lowercase English letters.
    There will be at most 3 dots in word for search queries.
    At most 104 calls will be made to addWord and search.
```

## Solution

Most of the complexity is in search. For normal words with "." We iterate over each children to find a match and return False if is not. If all children have been parse we check the bool word to confirm the path we navigate is a word or not. 

The more complex scenario is when "." shows up, in that case we  want to iterate and call recursivelly the function itself for a dept first search to validate if there's a valid word using any of the nodes from current position . Example "ab.c" will all call of "b" children until one is found that also has a child "c" with word=true.

```python

class TrieNode:
    def __init__(self):
#         the key will be a letter , up to all 26 and value a new TrieNode
        self.children = {}
#     We want to mark the end of a string of letters when is a specific word that has been added
        self.word = False
class WordDictionary:

    def __init__(self):
        self.node = TrieNode()
        

    def addWord(self, word: str) -> None:
        cur = self.node
        
        for char in word:
#        we add node if letter is not present in our trie
            if char not in cur.children:
                cur.children[char] = TrieNode()
#             iterate to next TrieNode till the end
            cur = cur.children[char]
#     After all letters were added we mark it as a word
        cur.word = True

    def search(self, word: str) -> bool:
        
        
        def dfs(j,node):
            for i in range(j,len(word)):
                if word[i] == ".":
                    
                    for childNode in node.children.values():
                        if dfs(i+1,childNode): 
                            return True
                    # else statement has a base case which this recurssion should eventually hit. So we want to bubble them up here too 
                    return False
                else:
                    if word[i] not in node.children.keys():
                        return False
                    node = node.children[word[i]]
            return node.word
        
        
        return dfs(0,self.node)


# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```