---
layout: default
title: Check if Binary String Has at Most One Segment of Ones
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 20
permalink: /problem-270-Check-if-Binary-String-Has-at-Most-One-Segment-of-Ones/
---
# Check if Binary String Has at Most One Segment of Ones
Given a binary string s without leading zeros, return true if s contains at most one contiguous segment of ones. Otherwise, return false.

##### Example 1:
```markdown
Input: s = "1001"
Output: false
Explanation: The ones do not form a contiguous segment.
```
##### Example 2:
```markdown
Input: s = "110"
Output: true
```
##### Constraints:
* 1 <= s.length <= 100
* s[i] is either '0' or '1'.
* s[0] is '1'

### Solution:
Just increase the count when 0 comes, and when we get 1, check the value of count, if is not 0, return false

```java
class Solution {
    public boolean checkOnesSegment(String s) {
        boolean consecOne = true;
        int count = 0;
        for(char c: s.toCharArray()){
            if(c == '0') count++;
            else {
                if(count != 0) return false;
            }
        }
        return true;
    }
}
```