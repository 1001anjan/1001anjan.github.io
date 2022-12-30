---
layout: default
title: Odd Even Linked List
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 1
permalink: /problem-1-Odd Even Linked List/
---

#  Odd Even Linked List
Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The first node is considered odd, and the second node is even, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in O(1) extra space complexity and O(n) time complexity.

##### Example 1:
![](../../assets/images/ds/oddeven-linked-list.jpeg)
```markdown
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]
```
##### Example 2:

```markdown
Input: head = [2,1,3,5,6,4,7]
Output: [2,3,6,7,1,5,4]
```
##### Constraints:
* The number of nodes in the linked list is in the range [0, 104].
* -10^6 <= Node.val <= 10^6

### Solution: 
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if(head == null) return head;
        ListNode oddList, evenList, ptr, qtr;
        // create first node
        oddList = ptr = head;
        head = head.next;
        if(head == null) return oddList;
        evenList = qtr = head;
        head = head.next;
        boolean f = true;
        while(head != null){
            
            if(f){
                ptr.next = head;
                ptr = head;
            }else{
                qtr.next = head;
                qtr = head;
            }
            head = head.next;
            f = !f;
        }

        ptr.next = evenList;
        qtr.next = null;
        return oddList;
    }
}
```
