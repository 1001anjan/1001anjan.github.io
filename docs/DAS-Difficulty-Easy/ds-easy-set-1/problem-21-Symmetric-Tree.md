---
layout: default
title: Symmetric Tree
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 21
permalink: /problem-21-Symmetric-Tree/
---
# Symmetric Tree
Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

##### Example 1:
![](../../assets/images/ds/symtree1.jpeg)
```markdown
Input: root = [1,2,2,3,4,4,3]
Output: true
```

##### Example 2:
![](../../assets/images/ds/symtree2.jpeg)
```markdown
Input: root = [1,2,2,null,3,null,3]
Output: false
```

### Constraints:
* The number of nodes in the tree is in the range [1, 1000].
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
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        return checkMiror(root.left, root.right);
    }
    public boolean checkMiror(TreeNode t1, TreeNode t2){
        if(t1 == null || t2 == null) return t1 == t2;

        if(t1.val == t2.val) 
            return checkMiror(t1.left, t2.right) && checkMiror(t1.right, t2.left);
        
        return false;
    }
}
```

