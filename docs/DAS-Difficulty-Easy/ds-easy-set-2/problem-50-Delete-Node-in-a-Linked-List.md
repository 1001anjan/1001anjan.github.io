---
layout: default
title: Delete Node in a Linked List
parent: Easy Set 2
grand_parent: DSA Easy Difficulty
nav_order: 19
permalink: /problem-50-Delete-Node-in-a-Linked-List/
---
# Delete Node in a Linked List

Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.

##### Example 1:
![](../../assets/images/ds/node1.jpeg)
```markdown
Input: head = [4,5,1,9], node = 5
Output: [4,1,9]
Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.
```
##### Constraints:
* The number of the nodes in the given list is in the range [2, 1000].
* -1000 <= Node.val <= 1000
* The value of each node in the list is unique.
* The node to be deleted is in the list and is not a tail node

### Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        
        //We are not going to delete the given node
        //We will delete the node next to it
        //Because for deleting the given node we need its previous node
        //And will copy its value to the given node
        
        //Storing the vaue of the next node to the given node
        int nextNodeVal = node.next.val;
        //Then removing that next node
        node.next = node.next.next;
        //And simply copy the value
        node.val = nextNodeVal;
    }
}
```
