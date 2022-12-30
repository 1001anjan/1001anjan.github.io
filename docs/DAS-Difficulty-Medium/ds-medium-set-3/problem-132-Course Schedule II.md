---
layout: default
title: Course Schedule II
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 32
permalink: /problem-132-Course Schedule II/
---
# Course Schedule II
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

* For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

##### Example 1:
```markdown
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
```
##### Example 2:
```markdown
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```
##### Example 3:
```markdown
Input: numCourses = 1, prerequisites = []
Output: [0]
```
##### Constraints:
* 1 <= numCourses <= 2000
* 0 <= prerequisites.length <= numCourses * (numCourses - 1)
* prerequisites[i].length == 2
* 0 <= ai, bi < numCourses
* ai != bi
* All the pairs [ai, bi] are distinct.

### Solution:
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        LinkedList<Integer> list = new LinkedList<>();
        Set<Integer> added = new HashSet<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        for(int[] arr : prerequisites){
            map.computeIfAbsent(arr[0], value -> new ArrayList<>()).add(arr[1]);
        }
        for(int k = 0; k < numCourses; k++){
            if(dfs(k, map, list, new HashSet<>(), added)) return new int[0];
        }
        int[] ans = new int[list.size()];
        int i = 0;
        for(int n : list) ans[i++] = n;
        return ans;
    }

    public boolean dfs(int start, Map<Integer, List<Integer>> map, LinkedList<Integer> list, Set<Integer> visited, Set<Integer> added){
        if(visited.contains(start)) return true;
        if(!map.containsKey(start)){
            if(added.add(start)) list.add(start);
            return false;
        }
        visited.add(start);
        
        while(!map.get(start).isEmpty()){
            Integer node = map.get(start).iterator().next();
            if(dfs(node, map, list, visited, added)) return true;
            map.get(start).remove(node);
        }
        if(added.add(start)) list.add(start);
        map.remove(start);
        visited.remove(start);
        return false; 
    }
}
```