---
layout: default
title: Diameter of Binary Tree
parent: Easy Set 3
grand_parent: DSA Easy Difficulty
nav_order: 35
permalink: /problem-98-Diameter-of-Binary-Tree/
---
# Diameter of Binary Tree

Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.

##### Example 1:
![](../../assets/images/ds/diamtree.jpeg)
```markdown
Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].
```
##### Example 2:
```markdown
Input: root = [1,2]
Output: 1
```
##### Constraints:

* The number of nodes in the tree is in the range [1, 104].
* -100 <= Node.val <= 100

### Solution:
```java
class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        // here we are using diameter array as reference to store value and not a diameter int variable to store the value
        int[] diameter = new int[1];
        helper(root,diameter);
        
        return diameter[0];
    }
    
    public int helper(TreeNode root, int[] diameter){
        
        if(root == null) return 0;
        
        int leftHeight = helper(root.left,diameter);
        int rightHeight = helper(root.right,diameter);
        
        // checking whether the previous diameter is max  or new diameter is max
        diameter[0] = Math.max(diameter[0],leftHeight + rightHeight);
        
        // here returning the max height which can either be left one or right one by adding current node as well 
        return 1 +  Math.max(leftHeight , rightHeight);
        
        
    }
}
```

