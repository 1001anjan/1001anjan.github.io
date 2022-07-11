---
layout: default
title: Search in a Binary Search Tree
parent: Data Structure Easy Set 4
grand_parent: Data Structure
nav_order: 20
permalink: /problem-120-Search-in-a-Binary-Search-Tree/
---
# Search in a Binary Search Tree

You are given the root of a binary search tree (BST) and an integer val.

Find the node in the BST that the node's value equals val and return the subtree rooted with that node. If such a node does not exist, return null.

##### Example 1:
```markdown
Input: root = [4,2,7,1,3], val = 2
Output: [2,1,3]
```
##### Example 2:
```markdown
Input: root = [4,2,7,1,3], val = 5
Output: []
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 5000].
* 1 <= Node.val <= 107
* root is a binary search tree.
* 1 <= val <= 107

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
    public TreeNode searchBST(TreeNode root, int val) {
        if(root == null) return null;
        if(root.val == val) return root;
        if(root.val>val)
            return searchBST(root.left, val);
        else
            return searchBST(root.right, val);
    }
}
```
