---
layout: default
title: House Robber III
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 23
permalink: /problem-123-House Robber III/
---
# House Robber III
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called root.

Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night.

Given the root of the binary tree, return the maximum amount of money the thief can rob without alerting the police.

##### Example 1:
![](../../assets/images/ds/rob1-tree.jpeg)
```markdown
Input: root = [3,2,3,null,3,null,1]
Output: 7
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```
##### Example 2:
![](../../assets/images/ds/rob2-tree.jpeg)
```markdown
Input: root = [3,4,5,1,3,null,1]
Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 10^4].
* 0 <= Node.val <= 10^4

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
    public int rob(TreeNode root) {
        int[] res = processRob(root);
        return Math.max(res[0], res[1]);
    }

// res[0] == include current node 
// res[1] = exculude current node
    public int[] processRob(TreeNode root){
        if(root == null) return new int[]{0, 0};        
        int[] left = processRob(root.left);
        int[] right = processRob(root.right);

        int includeCurrentNode = left[1] + right[1] + root.val;
        int excludeCurrentNode = Math.max(left[0], left[1]) + Math.max(right[0] , right[1]);
        return new int[]{includeCurrentNode,  excludeCurrentNode};
    }
}
```