---
layout: default
title: Binary Tree Level Order Traversal II
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 7
permalink: /problem-57-Binary Tree Level Order Traversal II/
---
# Binary Tree Level Order Traversal II
Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root).

##### Example 1:
![](../../assets/images/ds/tree11212.jpeg)
```markdown
Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]
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
* -1000 <= Node.val <= 1000

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        LinkedList<List<Integer>> ans = new LinkedList<>();
        processLevelOderBotton(root,ans, 0);
        return ans;
    }

    public void processLevelOderBotton(TreeNode root, LinkedList<List<Integer>> ans, int level){
        if(root == null) return;
        
        if(level == ans.size()){
            ans.addFirst(new ArrayList<>());
        }
        ans.get(ans.size() - level - 1).add(root.val);
        processLevelOderBotton(root.left, ans, level + 1);
        processLevelOderBotton(root.right, ans, level + 1);
        
        
    }
}
```