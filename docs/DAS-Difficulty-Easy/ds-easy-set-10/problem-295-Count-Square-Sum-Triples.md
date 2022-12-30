---
layout: default
title: Count Square Sum Triples
parent: Easy Set 10
grand_parent: DSA Easy Difficulty
nav_order: 15
permalink: /problem-295-Count-Square-Sum-Triples/
---
# Count Square Sum Triples
A square triple (a,b,c) is a triple where a, b, and c are integers and a2 + b2 = c2.

Given an integer n, return the number of square triples such that 1 <= a, b, c <= n.

##### Example 1:
```markdown
Input: n = 5
Output: 2
Explanation: The square triples are (3,4,5) and (4,3,5).
```
##### Example 2:
```markdown
Input: n = 10
Output: 4
Explanation: The square triples are (3,4,5), (4,3,5), (6,8,10), and (8,6,10).
```
##### Constraints:
* 1 <= n <= 250

### Solution:
```java
class Solution {
    public int countTriples(int n) {
        int c = 0;
        for(int i = 1; i <= n; i++){
            for(int j = i + 1; j <= n; j++){
                double s = Math.sqrt(i*i + j*j);
                if(s <= n && s % 1 == 0) c++;
            }
        }
        return 2*c;
    }
}
```