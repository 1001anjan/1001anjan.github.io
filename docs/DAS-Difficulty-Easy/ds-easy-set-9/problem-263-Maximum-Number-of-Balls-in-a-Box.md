---
layout: default
title: Maximum Number of Balls in a Box
parent: Easy Set 9
grand_parent: DSA Easy
nav_order: 13
permalink: /problem-263-Maximum-Number-of-Balls-in-a-Box/
---
# Maximum Number of Balls in a Box

You are working in a ball factory where you have n balls numbered from lowLimit up to highLimit inclusive (i.e., n == highLimit - lowLimit + 1), and an infinite number of boxes numbered from 1 to infinity.

Your job at this factory is to put each ball in the box with a number equal to the sum of digits of the ball's number. For example, the ball number 321 will be put in the box number 3 + 2 + 1 = 6 and the ball number 10 will be put in the box number 1 + 0 = 1.

Given two integers lowLimit and highLimit, return the number of balls in the box with the most balls.

##### Example 1:
```markdown
Input: lowLimit = 1, highLimit = 10
Output: 2
Explanation:
Box Number:  1 2 3 4 5 6 7 8 9 10 11 ...
Ball Count:  2 1 1 1 1 1 1 1 1 0  0  ...
Box 1 has the most number of balls with 2 balls.
```
##### Example 2:
````markdown
Input: lowLimit = 5, highLimit = 15
Output: 2
Explanation:
Box Number:  1 2 3 4 5 6 7 8 9 10 11 ...
Ball Count:  1 1 1 1 2 2 1 1 1 0  0  ...
Boxes 5 and 6 have the most number of balls with 2 balls in each.
````
##### Example 3:
```markdown
Input: lowLimit = 19, highLimit = 28
Output: 2
Explanation:
Box Number:  1 2 3 4 5 6 7 8 9 10 11 12 ...
Ball Count:  0 1 1 1 1 1 1 1 1 2  0  0  ...
Box 10 has the most number of balls with 2 balls.
```
##### Constraints:
* 1 <= lowLimit <= highLimit <= 10^5

### Solution:
```java
class Solution {
    public int countBalls(int lowLimit, int highLimit) {
        Map<Integer,Integer> m = new HashMap<>();
        int max = 0;
        
        int key = getKey(lowLimit);
        m.put(key, 1);
        max = Math.max(max,m.get(key));
        
        for(int i = lowLimit + 1; i <= highLimit; i++){
            if(i % 10 == 0){
               key = getKey(i); 
            }else{
               key++;
            }
            m.put(key, m.getOrDefault(key,0) + 1);
            max = Math.max(max,m.get(key));
        }
        
        return max;
    }
    
    public int getKey(int n){
        int sum = 0;
        while(n > 0){
            sum += n%10;
            n = n / 10;
        }
        return sum;
    }
}
```

#### Faster
```java
/**
 INPUT :- 1 <= lowLimit <= highLimit <= 10^5
 so the max number of boxes that can be there are 99999 = 45.
 **/
class Solution {
    public int countBalls(int lowLimit, int highLimit) {
        int[] boxes = new int[46];
        int max = 0;
        int key = getKey(lowLimit);
        boxes[key]++;
        max = Math.max(max,boxes[key]);
        
        for(int i = lowLimit + 1; i <= highLimit; i++){
            if(i % 10 == 0){
               key = getKey(i); 
            }else{
               key++;
            }
            boxes[key]++;
            max = Math.max(max,boxes[key]);
        }
        
        return max;        
        
    }
    
    public int getKey(int n){
        int sum = 0;
        while(n > 0){
            sum += n%10;
            n = n / 10;
        }
        return sum;
    }
}
```
