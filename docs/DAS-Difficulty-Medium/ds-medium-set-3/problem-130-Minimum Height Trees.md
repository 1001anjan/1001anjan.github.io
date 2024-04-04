---
layout: default
title: Minimum Height Trees
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 30
permalink: /problem-130-Minimum Height Trees/
---
# Minimum Height Trees
A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of n nodes labelled from 0 to n - 1, and an array of n - 1 edges where edges[i] = [ai, bi] indicates that there is an undirected edge between the two nodes ai and bi in the tree, you can choose any node of the tree as the root. When you select a node x as the root, the result tree has height h. Among all possible rooted trees, those with minimum height (i.e. min(h))  are called minimum height trees (MHTs).

Return a list of all MHTs' root labels. You can return the answer in any order.

The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

##### Example 1:
![](../../assets/images/ds/e111.jpeg)
```markdown
Input: n = 4, edges = [[1,0],[1,2],[1,3]]
Output: [1]
Explanation: As shown, the height of the tree is 1 when the root is the node with label 1 which is the only MHT.
```
##### Example 2:
![](../../assets/images/ds/e2222.jpeg)
```markdown
Input: n = 6, edges = [[3,0],[3,1],[3,2],[3,4],[5,4]]
Output: [3,4]
```
##### Constraints:
* 1 <= n <= 2 * 10^4
* edges.length == n - 1
* 0 <= ai, bi < n
* ai != bi
* All the pairs (ai, bi) are distinct.
* The given input is guaranteed to be a tree and there will be no repeated edges.

### Solution:
##### Time Limit Exceeded

```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        // base case
        Map<Integer, List<Integer>> adj = new HashMap<>();
        List<Integer[]> nodeHeight = new ArrayList<>();
        List<Integer> ans = new ArrayList<>();

        if(n == 0) return ans;
        if(n == 1){
            ans.add(0);
            return ans;
        } 

        for(int[] arr : edges){
            adj.computeIfAbsent(arr[0], value -> new ArrayList<>()).add(arr[1]);
            adj.computeIfAbsent(arr[1], value -> new ArrayList<>()).add(arr[0]);
        }

        for(int i = 0; i < n; i++){
            Queue<Integer> q = new LinkedList<>();
            Set<Integer> seen = new HashSet<>();
            q.offer(i);
            seen.add(i);
            int height = 0;

            while(!q.isEmpty()){
                int size = q.size();
                Queue<Integer> q1 = new LinkedList<>();
                while(size > 0){
                    List<Integer> list = adj.get(q.poll());
                    for(int in : list){
                        if(seen.contains(in)) continue;
                        q1.offer(in);
                        seen.add(in);
                    }
                    size --;
                }
                height ++;
                q = q1;
            }
            nodeHeight.add(new Integer[]{i, height});
        }

        int min = Collections.min(nodeHeight, (a, b) -> (a[1].compareTo(b[1])))[1];

        for(Integer[] inr : nodeHeight){
            if(inr[1] == min) ans.add(inr[0]);
        }
        return ans;
    }
}
```
#### removing leaves -- finding centroid 
```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        Set<Integer>[] adj = new HashSet[n];

        // initializing adjacency list for all the nodes
        for(int i = 0; i < n; i++){
            adj[i] = new HashSet<>();
        }

        // setting adges for the nodes
        for(int[] arr : edges){
            adj[arr[0]].add(arr[1]);
            adj[arr[1]].add(arr[0]);
        }

        List<Integer> leaves = new ArrayList<>();
        Set<Integer> process = new HashSet<>();

        int n1 = n;
        while(n > 2 ){
            leaves.clear();
            // calculate leaves node
            for(int i = 0; i < adj.length; i++){
                if(adj[i].size() == 1){
                    leaves.add(i);
                }
            }
            // detach leave node
            for(Integer l : leaves){
                adj[new ArrayList<>(adj[l]).get(0)].remove(l);
                adj[l].clear();
            }
            n -= leaves.size();
            process.addAll(leaves);
        }
        List<Integer> ans = new ArrayList<>();
        for(int i = 0; i < n1; i++){
            if(!process.contains(i)) ans.add(i);
        } 
        return ans;
    }
}
```
##### Improvement
```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {

        // edge cases
        if (n < 2) {
            ArrayList<Integer> centroids = new ArrayList<>();
            for (int i = 0; i < n; i++)
                centroids.add(i);
            return centroids;
        }

        // Build the graph with the adjacency list
        ArrayList<Set<Integer>> neighbors = new ArrayList<>();
        for (int i = 0; i < n; i++)
            neighbors.add(new HashSet<Integer>());

        for (int[] edge : edges) {
            Integer start = edge[0], end = edge[1];
            neighbors.get(start).add(end);
            neighbors.get(end).add(start);
        }

        // Initialize the first layer of leaves
        ArrayList<Integer> leaves = new ArrayList<>();
        for (int i = 0; i < n; i++)
            if (neighbors.get(i).size() == 1)
                leaves.add(i);

        // Trim the leaves until reaching the centroids
        int remainingNodes = n;
        while (remainingNodes > 2) {
            remainingNodes -= leaves.size();
            ArrayList<Integer> newLeaves = new ArrayList<>();

            // remove the current leaves along with the edges
            for (Integer leaf : leaves) {
                // the only neighbor left for the leaf node
                Integer neighbor = neighbors.get(leaf).iterator().next();
                // remove the edge along with the leaf node
                neighbors.get(neighbor).remove(leaf);
                if (neighbors.get(neighbor).size() == 1)
                    newLeaves.add(neighbor);
            }

            // prepare for the next round
            leaves = newLeaves;
        }

        // The remaining nodes are the centroids of the graph
        return leaves;
    }
}
```