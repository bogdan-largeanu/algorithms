## Problem

link:

```md
There is an m x n rectangular island that borders both the Pacific Ocean and Atlantic Ocean. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an m x n integer matrix heights where heights[r][c] represents the height above sea level of the cell at coordinate (r, c).

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is less than or equal to the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return a 2D list of grid coordinates result where result[i] = [ri, ci] denotes that rain water can flow from cell (ri, ci) to both the Pacific and Atlantic oceans.

 

Example 1:

Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
Explanation: The following cells can flow to the Pacific and Atlantic oceans, as shown below:
[0,4]: [0,4] -> Pacific Ocean 
       [0,4] -> Atlantic Ocean
[1,3]: [1,3] -> [0,3] -> Pacific Ocean 
       [1,3] -> [1,4] -> Atlantic Ocean
[1,4]: [1,4] -> [1,3] -> [0,3] -> Pacific Ocean 
       [1,4] -> Atlantic Ocean
[2,2]: [2,2] -> [1,2] -> [0,2] -> Pacific Ocean 
       [2,2] -> [2,3] -> [2,4] -> Atlantic Ocean
[3,0]: [3,0] -> Pacific Ocean 
       [3,0] -> [4,0] -> Atlantic Ocean
[3,1]: [3,1] -> [3,0] -> Pacific Ocean 
       [3,1] -> [4,1] -> Atlantic Ocean
[4,0]: [4,0] -> Pacific Ocean 
       [4,0] -> Atlantic Ocean
Note that there are other possible paths for these cells to flow to the Pacific and Atlantic oceans.

Example 2:

Input: heights = [[1]]
Output: [[0,0]]
Explanation: The water can flow from the only cell to the Pacific and Atlantic oceans.

 

Constraints:

    m == heights.length
    n == heights[r].length
    1 <= m, n <= 200
    0 <= heights[r][c] <= 105


```


## Solution

TODO: Improve, don't store previous pointer there so that more data is cached.

The problem is done using DFS.  
Going over each point and doing DFS, will result in a lot of duplication. We could theoreticaly cache those but there is a simpler way  
We go from the edge, and do DFS marking all points the water reaches from pacific and atlantic   
Then we just check the intersection of atlantic and pacific sets  

```python


class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        pacific, atlantic = set(), set()
        
        rows,cols = len(heights), len(heights[0])
        
        def dfs(r,c,ocean,prevValue):
        # prevValue . needs to be lower or equal with current
            visited = deque()
            if (r,c) not in ocean:
                visited.append((r,c,prevValue))
            while len(visited) >0:
                curr = visited.popleft()
                r,c,prev = curr

                if curr not in ocean:
                    if heights[r][c] >= prev:
#                         a ocean point can have multiple DFS paths, we want to make sure we compare if the path can go up from the previous number. Don't want last value in DFS chain to stop us from exporing a new DFS, thus we save it in visited points
                        newValue = heights[r][c]
                        ocean.add(curr)
                        
        #               GO LEFT AND RIGHT       
                        for i in [-1,1]:
                            if c+i < cols and c+i>=0:
                                visited.append((r,c+i,newValue))

                        # GO BOTTOM and TOP
                        for i in [-1,1]:
                            if r+i < rows and r+i>=0:
                                visited.append((r+i,c,newValue))
                
                
            return ocean
                    
                

        
        for r in range(rows):
            # prevValue . needs to be lower or equal with current, so we current first time
#         LEFT EDGE
            pacific = dfs(r,0,pacific,heights[r][0])
#         RIGHT EDGE
            atlantic = dfs(r,cols-1,atlantic,heights[r][cols-1])
    
        for c in range(cols):
#           TOP EDGE
            pacific = dfs(0,c,pacific,heights[0][c])
#           BOTTOM EDGE
            atlantic =  dfs(rows-1,c,atlantic,heights[rows-1][c])
    

#        Because the sets also have the previus value in them, need to remove them before comparing the intersection of the 2 sets
        s1 = set()
        for a,b,c in atlantic:
            s1.add((a,b))
        s2 = set()
        for a,b,c in pacific:
            s2.add((a,b))
#     intersection is values common in both sets 
        return s1.intersection(s2)
        
        
        
```