---
layout: default
title: Binary Tree Inorder Traversal
parent: Easy Set 1
grand_parent: DSA Easy
nav_order: 19
permalink: /problem-19-Binary-Tree-Inorder-Traversal/
---
# Binary Tree Inorder Traversal

Given the root of a binary tree, return the inorder traversal of its nodes' values.

#### Example 1:
```markdown
Input: root = [1,null,2,3]
Output: [1,3,2]
```

#### Example 2:
```markdown
Input: root = []
Output: []
```

### Example 3:
```markdown
Input: root = [1]
Output: [1]
```
### Constraints:

* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

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
    List<Integer> val = new ArrayList();
    public List<Integer> inorderTraversal(TreeNode root) {
        if(root == null) return new ArrayList<Integer>();
        inorderTraversal(root.left);
        val.add(root.val);
        inorderTraversal(root.right);
        return val;
        
    }
}
```
