---
layout: default
title: Cousins in Binary Tree
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 28
permalink: /problem-158-Cousins-in-Binary-Tree/
---
# Cousins in Binary Tree

Given the root of a binary tree with unique values and the values of two different nodes of the tree x and y, return true if the nodes corresponding to the values x and y in the tree are cousins, or false otherwise.

Two nodes of a binary tree are cousins if they have the same depth with different parents.

Note that in a binary tree, the root node is at the depth 0, and children of each depth k node are at the depth k + 1.

##### Example 1:
![](../../assets/images/ds/q1248-01.png)
```markdown
Input: root = [1,2,3,4], x = 4, y = 3
Output: false
```
##### Example 2:
![](../../assets/images/ds/q1248-02.png)
```markdown
Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
```
##### Example 3:
![](../../assets/images/ds/q1248-03.png)
```markdown
Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false
```
##### Constraints:
* The number of nodes in the tree is in the range [2, 100].
* 1 <= Node.val <= 100
* Each node has a unique value.
* x != y
* x and y are exist in the tree.

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
    public boolean isCousins(TreeNode root, int x, int y) {
        if(root == null || root.val == x || root.val == y) return false;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            int size = q.size();
            int x1 = -1;
            int y1 = -1;
            TreeNode p1, p2;
            p1 = p2 = null;
            Queue<TreeNode> q1 = new LinkedList<>();
            for(int i = 1; i<=size; i++){
                TreeNode t = q.poll();
                if(t.left != null && t.left.val == x){
                    x1= x;
                    p1 = t;
                }else if(t.left != null && t.left.val == y){
                    y1= y;
                    p2 = t;
                } 
                if(t.right != null && t.right.val == x){
                    x1 = x;
                    p1 = t;
                } else if(t.right != null && t.right.val == y){
                    y1 = y;
                    p2 = t;
                } 
                if(x1 == x && y1== y && p1 != p2) return true;
                if(t.left != null) q1.add(t.left);
                if(t.right != null) q1.add(t.right);
            }
            q = q1;
        }
        return false;
    }
}
```
