---
layout: default
title: Validate Binary Search Tree
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 4
permalink: /problem-54-Validate Binary Search Tree/
---
# Validate Binary Search Tree
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

* The left subtree of a node contains only nodes with keys less than the node's key.
* The right subtree of a node contains only nodes with keys greater than the node's key.
* Both the left and right subtrees must also be binary search trees.

##### Example 1:
![](../../assets/images/ds/tree1111.jpeg)

```markdown
Input: root = [2,1,3]
Output: true
```
##### Example 2:
![](../../assets/images/ds/tree2222.jpeg)

```markdown
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 104].
* -2^31 <= Node.val <= 2^31 - 1

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
    public boolean isValidBST(TreeNode root) {
       return checkIsValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean checkIsValidBST(TreeNode root, long minVal, long maxVal){
        if(root == null) return true;
        if(root.val >= maxVal || root.val <= minVal) return false;
        return checkIsValidBST(root.left, minVal, root.val) & checkIsValidBST(root.right, root.val, maxVal);
    }
}
```