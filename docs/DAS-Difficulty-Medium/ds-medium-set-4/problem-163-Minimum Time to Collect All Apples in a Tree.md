---
layout: default
title: Minimum Time to Collect All Apples in a Tree
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 13
permalink: /problem-163-Minimum Time to Collect All Apples in a Tree/
---
# Minimum Time to Collect All Apples in a Tree
Given an undirected tree consisting of n vertices numbered from 0 to n-1, which has some apples in their vertices. You spend 1 second to walk over one edge of the tree. Return the minimum time in seconds you have to spend to collect all apples in the tree, starting at vertex 0 and coming back to this vertex.

The edges of the undirected tree are given in the array edges, where edges[i] = [ai, bi] means that exists an edge connecting the vertices ai and bi. Additionally, there is a boolean array hasApple, where hasApple[i] = true means that vertex i has an apple; otherwise, it does not have any apple.

##### Example 1:
![](../../assets/images/ds/min_time_collect_apple_1.png)
```markdown
Input: n = 7, edges = [[0,1],[0,2],[1,4],[1,5],[2,3],[2,6]], hasApple = [false,false,true,false,true,true,false]
Output: 8
Explanation: The figure above represents the given tree where red vertices have an apple. One optimal path to collect all apples is shown by the green arrows.
```
##### Example 2:
![](../../assets/images/ds/min_time_collect_apple_2.png)
```markdown
Input: n = 7, edges = [[0,1],[0,2],[1,4],[1,5],[2,3],[2,6]], hasApple = [false,false,true,false,false,true,false]
Output: 6
Explanation: The figure above represents the given tree where red vertices have an apple. One optimal path to collect all apples is shown by the green arrows.
```
##### Example 3:
```markdown
Input: n = 7, edges = [[0,1],[0,2],[1,4],[1,5],[2,3],[2,6]], hasApple = [false,false,false,false,false,false,false]
Output: 0
```
##### Constraints:
* 1 <= n <= 10^5
* edges.length == n - 1
* edges[i].length == 2
* 0 <= ai < bi <= n - 1
* from_i < to_i
* hasApple.length == n

### Solution:
```java
class Solution {
    public int minTime(int n, int[][] edges, List<Boolean> hasApple) {
        Map<Integer, List<Integer>> adj = new HashMap<>();
        // create adjacency map
        for(int[] arr : edges){
            adj.computeIfAbsent(arr[0], data -> new ArrayList<>()).add(arr[1]);
            adj.computeIfAbsent(arr[1], data -> new ArrayList<>()).add(arr[0]);
        }

        return dfsComputeMinTime(0, -1, adj, hasApple);
    }

    private int dfsComputeMinTime(int node, int parent, Map<Integer, List<Integer>> map, List<Boolean> hasApple){
        if(!map.containsKey(node)) return 0;

        int totalCost = 0, childCost = 0;
        for(int child : map.get(node)){
            if(child == parent) continue;
            childCost = dfsComputeMinTime(child, node, map, hasApple);

            if(childCost > 0 || hasApple.get(child)){
                totalCost += childCost + 2;
            }
        }
        return totalCost;
    }
}
```