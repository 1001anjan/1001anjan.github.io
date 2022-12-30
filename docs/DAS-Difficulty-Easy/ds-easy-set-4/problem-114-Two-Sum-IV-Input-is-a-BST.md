---
layout: default
title: Two Sum IV - Input is a BST
parent: Easy Set 4
grand_parent: DSA Easy Difficulty
nav_order: 14
permalink: /problem-114-Two-Sum-IV-Input-is-a-BST/
---
# Two Sum IV - Input is a BST
Given the root of a Binary Search Tree and a target number k, return true if there exist two elements in the BST such that their sum is equal to the given target.

##### Example 1:
![](../../assets/images/ds/sum_tree_1.jpeg)
```markdown
Input: root = [5,3,6,2,4,null,7], k = 9
Output: true
```
##### Example 2:
```markdown
Input: root = [5,3,6,2,4,null,7], k = 28
Output: false
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 104].
* -104 <= Node.val <= 104
* root is guaranteed to be a valid binary search tree.
* -105 <= k <= 105

##### Solution:
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
    public boolean findTarget(TreeNode root, int k) {
        Set<Integer> set = new HashSet<Integer>();
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.add(root);
       // set.add(root.val);
        while(!queue.isEmpty()){
            TreeNode node = queue.remove();
            if(set.contains(k - node.val)){
               return true; 
            } 
            set.add(node.val);
            if(node.left != null) queue.add(node.left);
            if(node.right != null) queue.add(node.right);
        }
        return false;
    }
}
```
