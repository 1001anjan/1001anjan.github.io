---
layout: default
title: Print in Order
parent: Easy Set 6
grand_parent: DSA Easy Difficulty
nav_order: 19
permalink: /problem-179-Print-in-Order/
---
# Print in Order

Suppose we have a class:
```markdown
public class Foo {
public void first() { print("first"); }
public void second() { print("second"); }
public void third() { print("third"); }
}
```
The same instance of Foo will be passed to three different threads. Thread A will call first(), thread B will call second(), and thread C will call third(). Design a mechanism and modify the program to ensure that second() is executed after first(), and third() is executed after second().

##### Note:

We do not know how the threads will be scheduled in the operating system, even though the numbers in the input seem to imply the ordering. The input format you see is mainly to ensure our tests' comprehensiveness.

##### Example 1:
```markdown
Input: nums = [1,2,3]
Output: "firstsecondthird"
Explanation: There are three threads being fired asynchronously. The input [1,2,3] means thread A calls first(), thread B calls second(), and thread C calls third(). "firstsecondthird" is the correct output.
```
##### Example 2:
```markdown
Input: nums = [1,3,2]
Output: "firstsecondthird"
Explanation: The input [1,3,2] means thread A calls first(), thread B calls third(), and thread C calls second(). "firstsecondthird" is the correct output.
```
##### Constraints:
* nums is a permutation of [1, 2, 3].

### Solution:
```java
class Foo {

    private boolean first = false;
    private boolean second = false;
    private boolean third = false;
    
    public Foo(){
        
    }

    public void first(Runnable printFirst) throws InterruptedException {
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        
        first = true;
    }

    public void second(Runnable printSecond) throws InterruptedException {
        while (!this.first) {
            try {
                Thread.sleep(1);
            } catch (InterruptedException e) {
            }
        }
        
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        
        this.second = true;
    }

    public void third(Runnable printThird) throws InterruptedException {
        while (!this.second) {
            try {
               Thread.sleep(1);
            } catch (InterruptedException e) {
            }
        }
        
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
    }
}
```

