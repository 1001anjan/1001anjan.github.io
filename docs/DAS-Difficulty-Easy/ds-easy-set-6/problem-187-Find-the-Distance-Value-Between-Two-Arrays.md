---
layout: default
title: Find the Distance Value Between Two Arrays
parent: Easy Set 6
grand_parent: DSA Easy Difficulty
nav_order: 27
permalink: /problem-187-Find-the-Distance-Value-Between-Two-Arrays/
---
# Find the Distance Value Between Two Arrays
Given two integer arrays arr1 and arr2, and the integer d, return the distance value between the two arrays.

The distance value is defined as the number of elements arr1[i] such that there is not any element arr2[j] where |arr1[i]-arr2[j]| <= d.

##### Example 1:
```markdown
Input: arr1 = [4,5,8], arr2 = [10,9,1,8], d = 2
Output: 2
Explanation:
For arr1[0]=4 we have:
|4-10|=6 > d=2
|4-9|=5 > d=2
|4-1|=3 > d=2
|4-8|=4 > d=2
For arr1[1]=5 we have:
|5-10|=5 > d=2
|5-9|=4 > d=2
|5-1|=4 > d=2
|5-8|=3 > d=2
For arr1[2]=8 we have:
|8-10|=2 <= d=2
|8-9|=1 <= d=2
|8-1|=7 > d=2
|8-8|=0 <= d=2
```
##### Example 2:
```markdown
Input: arr1 = [1,4,2,3], arr2 = [-4,-3,6,10,20,30], d = 3
Output: 2
```
##### Example 3:
```markdown
Input: arr1 = [2,1,100,3], arr2 = [-5,-2,10,-3,7], d = 6
Output: 1
```
##### Constraints:
* 1 <= arr1.length, arr2.length <= 500
* -1000 <= arr1[i], arr2[j] <= 1000
* 0 <= d <= 100

### Solution:
```java
class Solution {
   
    public int findTheDistanceValue(int[] arr1, int[] arr2, int d) {
        Arrays.sort(arr2);
        int count = 0;
        for(int i=0;i<arr1.length;i++) 
            if(distance(arr2, arr1[i], d)) 
                count++;
        return count;  
    }

    public boolean distance(int [] arr, int k, int d)
    {
        int start = 0, last = arr.length-1;
        while(start<=last)
        {
            int mid = start + (last - start)/2;
            int diff = Math.abs(arr[mid] - k);
            if(diff <= d)
                return false;
            else if(arr[mid] > k)
                last = mid - 1;
            else
                start = mid + 1;
        }
        return true;
    }
}
```