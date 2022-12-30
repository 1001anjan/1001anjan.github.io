---
layout: default
title: Minimum Depth of Binary Tree
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 25
permalink: /problem-25-Minimum-Depth-of-Binary-Tree/
---
# Minimum Depth of Binary Tree
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

##### Example 1:
![](../../assets/images/ds/ex_depth.jpeg)
```markdown
Input: root = [3,9,20,null,null,15,7]
Output: 2
```
##### Example 2:
```markdown
Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5
```

### Constraints:

* The number of nodes in the tree is in the range [0, 105].
* -1000 <= Node.val <= 1000

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
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        if(root.left == null && root.right == null) return 1;
        int left = Integer.MAX_VALUE;
        int right = Integer.MAX_VALUE;
        if(root.left != null) {
            left = minDepth(root.left);
        }
        if(root.right != null){
            right = minDepth(root.right);
        }
        return 1 + Math.min(left,right );
    }
}
```
### Non-recursive
```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        int depth = 1;
        while (true){
            int level = queue.size();
            for (int i = 0; i < level; i++){
                TreeNode data = queue.poll();
                if (data.left == null && data.right == null) return depth;
                if (data.left != null) queue.offer(data.left);
                if (data.right != null) queue.offer(data.right);
            }
            depth++;
        }
    }
}
```

