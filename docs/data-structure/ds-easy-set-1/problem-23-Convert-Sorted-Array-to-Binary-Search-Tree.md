---
layout: default
title: Convert Sorted Array to Binary Search Tree
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 23
permalink: /problem-23-Convert-Sorted-Array-to-Binary-Search-Tree/
---
# Convert Sorted Array to Binary Search Tree

Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

##### Example 1:

![](../../assets/images/ds/btree1.jpeg)
```markdown
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:
```
![](../../assets/images/ds/btree2.jpeg)

##### Example 2:
![](../../assets/images/ds/btree.jpeg)

````markdown
Input: nums = [1,3]
Output: [3,1]
Explanation: [1,null,3] and [3,1] are both height-balanced BSTs.

````
### Constraints:
* 1 <= nums.length <= 104
* -104 <= nums[i] <= 104
* nums is sorted in a strictly increasing order.

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
    public TreeNode sortedArrayToBST(int[] nums) {
        return convertBalancedTree(null, nums, 0, nums.length-1);
    }
    
    public TreeNode convertBalancedTree(TreeNode head, int[] nums, int s, int e){
        if(s>e) return head;
        int mid = (s+e)/2;
        head = new TreeNode(nums[mid]);
        
        head.left = convertBalancedTree(head.left, nums, s, mid-1);
        head.right = convertBalancedTree(head.right, nums, mid+1, e);
        return head;
    }
}
```