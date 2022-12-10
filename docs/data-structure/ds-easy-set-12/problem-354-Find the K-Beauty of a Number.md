---
layout: default
title: Find the K-Beauty of a Number
parent: Data Structure Easy Set 12
grand_parent: Data Structure
nav_order: 14
permalink: /problem-354-Find the K-Beauty of a Number/
---
# Find the K-Beauty of a Number
The k-beauty of an integer num is defined as the number of substrings of num when it is read as a string that meet the following conditions:

* It has a length of k.
* It is a divisor of num.
Given integers num and k, return the k-beauty of num.

###### Note:
* Leading zeros are allowed.
* 0 is not a divisor of any value.
* A substring is a contiguous sequence of characters in a string.

##### Example 1:
```markdown
Input: num = 240, k = 2
Output: 2
Explanation: The following are the substrings of num of length k:
- "24" from "240": 24 is a divisor of 240.
- "40" from "240": 40 is a divisor of 240.
  Therefore, the k-beauty is 2.
```
##### Example 2:
```markdown
Input: num = 430043, k = 2
Output: 2
Explanation: The following are the substrings of num of length k:
- "43" from "430043": 43 is a divisor of 430043.
- "30" from "430043": 30 is not a divisor of 430043.
- "00" from "430043": 0 is not a divisor of 430043.
- "04" from "430043": 4 is not a divisor of 430043.
- "43" from "430043": 43 is a divisor of 430043.
  Therefore, the k-beauty is 2.
```
##### Constraints:
* 1 <= num <= 109
* 1 <= k <= num.length (taking num as a string)

### Solution:
```java
class Solution {
    public int divisorSubstrings(int num, int k) {
        String str = String.valueOf(num);
        int c = 0;
        for(int i = 0; i <= str.length() - k; i++){
            int d = Integer.parseInt(str.substring(i, i + k));
            if(d != 0 && num % d == 0) c++;
        }
        return c;
    }
}
```