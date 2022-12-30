---
layout: default
title: Remove Duplicates from Sorted Linked List
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 17
permalink: /problem-17-remove-duplicates-from-sorted-list/
---
# Remove Duplicates from Sorted List
Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.
#### Example 1
```markdown
Input: head = [1,1,2]
Output: [1,2]
```
#### Example 2
```markdown
Input: head = [1,1,2,3,3]
Output: [1,2,3]
```

### Constraints:

* The number of nodes in the list is in the range [0, 300].
* -100 <= Node.val <= 100
* The list is guaranteed to be sorted in ascending order.

### Solution
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
        if (head == null || head.next == null ) return head;
        ListNode res, ptr, rem;
        
        // create first node
        res = ptr = head;
        int currVal = head.val;
        head = head.next;
        res.next = null;
        
        while(head != null){
           if(head.val == currVal){
               rem = head;
               head = head.next;
               rem.next = null;
           }else{
               ptr.next = head;
               ptr = ptr.next;
               head = head.next;
               ptr.next = null;
               currVal = ptr.val;
           } 
        }
        return res;
    }
}
```