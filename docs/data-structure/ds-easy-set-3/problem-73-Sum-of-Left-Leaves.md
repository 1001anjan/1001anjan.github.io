---
layout: default
title: Sum of Left Leaves
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 10
permalink: /problem-73-Sum-of-Left-Leaves/
---
# Sum of Left Leaves

Given the root of a binary tree, return the sum of all left leaves.

A leaf is a node with no children. A left leaf is a leaf that is the left child of another node.

##### Example 1:
![](../../assets/images/ds/leftsum-tree.jpeg)
```markdown
Input: root = [3,9,20,null,null,15,7]
Output: 24
Explanation: There are two left leaves in the binary tree, with values 9 and 15 respectively.
```
##### Example 2:
````markdown
Input: root = [1]
Output: 0
````
##### Constraints:
* The number of nodes in the tree is in the range [1, 1000].
* -1000 <= Node.val <= 1000

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
class NodeMap{
    public TreeNode head;
    public char f;
    NodeMap(TreeNode t, char c){
        head = t;
        f = c;
    }
    
}
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        Stack<NodeMap> s = new Stack<NodeMap>();
        NodeMap m = new NodeMap(root,'*');
        s.push(m);
        int sum  = 0;
        NodeMap t;
        while(!s.isEmpty()){
            t = s.pop();
            if(t.f == 'L' && t.head.left == null && t.head.right == null) sum = sum + t.head.val;
            if(t.head.left != null ) s.push(new NodeMap(t.head.left, 'L'));
            if(t.head.right != null) s.push(new NodeMap(t.head.right, 'R'));
        }
        return sum;
    }
}
```


