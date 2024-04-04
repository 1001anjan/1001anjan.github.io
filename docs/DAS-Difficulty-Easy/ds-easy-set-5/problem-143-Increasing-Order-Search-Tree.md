---
layout: default
title: Increasing Order Search Tree
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 13
permalink: /problem-143-Increasing-Order-Search-Tree/
---
# Increasing Order Search Tree

Given the root of a binary search tree, rearrange the tree in in-order so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only one right child.

##### Example 1:
![](../../assets/images/ds/ex1.jpeg)
```markdown
Input: root = [5,3,6,2,4,null,8,1,null,null,null,7,9]
Output: [1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]
```
##### Example 2:
![](../../assets/images/ds/ex2.jpeg)
```markdown
Input: root = [5,1,7]
Output: [1,null,5,null,7]
```
##### Constraints:
* The number of nodes in the given tree will be in the range [1, 100].
* 0 <= Node.val <= 1000

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
    TreeNode t = new TreeNode();
    TreeNode next;
    public TreeNode increasingBST(TreeNode root) {
        if(root == null) return null;
        next = t;
        inOrderTraversal(root);
        return t.right;
    }
    
    public void inOrderTraversal(TreeNode head){
        if(head == null) return;
        inOrderTraversal(head.left);
        next.right = head;
        next = head;
        next.left = null;
        inOrderTraversal(head.right);
       
    }
}
```