---
layout: default
title: Find Mode in Binary Search Tree
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 27
permalink: /problem-90-Find-Mode-in-Binary-Search-Tree/
---
# Find Mode in Binary Search Tree

Given the root of a binary search tree (BST) with duplicates, return all the mode(s) (i.e., the most frequently occurred element) in it.

If the tree has more than one mode, return them in any order.

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than or equal to the node's key.
The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
Both the left and right subtrees must also be binary search trees.

##### Example 1:
![](../../assets/images/ds/mode-tree.jpeg)
```markdown
Input: root = [1,null,2,2]
Output: [2]
```
##### Example 2:
```markdown
Input: root = [0]
Output: [0]
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 104].
* -105 <= Node.val <= 105

Follow up: Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

### Solution:
```java
class Solution {
    private TreeNode pre = null;
    private int max = 1;
    private int cnt = 1; // counts for leftmost node self
    
    public int[] findMode(TreeNode root) {
        List<Integer> nums = new ArrayList<>();
        inOrder(root, nums);
        int[] arr = new int[nums.size()];
        for (int i = 0; i < nums.size(); i++) arr[i] = nums.get(i);
        return arr;
    }
    
    private void inOrder(TreeNode root, List<Integer> nums) {
        if (root == null) {
            return;
        }
        // in-order traversal, left-root-right
        inOrder(root.left, nums);
        // if consecutive integers are the same
        if (pre != null) {
            cnt = (pre.val == root.val) ? cnt + 1 : 1;
        }
        // if current value's frequency is larger than the max one
        if (cnt > max) {
            max = cnt;
            nums.clear();
            nums.add(root.val);
        } else if (cnt == max) {
            // frequency equals, add current root value
            nums.add(root.val);
        }
        pre = root; // update pre node
        inOrder(root.right, nums); // in-order
    }
}
```

```java
class Solution {
    TreeNode pre = null;
    int max = 1;
    int count = 1;
    public int[] findMode(TreeNode root) {
        List<Integer> list = new ArrayList<Integer>();
        traverseInorder(root, list);
        return list.stream().mapToInt(i->i).toArray();
    }
    
    public void traverseInorder(TreeNode root, List<Integer> list){
        if(root == null) return;
        traverseInorder(root.left, list);
        if(pre != null){
            count = (pre.val == root.val)? count+1: 1;
        }
        if(count>max){
            max = count;
            list.clear();
            list.add(root.val);
        }else if(count == max){
            list.add(root.val);
        }
        pre = root;
        traverseInorder(root.right, list);
    }
}
```
