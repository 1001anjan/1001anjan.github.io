---
layout: default
title: Relative Sort Array
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 18
permalink: /problem-178-Relative-Sort-Array/
---
# Relative Sort Array

Given two arrays arr1 and arr2, the elements of arr2 are distinct, and all elements in arr2 are also in arr1.

Sort the elements of arr1 such that the relative ordering of items in arr1 are the same as in arr2. Elements that do not appear in arr2 should be placed at the end of arr1 in ascending order.

##### Example 1:
```markdown
Input: arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
Output: [2,2,2,1,4,3,3,9,6,7,19]
```
##### Example 2:
```markdown
Input: arr1 = [28,6,22,8,44,17], arr2 = [22,28,8,6]
Output: [22,28,8,6,17,44]
```
##### Constraints:
* 1 <= arr1.length, arr2.length <= 1000
* 0 <= arr1[i], arr2[i] <= 1000
* All the elements of arr2 are distinct.
* Each arr2[i] is in arr1.

### Solution:
```java
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        Set<Integer> s = new HashSet<Integer>();
        int[] ans = new int[arr1.length];
        
        Map<Integer,Integer> m = new HashMap<>();
        for(int n : arr1) m.put(n,m.getOrDefault(n,0)+1);
        
        int i = 0;
        for(int n : arr2){
            s.add(n);
            for(int j = 1; j<= m.get(n); j++)
                ans[i++] = n;
        }
        
        Arrays.sort(arr1);
        for(int n : arr1){
            if(!s.contains(n)) ans[i++] = n;
        }
        
        return ans;
    }
}
```
#### Time-complexity O(n)
```java
class Solution{
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int j=0;
        int[] freq=new int[100000];
        int[] ans=new int[arr1.length];
        
        for(int i:arr1){
            freq[i]++;
        }
        
        for(int i:arr2){
            while(freq[i]!=0){
                ans[j++]=i;
                freq[i]--;
            }
            
        }
        
        for(int i=0;i<freq.length;i++){
            while(freq[i]!=0){
                ans[j++]=i;
                freq[i]--;
            }
        }
        return ans;
        
    }
}

```