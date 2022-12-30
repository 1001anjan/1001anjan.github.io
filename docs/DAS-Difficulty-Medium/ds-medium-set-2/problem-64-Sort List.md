---
layout: default
title: Sort List
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 14
permalink: /problem-64-Sort List/
---
# Sort List
Given the head of a linked list, return the list after sorting it in ascending order.

##### Example 1:
![](../../assets/images/ds/sort_list_1.jpeg)
```markdown
Input: head = [4,2,1,3]
Output: [1,2,3,4]
```
##### Example 2:
![](../../assets/images/ds/sort_list_2.jpeg)

```markdown
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]
```
##### Example 3:
```markdown
Input: head = []
Output: []
```
##### Constraints:
* The number of nodes in the list is in the range [0, 5 * 10^4].
* -10^5 <= Node.val <= 10^5

Follow up: Can you sort the linked list in O(n logn) time and O(1) memory (i.e. constant space)?

### Solution:
##### O(n*n) complexity
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
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode ptr = head, sortedList = null, qtr;
        while(ptr != null){
            qtr = ptr;
            ptr = ptr.next;
            sortedList = insertSortedList(sortedList, qtr);
        } 
        return sortedList;
        
    }

    public ListNode insertSortedList(ListNode list, ListNode node){
        if(list == null){
            list = node;
            list.next = null;
            return list;
        }
        // inserting as first node
        if(list.val >= node.val){
            node.next = list;
            list = node;
            return list;
        }
        // inserting to middle
        ListNode ptr = list;
        while(ptr.next != null){
            if(ptr.next.val > node.val){
                node.next = ptr.next;
                ptr.next = node;
                return list;
            }
            ptr = ptr.next;
        }
        // inserting as end node
        ptr.next = node;
        node.next = null;
        return list;
    }
}
```
##### Merge sort
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
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode slow = head, fast = head, prev = head;
        while(fast != null && fast.next != null){
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        prev.next = null;

        ListNode l1 = sortList(head);
        ListNode l2 = sortList(slow);
        return mergeList(l1, l2);
        
    }

    public ListNode mergeList(ListNode l1, ListNode l2){
        ListNode dummyHead = new ListNode(), ptr= dummyHead;
        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                ptr.next = l1;
                l1 = l1.next;
            }else{
                ptr.next = l2;
                l2 = l2.next;
            }
            ptr = ptr.next;
        }

        if(l1 != null){
            ptr.next = l1;
        }
        if(l2 != null){
            ptr.next = l2;
        }
        return dummyHead.next;
    }
}
```

