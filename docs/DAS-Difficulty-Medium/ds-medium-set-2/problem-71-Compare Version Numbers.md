---
layout: default
title: Compare Version Numbers
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 21
permalink: /problem-71-Compare Version Numbers/
---
# Compare Version Numbers
Given two version numbers, version1 and version2, compare them.

Version numbers consist of one or more revisions joined by a dot '.'. Each revision consists of digits and may contain leading zeros. Every revision contains at least one character. Revisions are 0-indexed from left to right, with the leftmost revision being revision 0, the next revision being revision 1, and so on. For example 2.5.33 and 0.1 are valid version numbers.

To compare version numbers, compare their revisions in left-to-right order. Revisions are compared using their integer value ignoring any leading zeros. This means that revisions 1 and 001 are considered equal. If a version number does not specify a revision at an index, then treat the revision as 0. For example, version 1.0 is less than version 1.1 because their revision 0s are the same, but their revision 1s are 0 and 1 respectively, and 0 < 1.

Return the following:

* If version1 < version2, return -1.
* If version1 > version2, return 1.
* Otherwise, return 0.

##### Example 1:
```markdown
Input: version1 = "1.01", version2 = "1.001"
Output: 0
Explanation: Ignoring leading zeroes, both "01" and "001" represent the same integer "1".
```
##### Example 2:
```markdown
Input: version1 = "1.0", version2 = "1.0.0"
Output: 0
Explanation: version1 does not specify revision 2, which means it is treated as "0".
```
##### Example 3:
```markdown
Input: version1 = "0.1", version2 = "1.1"
Output: -1
Explanation: version1's revision 0 is "0", while version2's revision 0 is "1". 0 < 1, so version1 < version2.
```
##### Constraints:
* 1 <= version1.length, version2.length <= 500
* version1 and version2 only contain digits and '.'.
* version1 and version2 are valid version numbers.
* All the given revisions in version1 and version2 can be stored in a 32-bit integer.

### Solution:
```java
class Solution {
    public int compareVersion(String version1, String version2) {
        int m = version1.length();
        int n = version2.length();
        char[] v1 = version1.toCharArray();
        char[] v2 = version2.toCharArray();
        int i = 0, j = 0;
        while(i < m || j < n){
            while(i < m && v1[i] == '0') i++;
            int value1 = 0;
            while(i < m && v1[i] != '.') value1 = value1*10 + (v1[i++] - '0');

            while(j < n && v2[j] == '0') j++;
            int value2 = 0;
            while(j < n && v2[j] != '.') value2 = value2*10 + (v2[j++] - '0');
            if(value1 > value2) return 1;
            else if(value1 < value2) return -1;
            i++;
            j++;
        }
        
        return 0;
    }
}
```