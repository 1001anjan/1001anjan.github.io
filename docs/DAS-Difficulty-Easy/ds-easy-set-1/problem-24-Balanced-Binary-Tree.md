---
layout: default
title: Balanced Binary Tree
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 24
permalink: /problem-24-Balanced-Binary-Tree/
---
# Balanced Binary Tree
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

##### Example 1:

![](../../assets/images/ds/balance_1.jpeg)
```markdown
Input: root = [3,9,20,null,null,15,7]
Output: true
```
##### Example 2:
![](../../assets/images/ds/balance_2.jpeg)
```markdown
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```
##### Example 3:
```markdown
Input: root = []
Output: true
```

### Constraints:
* The number of nodes in the tree is in the range [0, 5000].
* -104 <= Node.val <= 104

### Solution
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
    private boolean isBalanced = true;
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        if(root.left == null && root.right == null) return true;
        getMaxDepth(root);
        return isBalanced;
    }
    public int getMaxDepth(TreeNode head){
        if(head == null) return 0;
        if(head.left == null && head.right == null) return 1;
        int left = getMaxDepth(head.left);
        int right = getMaxDepth(head.right);
        if(Math.abs(left - right) > 1){
           isBalanced = false; 
        }
        return 1+ Math.max(left,right);
        
    }
}
```