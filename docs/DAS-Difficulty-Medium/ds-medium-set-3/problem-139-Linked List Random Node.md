---
layout: default
title: Linked List Random Node
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 39
permalink: /problem-139-Linked List Random Node/
---
# Linked List Random Node
Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

Implement the Solution class:

* Solution(ListNode head) Initializes the object with the head of the singly-linked list head.
* int getRandom() Chooses a node randomly from the list and returns its value. All the nodes of the list should be equally likely to be chosen.

##### Example 1:
```markdown
Input
["Solution", "getRandom", "getRandom", "getRandom", "getRandom", "getRandom"]
[[[1, 2, 3]], [], [], [], [], []]
Output
[null, 1, 3, 2, 2, 3]

Explanation
Solution solution = new Solution([1, 2, 3]);
solution.getRandom(); // return 1
solution.getRandom(); // return 3
solution.getRandom(); // return 2
solution.getRandom(); // return 2
solution.getRandom(); // return 3
// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
```

##### Constraints:
* The number of nodes in the linked list will be in the range [1, 10^4].
* -10^4 <= Node.val <= 10^4
* At most 10^4 calls will be made to getRandom.

##### Follow up:
* What if the linked list is extremely large and its length is unknown to you?
* Could you solve this efficiently without using extra space?

### Solution:
```java
class Solution {
    private ArrayList<Integer> range = new ArrayList<>();

    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        while (head != null) {
            this.range.add(head.val);
            head = head.next;
        }
    }

    /** Returns a random node's value. */
    public int getRandom() {
        int pick = (int)(Math.random() * this.range.size());
        return this.range.get(pick);
    }
}
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
```
The above solution is simple, which happens to be fast as well. But it comes with two caveats:

* It requires some space to keep the pool of elements for sampling, which does not meet the constraint asked in the follow-up question, i.e. a solution of constant space.

* It cannot cope with the scenario that we have a list with ever-growing elements, i.e. we don't have unlimited memory to hold all the elements. For example, we have a stream of numbers, and we would like to pick a random number at any given moment. With the above naive solution, we would have to keep all the numbers in the memory, which is not scalable.

We will address the above caveats in the next approach.
### Reservoir Sampling
````java
class Solution {
    private ListNode head;

    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        this.head = head;
    }

    /** Returns a random node's value. */
    public int getRandom() {
        int scope = 1, chosenValue = 0;
        ListNode curr = this.head;
        while (curr != null) {
            // decide whether to include the element in reservoir
            if (Math.random() < 1.0 / scope)
                chosenValue = curr.val;
            // move on to the next node
            scope += 1;
            curr = curr.next;
        }
        return chosenValue;
    }
}
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
````