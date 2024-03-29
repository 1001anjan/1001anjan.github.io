---
layout: default
title: Count Complete Tree Nodes
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 2
permalink: /problem-102-Count Complete Tree Nodes/
---
# Count Complete Tree Nodes
Given the root of a complete binary tree, return the number of the nodes in the tree.

According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Design an algorithm that runs in less than O(n) time complexity.

##### Example 1:
![](../../assets/images/ds/complete.jpeg)
```markdown
Input: root = [1,2,3,4,5,6]
Output: 6
```
##### Example 2:
```markdown
Input: root = []
Output: 0
```
##### Example 3:
```markdown
Input: root = [1]
Output: 1
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 5 * 10^4].
* 0 <= Node.val <= 5 * 10^4
* The tree is guaranteed to be complete.

### Solution:
```java
class Solution {

 public int countNodes(TreeNode root) {
	// edge conditions
	if (root == null) {
		return 0;
	}
	int left = helper1(root);
	int right = helper2(root);
	if (left == right) {
		return (1<<left)-1;
	}
	return countNodes(root.left) + countNodes(root.right) + 1;
}

private int helper1(TreeNode root) {
	if (root == null) {
		return 0;
	}
	return 1 + helper1(root.left);
}

private int helper2(TreeNode root) {
	if (root == null) {
		return 0;
	}
	return 1 + helper2(root.right);
}
}
```
