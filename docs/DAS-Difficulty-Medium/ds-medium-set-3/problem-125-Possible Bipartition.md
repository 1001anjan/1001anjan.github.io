---
layout: default
title: Possible Bipartition
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 25
permalink: /problem-125-Possible Bipartition/
---
# Possible Bipartition
We want to split a group of n people (labeled from 1 to n) into two groups of any size. Each person may dislike some other people, and they should not go into the same group.

Given the integer n and the array dislikes where dislikes[i] = [ai, bi] indicates that the person labeled ai does not like the person labeled bi, return true if it is possible to split everyone into two groups in this way.

##### Example 1:
```markdown
Input: n = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4] and group2 [2,3].
```
##### Example 2:
```markdown
Input: n = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false
```
##### Example 3:
```markdown
Input: n = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false
```
##### Constraints:
* 1 <= n <= 2000
* 0 <= dislikes.length <= 10^4
* dislikes[i].length == 2
* 1 <= dislikes[i][j] <= n
* ai < bi
* All the pairs of dislikes are unique.

### Solution:
```java
class Solution {
    public boolean possibleBipartition(int n, int[][] dislikes) {
        Map<Integer, List<Integer>> adj = new HashMap<>();
        // creating adjacency list 
        for(int[] arr : dislikes){
            adj.computeIfAbsent(arr[0], value -> new ArrayList<>()).add(arr[1]);
            adj.computeIfAbsent(arr[1], value -> new ArrayList<>()).add(arr[0]);
        }

        // initilizing all nodes color as -1 (-1 -> not colored, 0 -> RED, 1-> Green)
        int[] color = new int[n + 1]; 
        Arrays.fill(color, -1);
        for(int i = 1; i <= n; i++){
            if(color[i] == -1 && !bsfCheck(i, adj, color)) return false;
        }
        return true;

    }

    public boolean bsfCheck(int source, Map<Integer, List<Integer>> adj, int[] color){
        // making staring node as RED color
        color[source] = 0;
        Queue<Integer> q = new LinkedList<>();
        q.offer(source);

        while(!q.isEmpty()){
            int node = q.poll();
            // traversing all adjacent node
            if(!adj.containsKey(node)) continue;
            for(int n : adj.get(node)){
                if(color[node] == color[n]) return false;
                // if not processed the node for the coloring
                if(color[n] == -1){
                    color[n] = 1 - color[node];
                    q.add(n);
                }
            }
        }

        return true;
    }
}
```