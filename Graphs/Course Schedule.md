## Problem 

link: https://leetcode.com/problems/course-schedule/

```md
207. Course Schedule
Medium

11346

439

Add to List

Share
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

 

Example 1:

Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
Example 2:

Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
 

Constraints:

1 <= numCourses <= 2000
0 <= prerequisites.length <= 5000
prerequisites[i].length == 2
0 <= ai, bi < numCourses
All the pairs prerequisites[i] are unique.
```

## Solution

Summary: The gist of it is we represent the course dependency as a graph, and then perform a DFS to find if we visited a node twice. If we do it means we have 2 overlapping requirements, if we finish DFS the course then all is good.

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        preqreq = { c: [] for c in range(numCourses)}
        for course,prerequisites in prerequisites:
            preqreq[course].append( prerequisites)
            
        print(prerequisites)
#       3 States
#       visited = means we added to the result at the end of the DFS.
#       visiting/cycle = means we are currently parsing but not added yet to the list of visited
#       unvisited vertex not visited yet 
        
        output = []
        
        visited, cycle  = set(), set()
        
        def dfs(vertex):
            if vertex in cycle:
                return False
            if vertex in visited:
                return True
            
            cycle.add(vertex)
            
            for prerequisites in preqreq[vertex]:
#                this goes through all prerequisites and does DFS.
#                can return the false from above so want to bubble that up
                if dfs(prerequisites) == False:
                    return False
#             At this point we parse all course vertex using DFS so we can reset the cycle
            cycle.remove(vertex)
#     After all the checks above we can not safely added to visited 
            visited.add(vertex)
            output.append(vertex)
#         Covering the basecase to mark the DFS as finishing without finding a cycle
            return True
         
#     Now we do DFS on all course vertexes
        for c in range(numCourses):
#         if dfs is false, it means we have a cycle and return the expect empty list
            if dfs(c) == False:
                return []
        
        return output
             
```

