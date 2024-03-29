---
layout: default
title: Middle of the Linked List
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 10
permalink: /problem-140-Middle-of-the-Linked-List/
---
# Middle of the Linked List

Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.



##### Example 1:
![](../../assets/images/ds/lc-midlist1.jpeg![img.png](img.png))
````markdown
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
````
##### Example 2:
![](../../assets/images/ds/lc-midlist2.jpeg)
```markdown
Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
```
##### Constraints:
* The number of nodes in the list is in the range [1, 100].
* 1 <= Node.val <= 100

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
    public ListNode middleNode(ListNode head) {
        ListNode slow, fast;
        slow = fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```