# Problem Word Search II - Backtracking Trie
Link: https://leetcode.com/problems/word-search-ii/description/
Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

 

Example 1:

Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]

Example 2:

Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []


# Solution
Summary: 
DFS each box, compare using a trie and remove from trie the word once you found it once
```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.finishWord= False
    
    def addWord(self, word):
        curr = self

        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
        curr.finishWord = True

    def prune(self, word):
        curr = self
        stack = []
        
        for ch in word:
            stack.append(curr)
            curr = curr.children[ch]
        
        curr.is_word = False
        
        for t_node, ch in reversed(list(zip(stack, word))):
            if len(t_node.children[ch].children) > 0:  # has children
                return
            else:
                del t_node.children[ch]


class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        root = TrieNode()
        for w in words:
            root.addWord(w)
        
        ROWS,COLS = len(board) , len(board[0])
        result,visited = set(),set()

        def dfs(r,c,trieNode,word):
            # return if word  not out of boundary or already visited or not in list of children
            if (r<0 or c<0 or 
                r == ROWS or c == COLS or
                (r,c) in visited or
                board[r][c] not in trieNode.children):
                return

            # we add and remove current visited node
            visited.add((r,c))
            
            # navigate the trie to our character
            trieNode = trieNode.children[board[r][c]]
            
            # add char to our current word 
            word += board[r][c]
            if trieNode.finishWord:
                result.add(word)
                root.prune(word)
            
            # go the 4 direction
            dfs(r+1,c, trieNode,word)
            dfs(r,c+1, trieNode,word)
            dfs(r-1,c, trieNode,word)
            dfs(r,c-1, trieNode,word)

            visited.remove((r,c))
        
        for r in range(ROWS):
            for c in range(COLS):
                dfs(r,c,root,"")
        
        return list(result)
```