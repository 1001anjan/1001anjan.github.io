---
layout: default
title: Minimum Absolute Difference in BST
parent: Easy Set 13
grand_parent: DSA Easy Difficulty
nav_order: 13
permalink: /problem-383-Minimum Absolute Difference in BST/
---
# Minimum Absolute Difference in BST
Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.

##### Example 1:
![](../../assets/images/ds/bst11.jpeg)
```markdown
Input: root = [4,2,6,1,3]
Output: 1
```
##### Example 2:
![](../../assets/images/ds/bst22.jpeg)
```markdown
Input: root = [1,0,48,null,null,12,49]
Output: 1
```
##### Constraints:
* The number of nodes in the tree is in the range [2, 104].
* 0 <= Node.val <= 10^5

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
    public int getMinimumDifference(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        inoderTraverse(root,list);
        int prev = list.get(1);
        int diff = prev - list.get(0);
        for(int i = 2; i < list.size(); i++){
            int curr = list.get(i);
            diff = Math.min(diff,curr - prev);
            prev = curr;
        }
        return diff;
    }
    
    public void inoderTraverse(TreeNode tree, List<Integer> list){
        if(tree == null) return;
        inoderTraverse(tree.left,list);
        list.add(tree.val);
        inoderTraverse(tree.right,list);
    }
}
```
##### Faster solution
```java
class Solution {
    /*
    As the tree is BST, we will do the inorder so that we will get a asceding order.
    We will just calculate the difference with adjaced nodes in the inorder.
    PS: Just consider the inorder of the tree as soreted array in ascending order and 
    you have to find the min diff of two elements.
    */
    int minDiff=Integer.MAX_VALUE,prev=-1;
    public int getMinimumDifference(TreeNode root) {
        inorder(root);
        return minDiff;
    }
    public void inorder(TreeNode root){
        if(root != null){
            inorder(root.left);
            if(prev != -1)
                minDiff = Math.min(Math.abs(root.val-prev),minDiff);
            prev=root.val;
            inorder(root.right);
        }
    }
}
```