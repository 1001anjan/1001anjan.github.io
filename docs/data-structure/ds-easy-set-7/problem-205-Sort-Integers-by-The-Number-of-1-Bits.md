---
layout: default
title: Sort Integers by The Number of 1 Bits
parent: Data Structure Easy Set 7
grand_parent: Data Structure
nav_order: 15
permalink: /problem-205-Sort-Integers-by-The-Number-of-1-Bits/
---
# Sort Integers by The Number of 1 Bits

You are given an integer array arr. Sort the integers in the array in ascending order by the number of 1's in their binary representation and in case of two or more integers have the same number of 1's you have to sort them in ascending order.

Return the array after sorting it.

##### Example 1:
```markdown
Input: arr = [0,1,2,3,4,5,6,7,8]
Output: [0,1,2,4,8,3,5,6,7]
Explantion: [0] is the only integer with 0 bits.
[1,2,4,8] all have 1 bit.
[3,5,6] have 2 bits.
[7] has 3 bits.
The sorted array by bits is [0,1,2,4,8,3,5,6,7]
```

##### Example 2:
```markdown
Input: arr = [1024,512,256,128,64,32,16,8,4,2,1]
Output: [1,2,4,8,16,32,64,128,256,512,1024]
Explantion: All integers have 1 bit in the binary representation, you should just sort them in ascending order.
```

##### Constraints:
* 1 <= arr.length <= 500
* 0 <= arr[i] <= 104

### Solution:
```java
class Solution {
    public int[] sortByBits(int[] arr) {
        int[][] map = new int[arr.length][2];
        for(int i = 0; i < arr.length; i++){
            map[i][0] = arr[i];
            map[i][1] = countBinaryOne(arr[i]);
        }
        
        Arrays.sort(map, (a,b) -> {
            if(a[1] == b[1]) return a[0] - b[0];
            return a[1] - b[1];
        });
        
        for(int i = 0; i < arr.length; i++){
            arr[i] = map[i][0];
        }
        
        return arr;
    }
    
    public int countBinaryOne(int n){
        int count = 0;
        while(n>0){
            if((n & 1) == 1) count++;
            n = n >> 1;
        }
        return count;
    }
}
```
#### Same time complexity but constant memory and faster execution time 
```java
class Solution {
    public int[] sortByBits(int[] arr) {
        for ( int i =0 ;i< arr.length ;i++){
            arr[i] += Integer.bitCount(arr[i])*10001;
        }
        Arrays.sort(arr);
         for ( int i =0 ;i< arr.length ;i++){
             arr[i] = arr[i] %10001;
         }
        return arr;
    }
}

```