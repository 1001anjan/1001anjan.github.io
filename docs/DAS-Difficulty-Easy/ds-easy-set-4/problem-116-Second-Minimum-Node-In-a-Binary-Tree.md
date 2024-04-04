---
layout: default
title: Second Minimum Node In a Binary Tree
parent: Easy Set 4
grand_parent: DSA Easy
nav_order: 16
permalink: /problem-116-Second-Minimum-Node-In-a-Binary-Tree/
---
# Second Minimum Node In a Binary Tree
Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly two or zero sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes. More formally, the property root.val = min(root.left.val, root.right.val) always holds.

Given such a binary tree, you need to output the second minimum value in the set made of all the nodes' value in the whole tree.

If no such second minimum value exists, output -1 instead.

##### Example 1:
![](../../assets/images/ds/smbt1.jpeg)
```markdown
Input: root = [2,2,5,null,null,5,7]
Output: 5
Explanation: The smallest value is 2, the second smallest value is 5.
```
##### Example 2:
```markdown
Input: root = [2,2,2]
Output: -1
Explanation: The smallest value is 2, but there isn't any second smallest value.
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 25].
* 1 <= Node.val <= 231 - 1
* root.val == min(root.left.val, root.right.val) for each internal node of the tree.

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
    public int findSecondMinimumValue(TreeNode root) {
        Long min1,min2;
        min1 = min2 = Long.MAX_VALUE;
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.add(root);
        while(!queue.isEmpty()){
            TreeNode node = queue.remove();
            if(min1>node.val && min2>node.val){
                min2 = min1;
                min1 =  Long.valueOf(node.val);
            }else if(min2>node.val && node.val != min1){
                min2 = Long.valueOf(node.val);
            }
            if(node.left != null) queue.add(node.left);
            if(node.right != null) queue.add(node.right);
        }
        System.out.println(min1+" "+min2);
        if(Long.MAX_VALUE == min2) return -1;
        return min2.intValue();
    }
}
```


