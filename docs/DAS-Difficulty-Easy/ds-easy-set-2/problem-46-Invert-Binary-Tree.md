---
layout: default
title: Invert Binary Tree
parent: Easy Set 2
grand_parent: DSA Easy
nav_order: 15
permalink: /problem-46-Invert-Binary-Tree/
---
# Invert Binary Tree
Given the root of a binary tree, invert the tree, and return its root.

##### Example 1:
![](../../assets/images/ds/invert1-tree.jpeg)
```markdown
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```
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
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return root;
        TreeNode ptr;
        ptr = root.left;
        root.left = root.right;
        root.right = ptr;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```

