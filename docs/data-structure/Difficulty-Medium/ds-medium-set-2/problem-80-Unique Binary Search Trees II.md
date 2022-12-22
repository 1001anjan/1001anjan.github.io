---
layout: default
title: Unique Binary Search Trees II
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 30
permalink: /problem-80-Unique Binary Search Trees II/
---
# Unique Binary Search Trees II
Given an integer n, return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.

##### Example 1:
![](../../assets/images/ds/uniquebstn3.jpeg)

```markdown
Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```
##### Example 2:
```markdown
Input: n = 1
Output: [[1]]
```
##### Constraints:
* 1 <= n <= 8

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
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode>[] dp = new ArrayList[n + 1];
        // base case
        dp[0] = new ArrayList<>();
        dp[0].add(null);
        dp[1] = new ArrayList<>();
        dp[1].add(new TreeNode(1));

        // process dp for target number
        for(int i = 2; i <= n; i++){
            dp[i] = new ArrayList<>();
            for(int j = 1; j <= i; j++){
                for(TreeNode leftNode : dp[j - 1]){
                    for(TreeNode rightNode : dp[i - j]){
                        TreeNode newNode = new TreeNode(j);
                        newNode.left = leftNode;
                        newNode.right = clone(rightNode, j);
                        dp[i].add(newNode);
                    }
                }
            }
        }
      return dp[n];
    }


    static TreeNode clone(TreeNode node, int offset){
        if(node == null) return null;
        TreeNode newNode = new TreeNode(node.val + offset);
        newNode.left = clone(node.left, offset);
        newNode.right = clone(node.right, offset);
        return newNode;
    }
}
```