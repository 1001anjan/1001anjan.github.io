---
layout: default
title: Add Two Numbers
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 2
permalink: /problem-2-Add Two Numbers/
---
# Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.


##### Example 1:
![](../../assets/images/ds/addtwonumber1.jpeg)
```markdown
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```
##### Example 2:
```markdown
Input: l1 = [0], l2 = [0]
Output: [0]
```
##### Example 3:
```markdown
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

##### Constraints:
* The number of nodes in each linked list is in the range [1, 100].
* 0 <= Node.val <= 9
* It is guaranteed that the list represents a number that does not have leading zeros.

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode resultList, ptr;
        int c = 0;
        // creating first node 
        ListNode newNode = new ListNode((l1.val + l2.val)%10);
        c = (l1.val + l2.val) / 10;
        resultList = ptr = newNode;
        l1 = l1.next;
        l2 = l2.next;

        while(l1 != null && l2 != null){
            newNode = new ListNode((l1.val + l2.val + c)%10);
            c = (l1.val + l2.val + c) / 10;
            ptr.next = newNode;
            ptr = newNode;
            l1 = l1.next;
            l2 = l2.next;
        } 

        while(l1 != null){
            newNode = new ListNode((l1.val + c)%10);
            c = (l1.val + c) / 10;
            ptr.next = newNode;
            ptr = newNode;
            l1 = l1.next;
        }

        while(l2 != null){
            newNode = new ListNode((l2.val + c)%10);
            c = (l2.val + c) / 10;
            ptr.next = newNode;
            ptr = newNode;
            l2 = l2.next;
        }

        if(c > 0){
            newNode = new ListNode(c);
            ptr.next = newNode;
        }
        return resultList;
    }
}
```