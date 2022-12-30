---
layout: default
title: Minimum Distance Between BST Nodes
parent: Easy Set 13
grand_parent: DSA Easy Difficulty
nav_order: 24
permalink: /problem-394-Minimum Distance Between BST Nodes/
---
# Minimum Distance Between BST Nodes
Given the root of a Binary Search Tree (BST), return the minimum difference between the values of any two different nodes in the tree.

##### Example 1:
![](../../assets/images/ds/bst1.jpeg)
```markdown
Input: root = [4,2,6,1,3]
Output: 1
```
##### Example 2:
![](../../assets/images/ds/bst2.jpeg)
```markdown
Input: root = [1,0,48,null,null,12,49]
Output: 1
```
##### Constraints:
* The number of nodes in the tree is in the range [2, 100].
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
    public int minDiffInBST(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        list = inorderTravaerse(root, list);
        int prev = list.get(1);
        int diff = prev - list.get(0);
        for(int i = 2; i < list.size(); i++){
            int curr = list.get(i);
            diff = Math.min(diff, curr - prev);
            prev = curr;
        }
        return diff;
    }
    
    public List<Integer> inorderTravaerse(TreeNode root, List<Integer> list){
        if(root == null) return list;
        list = inorderTravaerse(root.left, list);
        list.add(root.val);
        list = inorderTravaerse(root.right, list);
        return list;
    }
}
```
