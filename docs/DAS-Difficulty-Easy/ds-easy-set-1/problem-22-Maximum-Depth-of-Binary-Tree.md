---
layout: default
title: Maximum Depth of Binary Tree
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 22
permalink: /problem-22-Maximum-Depth-of-Binary-Tree/
---
# Maximum Depth of Binary Tree

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.



##### Example 1:
![](../../assets/images/ds/tmp-tree.jpeg)

```markdown
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

##### Example 2:
```markdown
Input: root = [1,null,2]
Output: 2
```

##### Constraints:
* The number of nodes in the tree is in the range [0, 104].
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
    public int maxDepth(TreeNode root) {
        if(root == null ) return 0;
        if(root.left == null && root.right == null) return 1;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

