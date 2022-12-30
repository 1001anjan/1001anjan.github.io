---
layout: default
title: Number of Students Unable to Eat Lunch
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 6
permalink: /problem-256-Number-of-Students-Unable-to-Eat-Lunch/
---
# Number of Students Unable to Eat Lunch

The school cafeteria offers circular and square sandwiches at lunch break, referred to by numbers 0 and 1 respectively. All students stand in a queue. Each student either prefers square or circular sandwiches.

The number of sandwiches in the cafeteria is equal to the number of students. The sandwiches are placed in a stack. At each step:

* If the student at the front of the queue prefers the sandwich on the top of the stack, they will take it and leave the queue.
* Otherwise, they will leave it and go to the queue's end.
This continues until none of the queue students want to take the top sandwich and are thus unable to eat.

You are given two integer arrays students and sandwiches where sandwiches[i] is the type of the i​​​​​​th sandwich in the stack (i = 0 is the top of the stack) and students[j] is the preference of the j​​​​​​th student in the initial queue (j = 0 is the front of the queue). Return the number of students that are unable to eat.

##### Example 1:
```markdown
Input: students = [1,1,0,0], sandwiches = [0,1,0,1]
Output: 0
Explanation:
- Front student leaves the top sandwich and returns to the end of the line making students = [1,0,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,0,1,1].
- Front student takes the top sandwich and leaves the line making students = [0,1,1] and sandwiches = [1,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [1,1,0].
- Front student takes the top sandwich and leaves the line making students = [1,0] and sandwiches = [0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,1].
- Front student takes the top sandwich and leaves the line making students = [1] and sandwiches = [1].
- Front student takes the top sandwich and leaves the line making students = [] and sandwiches = [].
  Hence all students are able to eat.
```
##### Example 2:
```markdown
Input: students = [1,1,1,0,0,1], sandwiches = [1,0,0,0,1,1]
Output: 3
```
##### Constraints:
* 1 <= students.length, sandwiches.length <= 100
* students.length == sandwiches.length
* sandwiches[i] is 0 or 1.
* students[i] is 0 or 1.

### Solution:
```java
class Solution {
    public int countStudents(int[] students, int[] sandwiches) {
        Queue<Integer> q = new LinkedList<>();
        for(int n : students) q.add(n);
        int c = q.size();
        int i = 0;
        
        while(c > 0){
            int n = q.poll();
            if(n == sandwiches[i]){
                i++;
                c = q.size();
            }else{
                q.add(n);
                c--;
            }
        }
        return q.size();
    }
}
```

##### Array Implementation and faster
```java
class Solution {
    public int countStudents(int[] students, int[] sandwiches) {
        int c0, c1;
        c0 = c1 = 0;
        for(int n : students){
            if(n == 0) 
                c0++;
            else
                c1++;
        }
        
        for(int n : sandwiches){
            if(n == 0){
                if(c0 == 0) break;
                c0--;
            }else{
                if(c1 == 0) break;
                c1--;
            }
        }
        
        return c1 + c0;
    }
}
```