---
layout: default
title: Binary Gap
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 8
permalink: /problem-138-Binary-Gap/
---
# Binary Gap
Given a positive integer n, find and return the longest distance between any two adjacent 1's in the binary representation of n. If there are no two adjacent 1's, return 0.

Two 1's are adjacent if there are only 0's separating them (possibly no 0's). The distance between two 1's is the absolute difference between their bit positions. For example, the two 1's in "1001" have a distance of 3.

##### Example 1:
```markdown
Input: n = 22
Output: 2
Explanation: 22 in binary is "10110".
The first adjacent pair of 1's is "10110" with a distance of 2.
The second adjacent pair of 1's is "10110" with a distance of 1.
The answer is the largest of these two distances, which is 2.
Note that "10110" is not a valid pair since there is a 1 separating the two 1's underlined.
```
##### Example 2:
```markdown
Input: n = 8
Output: 0
Explanation: 8 in binary is "1000".
There are not any adjacent pairs of 1's in the binary representation of 8, so we return 0.
```
##### Example 3:
```markdown
Input: n = 5
Output: 2
Explanation: 5 in binary is "101".
```
##### Constraints:
* 1 <= n <= 109

```java
class Solution {
    public int binaryGap(int n) {
        int prevMax = 0;
        String bits = Integer.toBinaryString(n);
        int s = 0;
        int e = 0;
        boolean f = false;
        for(int i=0; i<bits.length(); i++){
            if(bits.charAt(i) == '1'){
                if(!f){
                    s = i;
                    f = true;
                }else{
                    e = i;
                    prevMax = Math.max(prevMax, e-s);
                    s = i;
                }
            }
        }
        return prevMax;
    }
}
```
```java
class Solution {
    public int binaryGap(int N) {
        int last = -1, ans = 0;
        for (int i = 0; i < 32; ++i)
            if (((N >> i) & 1) > 0) {
                if (last >= 0)
                    ans = Math.max(ans, i - last);
                last = i;
            }

        return ans;
    }
}
```