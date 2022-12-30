---
layout: default
title: Container With Most Water
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 7
permalink: /problem-7-Container With Most Water/
---
# Container With Most Water
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

##### Example 1:
![](../../assets/images/ds/question_11.jpeg)
```markdown
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```
##### Example 2:
```markdown
Input: height = [1,1]
Output: 1
```
##### Constraints:
* n == height.length
* 2 <= n <= 10^5
* 0 <= height[i] <= 10^4

### Solution:
```java
class Solution {
    public int maxArea(int[] height) {
        int max = 0, s = 0, e = height.length - 1;
        while( s < e){
            int h;
            if(height[s] > height[e]){
                h = height[e];
                max = Math.max(max, h * (e - s));
                e--;
            }else{
                h = height[s];
                max = Math.max(max, h * (e - s));
                s++; 
            }
        }
        return max;
    }
}
```
