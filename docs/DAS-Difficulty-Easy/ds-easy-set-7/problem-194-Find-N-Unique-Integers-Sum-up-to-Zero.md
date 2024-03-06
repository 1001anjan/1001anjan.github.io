---
layout: default
title: Find N Unique Integers Sum up to Zero
parent: Easy Set 7
grand_parent: DSA Easy
nav_order: 4
permalink: /problem-194-Find-N-Unique-Integers-Sum-up-to-Zero/
---
# Find N Unique Integers Sum up to Zero

Given an integer n, return any array containing n unique integers such that they add up to 0.

##### Example 1:
```markdown
Input: n = 5
Output: [-7,-1,1,3,4]
Explanation: These arrays also are accepted [-5,-1,1,2,3] , [-3,-1,2,-2,4].
```
##### Example 2:
```markdown
Input: n = 3
Output: [-1,0,1]
```
##### Example 3:
```markdown
Input: n = 1
Output: [0]
```
##### Constraints:
* 1 <= n <= 1000

### Solution:
```java
class Solution {
    public int[] sumZero(int n) {
        int[] ans = new int[n];
        int k = 1;
        if(n%2 == 0){
            for(int i = 0; i<n; i++){
                if(i%2 == 0)
                    ans[i] = k;
                else{
                    ans[i] = k*-1;
                    k++;
                }     
            }
        }else{
            ans[0] = 0;
            for(int i = 1; i<n; i++){
                if(i%2 == 0){
                    ans[i] = k*-1;
                    k++;
                }
                else{
                    ans[i] = k;
                }  
            }
        }
        return ans;
    }
}
```
### Other
```java
class Solution {
    public int[] sumZero(int n) {
        int[] result = new int[n];
        int start = (n/2)*-1, end = n/2, i = 0;
        
        while (start < end)
        {
            result[i] = start;
            result[n - i - 1] = end;
            ++start;
            --end;
            ++i;
        }
        
        return result;
    }
}
```