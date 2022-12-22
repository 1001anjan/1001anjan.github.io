---
layout: default
title: H-Index II
parent: Data Structure Medium Set 3
grand_parent: Data Structure
nav_order: 15
permalink: /problem-115-H-Index II/
---
# H-Index II
Given an array of integers citations where citations[i] is the number of citations a researcher received for their ith paper and citations is sorted in an ascending order, return compute the researcher's h-index.

According to the definition of h-index on Wikipedia: A scientist has an index h if h of their n papers have at least h citations each, and the other n − h papers have no more than h citations each.

If there are several possible values for h, the maximum one is taken as the h-index.

You must write an algorithm that runs in logarithmic time.

##### Example 1:
```markdown
Input: citations = [0,1,3,5,6]
Output: 3
Explanation: [0,1,3,5,6] means the researcher has 5 papers in total and each of them had received 0, 1, 3, 5, 6 citations respectively.
Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, their h-index is 3.
```
##### Example 2:
```markdown
Input: citations = [1,2,100]
Output: 2
```
##### Constraints:
* n == citations.length
* 1 <= n <= 10^5
* 0 <= citations[i] <= 1000
* citations is sorted in ascending order.

### Solution:
```java
class Solution {
    public int hIndex(int[] citations) {
        int len = citations.length;
        int s = 0;
        int e = len - 1;
        while(s <= e){
            int mid = (s + e)/2;
            if(citations[mid] >= len - mid){
                e = mid - 1;
            }else{
                s = mid + 1;
            }
        }
        return len - s;
    }
}
```