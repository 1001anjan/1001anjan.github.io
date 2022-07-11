---
layout: default
title: Merge Two Binary Trees
parent: Data Structure Easy Set 4
grand_parent: Data Structure
nav_order: 9
permalink: /problem-109-Merge-Two-Binary-Trees/
---
# Merge Two Binary Trees

You are given two binary trees root1 and root2.

Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

Return the merged tree.

Note: The merging process must start from the root nodes of both trees.

##### Example 1:
![](../../assets/images/ds/merge.jpeg)
```markdown
Input: root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
Output: [3,4,5,5,4,null,7]
```
##### Example 2:
```markdown
Input: root1 = [1], root2 = [1,2]
Output: [2,2]
```
##### Constraints:
* The number of nodes in both trees is in the range [0, 2000].
* -104 <= Node.val <= 104

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
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1 == null) return root2;
        if(root2 == null) return root1;
        root1.val = root1.val + root2.val;
        root1.left = mergeTrees(root1.left,root2.left);
        root1.right = mergeTrees(root1.right,root2.right);
        return root1;
    }
}
```
#### Non-recursive
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
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1 == null) return root2;
        if(root2 == null) return root1;
        Stack<TreeNode> s1 = new Stack<TreeNode>();
        Stack<TreeNode> s2 = new Stack<TreeNode>();
        TreeNode h1, h2;
        h1 = root1;
        h2 = root2;
        s1.push(h1);
        s2.push(h2);
        while(!s1.isEmpty() && !s2.isEmpty()){
            h1 = s1.pop();
            h2 = s2.pop();
            h1.val = h1.val + h2.val;
            if(h1.left != null && h2.left != null){
                s1.push(h1.left);
                s2.push(h2.left);
            }
            if(h1.right !=null && h2.right != null){
                s1.push(h1.right);
                s2.push(h2.right);
            }
            
            if(h1.left == null && h2.left != null){
                h1.left = h2.left;
                h2.left = null;
            }
            if(h1.right == null && h2.right != null){
                h1.right = h2.right;
                h2.right = null;
            }
        }
        return root1;
    }
}
```


