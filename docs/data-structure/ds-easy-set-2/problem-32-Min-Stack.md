---
layout: default
title: Min Stack
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 1
permalink: /problem-31-Min-Stack/
---
#  Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

* MinStack() initializes the stack object.
* void push(int val) pushes the element val onto the stack.
* void pop() removes the element on the top of the stack.
* int top() gets the top element of the stack.
* int getMin() retrieves the minimum element in the stack.


##### Example 1:
```markdown
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

### Constraints:
* -231 <= val <= 231 - 1
* Methods pop, top and getMin operations will always be called on non-empty stacks.
* At most 3 * 104 calls will be made to push, pop, top, and getMin.

### Solution
```java
class MinStack {
    public class Node {
        int val;
        Node above;
        Node below;
        Node() {
            val = 0;
            above = null;
            below = null;
        }
    }
    
    Node top;
    public MinStack() {
        top = new Node();
    }
    
    public void push(int val) {
        Node newNode = new Node();
        newNode.val = val;
        top.above = newNode;
        newNode.below = top;
        top = newNode;
    }
    
    // old top node gets lost to the abyss of rubbish data
    public void pop() {
        top = top.below;
        top.above = null;
    }
    
    public int top() {
        return top.val;
    }
    
    public int getMin() {
        int min = 2147483647;  // max int
        Node traverse = top;
        while (traverse.below != null) {
            if (traverse.val < min) min = traverse.val;
            traverse = traverse.below;
        }
        return min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```