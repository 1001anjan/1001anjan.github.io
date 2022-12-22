---
layout: default
title: Path Sum II
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 10
permalink: /problem-60-Path Sum II/
---
# Path Sum II
Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.

A root-to-leaf path is a path starting from the root and ending at any leaf node. A leaf is a node with no children.

##### Example 1:
![](../../assets/images/ds/pathsumii1.jpeg)

```markdown
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
Explanation: There are two paths whose sum equals targetSum:
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22
```
##### Example 2:
![](../../assets/images/ds/pathsum2222.jpeg)

```markdown
Input: root = [1,2,3], targetSum = 5
Output: []
```
##### Example 3:
```markdown
Input: root = [1,2], targetSum = 0
Output: []
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 5000].
* -1000 <= Node.val <= 1000
* -1000 <= targetSum <= 1000

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
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> ans = new ArrayList<>();
        processPathSum(root, ans, 0, targetSum, new ArrayList<>());
        return ans;
    }

    public void processPathSum(TreeNode root, List<List<Integer>> ans, int sum, int target, List<Integer> list){
        if(root == null) return;
        sum += root.val;
        list.add(root.val);
        if(root.left == null && root.right == null && sum == target){
            ans.add(list);
            return;
        }
        
        processPathSum(root.left, ans, sum, target, new ArrayList<>(list));
        processPathSum(root.right, ans, sum, target, new ArrayList<>(list));

    }
}
```
##### Optimise memory allocation 
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
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> ans = new ArrayList<>();
        processPathSum(root, ans, 0, targetSum, new ArrayList<>());
        return ans;
    }

    public void processPathSum(TreeNode root, List<List<Integer>> ans, int sum, int target, List<Integer> list){
        if(root == null) return;
        sum += root.val;
        if(root.left == null && root.right == null && sum == target){
            List<Integer> l = new ArrayList<>(list);
            l.add(root.val);
            ans.add(new ArrayList<>(l));
            return;
        }
        list.add(root.val);

        processPathSum(root.left, ans, sum, target, list);
        processPathSum(root.right, ans, sum, target, list);
        list.remove(list.size() - 1);
    }
}
```