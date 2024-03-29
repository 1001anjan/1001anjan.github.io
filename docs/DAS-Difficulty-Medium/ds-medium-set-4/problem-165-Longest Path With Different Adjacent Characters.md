---
layout: default
title: Longest Path With Different Adjacent Characters
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 15
permalink: /problem-165-Longest Path With Different Adjacent Characters/
---
# Longest Path With Different Adjacent Characters
You are given a tree (i.e. a connected, undirected graph that has no cycles) rooted at node 0 consisting of n nodes numbered from 0 to n - 1. The tree is represented by a 0-indexed array parent of size n, where parent[i] is the parent of node i. Since node 0 is the root, parent[0] == -1.

You are also given a string s of length n, where s[i] is the character assigned to node i.

Return the length of the longest path in the tree such that no pair of adjacent nodes on the path have the same character assigned to them.

##### Example 1:
```markdown
![](../../assets/images/ds/160_example_1_1.png)
Input: parent = [-1,0,0,1,1,2], s = "abacbe"
Output: 3
Explanation: The longest path where each two adjacent nodes have different characters in the tree is the path: 0 -> 1 -> 3. The length of this path is 3, so 3 is returned.
It can be proven that there is no longer path that satisfies the conditions.
```
##### Example 2:
```markdown
![](../../assets/images/ds/160_example_1_1.png)
Input: parent = [-1,0,0,0], s = "aabc"
Output: 3
Explanation: The longest path where each two adjacent nodes have different characters is the path: 2 -> 0 -> 3. The length of this path is 3, so 3 is returned.
```
##### Constraints:
* n == parent.length == s.length
* 1 <= n <= 10^5
* 0 <= parent[i] <= n - 1 for all i >= 1
* parent[0] == -1
* parent represents a valid tree.
* s consists of only lowercase English letters.

### Solution:
```java
class Solution {
    int longestPath = 1;
    public int longestPath(int[] parent, String s) {
        Map<Integer, List<Integer>> adj = new HashMap<>();
        for(int i = 1; i < parent.length; i++){
            adj.computeIfAbsent(parent[i], value -> new ArrayList<>()).add(i);
        }

        dfsComputeLongestPath(0, adj, s.toCharArray());
        return longestPath;
    }

    private int dfsComputeLongestPath(int node, Map<Integer, List<Integer>> childs, char[] s){
        // If the node is the only child, return 1 for the currentNode itself.
        if(!childs.containsKey(node)) return 1;
        int longestChain = 0, secondLongestChain = 0;
        for(int child : childs.get(node)){
            int longestChainStartingFromChild = dfsComputeLongestPath(child, childs, s);

            if(s[child] == s[node]) continue;

            if(longestChainStartingFromChild > longestChain){
                secondLongestChain = longestChain;
                longestChain = longestChainStartingFromChild;
            }else if(longestChainStartingFromChild > secondLongestChain){
                secondLongestChain = longestChainStartingFromChild;
            }
        }

        // Add "1" for the node itself.
        longestPath = Math.max(longestPath, longestChain + secondLongestChain + 1);
        return longestChain + 1;
    }
}
```