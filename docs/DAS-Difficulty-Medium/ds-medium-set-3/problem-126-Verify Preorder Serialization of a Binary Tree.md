---
layout: default
title: Verify Preorder Serialization of a Binary Tree
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 26
permalink: /problem-126-Verify Preorder Serialization of a Binary Tree/
---
# Verify Preorder Serialization of a Binary Tree
One way to serialize a binary tree is to use preorder traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as '#'.

![](../../assets/images/ds/pre-tree.jpeg)

For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where '#' represents a null node.

Given a string of comma-separated values preorder, return true if it is a correct preorder traversal serialization of a binary tree.

It is guaranteed that each comma-separated value in the string must be either an integer or a character '#' representing null pointer.

You may assume that the input format is always valid.

* For example, it could never contain two consecutive commas, such as "1,,3".
Note: You are not allowed to reconstruct the tree.


##### Example 1:
```markdown
Input: preorder = "9,3,4,#,#,1,#,#,2,#,6,#,#"
Output: true
```
##### Example 2:
```markdown
Input: preorder = "1,#"
Output: false
```
##### Example 3:
```markdown
Input: preorder = "9,#,#,1"
Output: false
```
##### Constraints:
* 1 <= preorder.length <= 10^4
* preorder consist of integers in the range [0, 100] and '#' separated by commas ','.

### Solution:
##### Using stack
```java
class Solution {
    public boolean isValidSerialization(String preorder) {
        if(preorder.length() == 1) return preorder.charAt(0) == '#';
        Stack<Character> st = new Stack<>();
        String[] strs = preorder.split(",");
        for(int i = 0; i < strs.length - 1; i++){
            if(!strs[i].equals("#")){
                st.push('L');
            }else{
                if(st.isEmpty()) return false;
                st.pop();
            }
        }
        return st.isEmpty();
    }
}
```

```java
class Solution {
     public boolean isValidSerialization(String preorder) {
        String[] strs = preorder.split(",");
        int degree = -1;         // root has no indegree, for compensate init with -1
        for (String str: strs) {
            degree++;             // all nodes have 1 indegree (root compensated)
            if (degree > 0) {     // total degree should never exceeds 0
                return false;
            }      
            if (!str.equals("#")) {// only non-leaf node has 2 outdegree
                degree -= 2;
            }  
        }
        return degree == 0;
    }
}
```
