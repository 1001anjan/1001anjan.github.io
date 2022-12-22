---
layout: default
title: Remove Duplicates from Sorted List II
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 47
permalink: /problem-47-Remove Duplicates from Sorted List II/
---
# Remove Duplicates from Sorted List II
Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

##### Example 1:
![](../../assets/images/ds/linkedlist1.jpeg)

```markdown
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```
##### Example 2:
![](../../assets/images/ds/linkedlist2.jpeg)

```markdown
Input: head = [1,1,1,2,3]
Output: [2,3]
```
##### Constraints:
* The number of nodes in the list is in the range [0, 300].
* -100 <= Node.val <= 100
* The list is guaranteed to be sorted in ascending order.

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
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode ptr = head, qtr = head.next;

        // deleting starting node 
        while(ptr.val == qtr.val){
            while(qtr != null && ptr.val == qtr.val){
                ListNode temp = qtr;
                qtr = qtr.next;
                temp.next = null;
            } 
            if(qtr == null) return null;
            head = ptr = qtr;
            qtr = qtr.next;
            if(qtr == null) return head;
        }
        // checking remaining nodes
        ListNode prev = head;
        ptr = qtr;
        qtr = qtr.next;
        while(qtr != null){
            if(ptr.val != qtr.val){
                prev = ptr;
                ptr = qtr;
                qtr = qtr.next;
            }else{
                while(qtr != null && ptr.val == qtr.val){
                    ptr.next = ptr.next;
                    qtr = qtr.next;
                } 
                if(qtr == null){
                    prev.next = null;
                    return head;
                }
                prev.next = qtr;
                ptr = qtr;
                qtr = qtr.next;
            }
        }


        return head;
    }
}
```


