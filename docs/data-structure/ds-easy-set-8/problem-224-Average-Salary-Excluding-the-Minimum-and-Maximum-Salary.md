---
layout: default
title: Average Salary Excluding the Minimum and Maximum Salary
parent: Data Structure Easy Set 8
grand_parent: Data Structure
nav_order: 4
permalink: /problem-224-Average-Salary-Excluding-the-Minimum-and-Maximum-Salary/
---
# Average Salary Excluding the Minimum and Maximum Salary

You are given an array of unique integers salary where salary[i] is the salary of the ith employee.

Return the average salary of employees excluding the minimum and maximum salary. Answers within 10-5 of the actual answer will be accepted.

##### Example 1:
```markdown
Input: salary = [4000,3000,1000,2000]
Output: 2500.00000
Explanation: Minimum salary and maximum salary are 1000 and 4000 respectively.
Average salary excluding minimum and maximum salary is (2000+3000) / 2 = 2500
```
##### Example 2:
```markdown
Input: salary = [1000,2000,3000]
Output: 2000.00000
Explanation: Minimum salary and maximum salary are 1000 and 3000 respectively.
Average salary excluding minimum and maximum salary is (2000) / 1 = 2000
```
##### Constraints:
* 3 <= salary.length <= 100
* 1000 <= salary[i] <= 106
* All the integers of salary are unique.

### Solution:
```java
class Solution {
    public double average(int[] salary) {
       int max = Math.max(salary[0],salary[1]);
        int min = Math.min(salary[0],salary[1]);
        double sum = max + min;
        for(int i = 2; i < salary.length; i++){
            if(max < salary[i]){
                max = salary[i];
            }else if(min > salary[i]){
                min = salary[i];
            }
            sum += salary[i];
        }
        sum = sum - max - min;

        return sum/(salary.length - 2);
    }
}
```