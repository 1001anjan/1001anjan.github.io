---
layout: default
title: Minimum Height Trees
parent: Data Structure Medium Set 3
grand_parent: Data Structure
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