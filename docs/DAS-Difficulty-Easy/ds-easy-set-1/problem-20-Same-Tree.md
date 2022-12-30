---
layout: default
title: Same Tree
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 20
permalink: /problem-20-Same-Tree/
---
# Same Tree

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

##### Example 1:
```markdown
Input: p = [1,2,3], q = [1,2,3]
Output: true
```


#### Example 2
```markdown
Input: p = [1,2], q = [1,null,2]
Output: false
```


#### Example 3:
```markdown
Input: p = [1,2,1], q = [1,1,2]
Output: false
```
### Constraints:
* The number of nodes in both trees is in the range [0, 100].
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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null) return true;
        if(p != null && q == null) return false;
        if(p == null && q != null) return false;
        if(p.val != q.val) return false;
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```