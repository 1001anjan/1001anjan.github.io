---
layout: default
title: First Bad Version
parent: Easy Set 13
grand_parent: DSA Easy Difficulty
nav_order: 9
permalink: /problem-379-First Bad Version/
---
# First Bad Version
You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

##### Example 1:
```markdown
Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.
```
##### Example 2:
```markdown
Input: n = 1, bad = 1
Output: 1
```
##### Constraints:
* 1 <= bad <= n <= 231 - 1

### Solution:
```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int l = 1;
        while(l <= n){
            int m = l + (n - l)/2;;
            if(isBadVersion(m)){
                n = m - 1;
            }else{
                l = m + 1;
            }
        }
        return l;
    }
}
```