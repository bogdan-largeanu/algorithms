## Problem: Number of Islands

link: https://leetcode.com/problems/number-of-islands/

```
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

 

Example 1:

Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1

Example 2:

Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3

 

Constraints:

    m == grid.length
    n == grid[i].length
    1 <= m, n <= 300
    grid[i][j] is '0' or '1'.

Accepted
1,768,716
Submissions
3,202,439
```


## Solution

Iterate over every element of the matrix. if we find a "1" count as an island and perform a DFS(marking all elements found during this as 2).

```python
class Solution:
    def bfs(self,row,col,grid):
        def checkSides(row,col):
            bfs = []
#      top
            if row > 0:
                top = grid[row-1][col]
                if top == "1":
                    bfs.append([row-1,col])
                    grid[row-1][col] = 2
#       left
            if col> 0:
                left = grid[row][col-1]
                if left == "1":
                    bfs.append([row,col-1])
                    grid[row][col-1] = 2
#         right 
            if col < len(grid[row])-1:
                right = grid[row][col+1]
                if right == "1":
                    bfs.append([row,col+1])
                    grid[row][col+1] = 2
#         bottom 
            if row < len(grid)-1:
                bottom = grid[row+1][col]
                if bottom == "1":
                    bfs.append([row+1,col])
                    grid[row+1][col] = 2
            
            return bfs
        
        
        bfs = []
        bfs.append([row,col])
        grid[row][col] = 2 
        while len(bfs)>0:
            row,col = bfs.pop(0)
            sides = checkSides(row,col)
            bfs.extend(sides)
        return grid
    def numIslands(self, grid: List[List[str]]) -> int:
#         create a BFS. start from 0, and add adiacent points. Any pointed added, change number to 2 to mark is been visited already.
# for any new BFS started from 0 increase counter of islands

        counter = 0
        newGrid = grid
        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col] == "1":
                    counter += 1
                    newGrid = self.bfs(row,col,newGrid)
                                                        
        return counter
                    
```