---
layout: default
title: Binary Tree Right Side View
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 43
permalink: /problem-93-Binary Tree Right Side View/
---
# Binary Tree Right Side View
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

##### Example 1:
![](../../assets/images/ds/tree1212.jpeg)
```markdown
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```
###### Example 2:
```markdown
Input: root = [1,null,3]
Output: [1,3]
```
##### Example 3:
```markdown
Input: root = []
Output: []
```
A useful test case for this problem would be:
```markdown
Input: root = [1,2,3,null,5,6,null,4]
```
![](../../assets/images/ds/cef92daf-88dd-46b5-a329-b179916c6482_1618278364.1240458.png )

##### Constraints:
* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

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
    public List<Integer> rightSideView(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        List<Integer> res = new ArrayList<>();
        q.offer(root);

        while(!q.isEmpty()){
            Queue<TreeNode> q1 = new LinkedList<>();
            int size = q.size();
            for(int i = 1; i < size; i++){
                TreeNode n = q.poll();
                if(n.left != null) q1.offer(n.left);
                if(n.right != null) q1.offer(n.right);
            }
            TreeNode n = q.poll();
            if(n == null) break;
            res.add(n.val);
            if(n.left != null) q1.offer(n.left);
            if(n.right != null) q1.offer(n.right);

            q = q1;
        }

        return res;
    }
}
```
The core idea of this algorithm:

1.Each depth of the tree only select one node.
2. View depth is current size of result list.
```java
public class Solution {
    public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<Integer>();
    rightView(root, result, 0);
    return result;
    }

    public void rightView(TreeNode curr, List<Integer> result, int currDepth){
        if(curr == null){
            return;
        }
        if(currDepth == result.size()){
            result.add(curr.val);
        }
        
        rightView(curr.right, result, currDepth + 1);
        rightView(curr.left, result, currDepth + 1);
        
    }
}
```