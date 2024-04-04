---
layout: default
title: Path Sum III
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 16
permalink: /problem-166-Path Sum III/
---
# Path Sum III
Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the values along the path equals targetSum.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

##### Example 1:
![](../../assets/images/ds/pathsum3-1-tree.jpeg)
```markdown
Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
Output: 3
Explanation: The paths that sum to 8 are shown.
```
##### Example 2:
```markdown
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: 3
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 1000].
* -10^9 <= Node.val <= 10^9
* -1000 <= targetSum <= 1000

### Solution:
##### Complexity:
* Space: O(n) due to recursion.
* Time: O(n^2)
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
    public int pathSum(TreeNode root, int targetSum) {
        if(root == null) return 0;
        return dfsSum(root, targetSum) + pathSum(root.left, targetSum) + pathSum(root.right, targetSum);
    }

    private int dfsSum(TreeNode node, long sum){
        if(node == null) return 0;
        return (node.val == sum ? 1 : 0) + dfsSum(node.left, sum - node.val) + dfsSum(node.right, sum - node.val);
    }
}
```
```java
class Solution {
    int count;
    
    public int pathSum(TreeNode root, int targetSum) {
        count= 0;
        
        List<Integer> l1= new ArrayList<>();
        preorder(root, targetSum, 0, l1);
        
        return count;
    }
    
    public void preorder(TreeNode root, int targetSum, long temp, List<Integer> l1){
        if(root == null){
            return;
        }
        
        // temp+= root.val;
        l1.add(root.val);
        
        preorder(root.left, targetSum, temp, l1);
        preorder(root.right, targetSum, temp, l1);

        for(int i= l1.size()-1; i>=0; i--){
            temp+= l1.get(i);
            
            if(temp == targetSum){
                count++;
            }
        }
        
        //  Backtracking (restoring the previous condition)
        l1.remove(l1.size()-1);
    }
}
```
