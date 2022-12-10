---
layout: default
title: Univalued Binary Tree
parent: Data Structure Easy Set 5
grand_parent: Data Structure
nav_order: 24
permalink: /problem-154-Univalued-Binary-Tree/
---
# Univalued Binary Tree
A binary tree is uni-valued if every node in the tree has the same value.

Given the root of a binary tree, return true if the given tree is uni-valued, or false otherwise.

##### Example 1:
![](../../assets/images/ds/unival_bst_1.png)

```markdown
Input: root = [1,1,1,1,1,null,1]
Output: true
```
##### Example 2:
![](../../assets/images/ds/unival_bst_2.png)

```markdown
Input: root = [2,2,2,5,2]
Output: false
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 100].
* 0 <= Node.val < 100

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
    public boolean isUnivalTree(TreeNode root) {
       Stack<TreeNode> stack = new Stack();
        stack.push(root);
        int val = root.val;
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            if(val != node.val) return false;
            if(node.left != null) stack.push(node.left);
            if(node.right != null) stack.push(node.right);
        }
        return true;
    }
}
```