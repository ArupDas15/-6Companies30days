# 207. Course Schedule

Problem Link: https://leetcode.com/problems/course-schedule/description/


There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course a_i.

* For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return true if you can finish all courses. Otherwise, return false.

Example 1:
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.```

Example 2:
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.```
Input: rectangles = [[1,1,2,3],[1,3,2,4],[3,1,4,2],[3,2,4,4]]
Output: false
Explanation: Because there is a gap between the two rectangular regions.
```

### Constraints
```
* 1 <= numCourses <= 2000
* 0 <= prerequisites.length <= 5000
* prerequisites[i].length == 2
* 0 <= ai, bi < numCourses
* All the pairs prerequisites[i] are unique.
```

### Approach: 
Uses Topological sorting algorithm. If we can topologically sort all the courses then we can study all the courses.

Time Complexity: O(V+E) [Same as Kahn's Algo] 

Space Complexity: O(V)

### Solution
```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> adj[numCourses];
        vector<int> in(numCourses,0);
        for(int i=0;i<prerequisites.size();i++) adj[prerequisites[i][1]].push_back(prerequisites[i][0]);
        for(int i=0;i<numCourses;i++){
            for(auto j : adj[i]){
                in[j]++;    
            }
        }
        queue<int>q;
        for(int i=0;i<numCourses;i++){
            if(!in[i])q.push(i);
        }
        vector<int>topo;
        while(!q.empty()){
            int node = q.front();
            q.pop();
            topo.push_back(node);
            for(auto i:adj[node]){
              in[i]--;
              if(!in[i]) q.push(i);
            }
        }
        return topo.size()==numCourses;
    }
};
```


