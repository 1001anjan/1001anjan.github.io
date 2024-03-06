---
layout: default
title: Recover Binary Search Tree
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 6
permalink: /problem-56-Recover Binary Search Tree/
---
# Recover Binary Search Tree
You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.

##### Example 1:
![](../../assets/images/ds/recover1.jpeg)

```markdown
Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.
```
##### Example 2:
![](../../assets/images/ds/recover2.jpeg)

```markdown
Input: root = [3,1,4,null,null,2]
Output: [2,1,4,null,null,3]
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.
```
##### Constraints:
* The number of nodes in the tree is in the range [2, 1000].
* -2^31 <= Node.val <= 2^31 - 1


Follow up: A solution using O(n) space is pretty straight-forward. Could you devise a constant O(1) space solution?

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
    public void recoverTree(TreeNode root) {
        while(!processRecoverTree(root, Long.MIN_VALUE, Long.MAX_VALUE, null, null));
    }
    public boolean processRecoverTree(TreeNode root, long min, long max, TreeNode minNode, TreeNode maxNode){
        if(root == null) return true;
        if(root.val > max){
            int t = root.val;
            root.val = maxNode.val;
            maxNode.val = t;
            return false;
        }
        if(root.val < min){
            int t = root.val;
            root.val = minNode.val;
            minNode.val = t;
            return false;
        }
        return processRecoverTree(root.left, min, root.val, minNode, root) &
        processRecoverTree(root.right, root.val, max, root, maxNode);
    }
}
```