---
layout: default
title: Kth Smallest Element in a BST
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 4
permalink: /problem-104-Kth Smallest Element in a BST/
---
# Kth Smallest Element in a BST
Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.

##### Example 1:
![](../../assets/images/ds/kthtree1.jpeg)
```markdown
Input: root = [3,1,4,null,2], k = 1
Output: 1
```
##### Example 2:
![](../../assets/images/ds/kthtree2.jpeg)
```markdown
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```
##### Constraints:
* The number of nodes in the tree is n.
* 1 <= k <= n <= 104
* 0 <= Node.val <= 104


* Follow up: If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?

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
    public int kthSmallest(TreeNode root, int k) {
        List<Integer> list = new LinkedList<>();
        inoderTraverse(root, list);
        return list.get(k - 1);
    }

    public void inoderTraverse(TreeNode root, List<Integer> list){
        if(root == null) return;
        inoderTraverse(root.left, list);
        list.add(root.val);
        inoderTraverse(root.right, list);
    }
}
```