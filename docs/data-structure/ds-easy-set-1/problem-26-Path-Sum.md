---
layout: default
title: Path Sum
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 26
permalink: /problem-26-Path-Sum/
---
# Path Sum
Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.

A leaf is a node with no children.

##### Example 1:
![](../../assets/images/ds/pathsum1.jpeg)
```markdown
Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
Output: true
Explanation: The root-to-leaf path with the target sum is shown.
```
##### Example 2:
![](../../assets/images/ds/pathsum2.jpeg)
```markdown
Input: root = [1,2,3], targetSum = 5
Output: false
Explanation: There two root-to-leaf paths in the tree:
(1 --> 2): The sum is 3.
(1 --> 3): The sum is 4.
There is no root-to-leaf path with sum = 5.
```
##### Example 3:
```markdown
Input: root = [], targetSum = 0
Output: false
Explanation: Since the tree is empty, there are no root-to-leaf paths.
```

### Constraints:
* The number of nodes in the tree is in the range [0, 5000].
* -1000 <= Node.val <= 1000
* -1000 <= targetSum <= 1000

### Solution
#### Non-Recursive 
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
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root == null) return false;
        Stack<TreeNode> stack = new Stack<TreeNode>();
        Map<TreeNode, Relation> map = new HashMap<TreeNode, Relation>();
        stack.push(root);
        map.put(root, new Relation(null, root.val));
        TreeNode ptr;
        int sum = 0;
        Relation rl;
        while(!stack.isEmpty()){
            ptr = stack.pop();
            rl = map.get(ptr);
            if(rl.parent != null){
              sum =  map.get(rl.parent).sumVal + ptr.val;
            }else{
                sum = ptr.val;
            }
            if(ptr.left == null && ptr.right == null && sum == targetSum) return true;
            if(ptr.right != null) {
                stack.push(ptr.right);
                 map.put(ptr.right,new Relation(ptr, sum+ptr.right.val));
            }
            if(ptr.left != null) {
                stack.push(ptr.left);
                map.put(ptr.left,new Relation(ptr, sum+ptr.left.val));
            }
        }
        return false;
    }
}

class Relation{
    public TreeNode parent;
    public int sumVal;
    public Relation(TreeNode node, int val){
        parent = node;
        sumVal = val;
    }
}
```

#### Recursive
```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false; 
        
        return solve(root, targetSum);
    }
    
    public boolean solve(TreeNode root, int targetSum) { 
        if (root == null) return false;
        if (root != null && root.left == null && root.right == null) { 
            return (targetSum-root.val) == 0; 
        }
        
        boolean a = solve(root.left, targetSum-root.val);
        boolean b = solve(root.right, targetSum-root.val);
        
        return a || b; 
    }
}
```

