---
layout: default
title: Check if All the Integers in a Range Are Covered
parent: Easy Set 10
grand_parent: DSA Easy
nav_order: 8
permalink: /problem-288-Check-if-All-the-Integers-in-a-Range-Are-Covered/
---
# Check if All the Integers in a Range Are Covered
You are given a 2D integer array ranges and two integers left and right. Each ranges[i] = [starti, endi] represents an inclusive interval between starti and endi.

Return true if each integer in the inclusive range [left, right] is covered by at least one interval in ranges. Return false otherwise.

An integer x is covered by an interval ranges[i] = [starti, endi] if starti <= x <= endi.

##### Example 1:
```markdown
Input: ranges = [[1,2],[3,4],[5,6]], left = 2, right = 5
Output: true
Explanation: Every integer between 2 and 5 is covered:
- 2 is covered by the first range.
- 3 and 4 are covered by the second range.
- 5 is covered by the third range.
```
##### Example 2:
```markdown
Input: ranges = [[1,10],[10,20]], left = 21, right = 21
Output: false
Explanation: 21 is not covered by any range.
```
##### Constraints:
* 1 <= ranges.length <= 50
* 1 <= starti <= endi <= 50
* 1 <= left <= right <= 50

### Solution:
```java
class Solution {
    public boolean isCovered(int[][] ranges, int left, int right) {
        boolean[] all = new boolean[51];
        for(int[] arr : ranges){
            for(int i = arr[0]; i <= arr[1]; i++)
                all[i] = true;
        }
        while(left <= right){
            if(!all[left]) return false;
            left++;
        }
        
        return true;
    }
}
```

