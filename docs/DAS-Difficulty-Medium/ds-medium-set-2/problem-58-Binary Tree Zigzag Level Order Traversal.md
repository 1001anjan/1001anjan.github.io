---
layout: default
title: Binary Tree Zigzag Level Order Traversal
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 8
permalink: /problem-58-Binary Tree Zigzag Level Order Traversal/
---
# Binary Tree Zigzag Level Order Traversal
Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

##### Example 1:
![](../../assets/images/ds/tree11212.jpeg)
```markdown
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
```
##### Example 2:
```markdown
Input: root = [1]
Output: [[1]]
```
##### Example 3:
```markdown
Input: root = []
Output: []
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 2000].
* -100 <= Node.val <= 100

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        processZigzagLevelOrder(root, ans, 0, true);
        return ans;
    }

    public void processZigzagLevelOrder(TreeNode root, List<List<Integer>> ans, int level, boolean isLeftToRight){
        if(root == null) return;
        if(level == ans.size()){
            ans.add(new ArrayList<>());
        }
        if(isLeftToRight){
            ans.get(level).add(root.val);
        }else{
            ans.get(level).add(0,root.val);
        }
        
        
        processZigzagLevelOrder(root.left, ans, level + 1, !isLeftToRight);
        processZigzagLevelOrder(root.right, ans, level + 1, !isLeftToRight);
    }
}
```