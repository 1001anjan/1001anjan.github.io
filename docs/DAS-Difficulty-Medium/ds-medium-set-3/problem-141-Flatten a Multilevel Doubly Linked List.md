---
layout: default
title: Flatten a Multilevel Doubly Linked List
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 41
permalink: /problem-141-Flatten a Multilevel Doubly Linked List/
---
# Flatten a Multilevel Doubly Linked List
You are given a doubly linked list, which contains nodes that have a next pointer, a previous pointer, and an additional child pointer. This child pointer may or may not point to a separate doubly linked list, also containing these special nodes. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure as shown in the example below.

Given the head of the first level of the list, flatten the list so that all the nodes appear in a single-level, doubly linked list. Let curr be a node with a child list. The nodes in the child list should appear after curr and before curr.next in the flattened list.

Return the head of the flattened list. The nodes in the list must have all of their child pointers set to null.

##### Example 1:
![](../../assets/images/ds/flatten11.jpeg)
```markdown
Input: head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
Output: [1,2,3,7,8,11,12,9,10,4,5,6]
Explanation: The multilevel linked list in the input is shown.
After flattening the multilevel linked list it becomes:
```
![](../../assets/images/ds/flatten12.jpeg)
##### Example 2:
![](../../assets/images/ds/flatten22222.jpg)
```markdown
Input: head = [1,2,null,3]
Output: [1,3,2]
Explanation: The multilevel linked list in the input is shown.
After flattening the multilevel linked list it becomes:
```
![](../../assets/images/ds/list121.jpeg)
##### Example 3:

```markdown
Input: head = []
Output: []
Explanation: There could be empty list in the input.
```
##### Constraints:
* The number of Nodes will not exceed 1000.
* 1 <= Node.val <= 10^5


##### How the multilevel linked list is represented in test cases:

We use the multilevel linked list from Example 1 above:
```markdown
1---2---3---4---5---6--NULL
|
7---8---9---10--NULL
|
11--12--NULL
```
The serialization of each level is as follows:
```markdown
[1,2,3,4,5,6,null]
[7,8,9,10,null]
[11,12,null]
```
To serialize all levels together, we will add nulls in each level to signify no node connects to the upper node of the previous level. The serialization becomes:

```markdown
[1,    2,    3, 4, 5, 6, null]
             |
[null, null, 7,    8, 9, 10, null]
                   |
[            null, 11, 12, null]
```
Merging the serialization of each level and removing trailing nulls we obtain:
```markdown
[1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
```

### Solution:
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;
};
*/

class Solution {
    public Node flatten(Node head) {
        Node ptr, qtr, res;
        ptr = qtr = res = head;
        Stack<Node> stack = new Stack<>();
        while(ptr != null){
            if(ptr.next == null && !stack.isEmpty() && ptr.child == null){
                ptr = stack.pop();
                qtr.next = ptr;
                ptr.prev = qtr;
                qtr = ptr;
            }else
            if(ptr.child != null){
                if(ptr.next != null) stack.push(ptr.next);
                ptr = ptr.child;
                qtr.next = ptr;
                ptr.prev = qtr;
                qtr.child = null;
                qtr = ptr;
            }else{
                ptr = ptr.next;
                qtr = ptr;
            }
        }

        return res;
    }
}
```
#### Recursion
```java
class Solution {

    public Node flatten(Node head) {
        return helper(head, new Node());
    }

    public Node helper(Node head, Node prevDummy) {
        Node cur = head;
        while (cur != null) {
            if (cur.child != null) {
                Node next = cur.next;
                cur.child.prev = cur;
                cur.next = helper(cur.child, prevDummy);
                cur.child = null;
                if (next != null) {
                    Node prev = prevDummy.next;
                    prev.next = next;
                    next.prev = prev;
                }
            }

            prevDummy.next = cur;
            cur = cur.next;
        }

        return head;
    }
}
```