---
layout: default
title: Leaf-Similar Trees
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 9
permalink: /problem-139-Leaf-Similar-Trees/
---
# Leaf-Similar Trees

Consider all the leaves of a binary tree, from left to right order, the values of those leaves form a leaf value sequence.

For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similar if their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.


![](../../assets/images/ds/leaf-similar-1.jpeg)
##### Example 1:
```markdown
Input: root1 = [3,5,1,6,2,9,8,null,null,7,4], root2 = [3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
Output: true
```
![](../../assets/images/ds/leaf-similar-2.jpeg)
##### Example 2:
```markdown
Input: root1 = [1,2,3], root2 = [1,3,2]
Output: false
```
##### Constraints:
* The number of nodes in each tree will be in the range [1, 200].
* Both of the given trees will have values in the range [0, 200].

### Solution:
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        List<Integer> l1 = new ArrayList<>();
        List<Integer> l2 = new ArrayList<>();
        dfs(root1,l1);
        dfs(root2,l2);
        return l1.equals(l2);
    }
    
    public void dfs(TreeNode head, List<Integer> l){
        if(head == null) return;
        if(head.left == null && head.right == null) l.add(head.val);
        dfs(head.left,l);
        dfs(head.right,l);
    }
}
```