---
layout: default
title: Rank Transform of an Array
parent: Easy Set 7
grand_parent: DSA Easy Difficulty
nav_order: 9
permalink: /problem-199-Rank-Transform-of-an-Array/
---
# Rank Transform of an Array

Given an array of integers arr, replace each element with its rank.

The rank represents how large the element is. The rank has the following rules:

Rank is an integer starting from 1.
The larger the element, the larger the rank. If two elements are equal, their rank must be the same.
Rank should be as small as possible.

##### Example 1:
```markdown
Input: arr = [40,10,20,30]
Output: [4,1,2,3]
Explanation: 40 is the largest element. 10 is the smallest. 20 is the second smallest. 30 is the third smallest.
```

##### Example 2:
```markdown
Input: arr = [100,100,100]
Output: [1,1,1]
Explanation: Same elements share the same rank.
```

##### Example 3:
```markdown
Input: arr = [37,12,28,9,100,56,80,5,12]
Output: [5,3,4,2,8,6,7,1,3]
```

##### Constraints:
* 0 <= arr.length <= 105
* -109 <= arr[i] <= 109

### Solution:

```java
class Solution {
    public int[] arrayRankTransform(int[] arr) {
        Set<Integer> s = new HashSet<>();
        
        for(int n : arr) s.add(n);
        Integer[] temp = new Integer[s.size()];
        s.toArray(temp);
        Arrays.sort(temp);
        
        for(int j = 0; j<arr.length; j++){
            arr[j] = binarySearch(temp,arr[j]) + 1;
        }
        return arr;
    }
    
    public int binarySearch(Integer[] arr, int v){
        int s = 0;
        int e = arr.length - 1;
        while(s<=e){
            int mid = (e+s)/2;
            if(arr[mid] == v) return mid;
            if(arr[mid]>v) 
                e = mid - 1;
            else
                s = mid + 1;
        }
        return -1;
    }
}
```
#### Same Time Complexity but faster
```java
class Solution {
    public int[] arrayRankTransform(int[] arr) {
        
        int[]res=new int[arr.length];
        
        for(int i=0;i<arr.length;i++){
            res[i]=arr[i];
        }
        
        Arrays.sort(arr);
        
        HashMap<Integer,Integer>h1=new HashMap();
        int x=0;
        for(int i=0;i<arr.length;i++){
            if(!h1.containsKey(arr[i])){
                x++;
            h1.put(arr[i],x);
            }
        }
        
        int ans[]=new int[arr.length];
        
        for(int i=0;i<arr.length;i++){
            ans[i]=h1.get(res[i]);
        }
        return ans;
    }
}
```