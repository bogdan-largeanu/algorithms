# Problem 
link: https://leetcode.com/problems/valid-sudoku/description/

```
Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.
Note:

A Sudoku board (partially filled) could be valid but is not necessarily solvable.
Only the filled cells need to be validated according to the mentioned rules.
```

# Solution
Summary: We go over the entire sudoku and save them in a set for colums and rows. 
We got 3 requirements to check
1. no sets on rows has duplicates
2. no sets in colums has duplicates
3. no set in boxes has duplicates

The only "tricky" part is figuring out we can map the 9 sudoku boxes  by doing math floor to 3. This results in squareRow 0-2 = 0 ; 3-5 = 1 etc...


```python

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = collections.defaultdict(set)
        colms = collections.defaultdict(set)
        squareBox = collections.defaultdict(set)

        # Going over all rows and adding them to a set
        for i in range(len(board)):
            for j in range(len(board[0])):
                if(board[i][j] in rows[i] or
                   board[i][j] in colms[j] or 
                   board[i][j] in squareBox[(i//3,j//3)] # we flow the numbers so that values 0-8 get map to 0-2 (3 boxes on each row&column)
                   ):
                    return False
                if(board[i][j]== '.'): 
                    continue
                rows[i].add(board[i][j])
                colms[j].add(board[i][j])
                
                squareBox[(i //3,j//3)].add(board[i][j]) # we flow the numbers so that values 0-8 get map to 0-2 (3 boxes on each row&column)
        return True
```