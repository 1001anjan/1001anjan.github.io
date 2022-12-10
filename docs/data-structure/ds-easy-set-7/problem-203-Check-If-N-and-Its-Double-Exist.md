---
layout: default
title: Check If N and Its Double Exist
parent: Data Structure Easy Set 7
grand_parent: Data Structure
nav_order: 13
permalink: /problem-203-Check-If-N-and-Its-Double-Exist/
---
# Check If N and Its Double Exist

Given an array arr of integers, check if there exists two integers N and M such that N is the double of M ( i.e. N = 2 * M).

More formally check if there exists two indices i and j such that :
* i != j
* 0 <= i, j < arr.length
* arr[i] == 2 * arr[j]

##### Example 1:
```markdown
Input: arr = [10,2,5,3]
Output: true
Explanation: N = 10 is the double of M = 5,that is, 10 = 2 * 5.
```

##### Example 2:
```markdown
Input: arr = [7,1,14,11]
Output: true
Explanation: N = 14 is the double of M = 7,that is, 14 = 2 * 7.
```

##### Example 3:
```markdown
Input: arr = [3,1,7,11]
Output: false
Explanation: In this case does not exist N and M, such that N = 2 * M.
```

##### Constraints:
* 2 <= arr.length <= 500
* -10^3 <= arr[i] <= 10^3

### Solution:
#### Time Complexity O(nLogN) Space: O(1);
```java
class Solution {
    public boolean checkIfExist(int[] arr) {
        Arrays.sort(arr);
        for(int i = 0; i<arr.length; i++){
            if(binarySearch(arr, arr[i]*2, i)) return true;
        }
        return false;
    }
    
    public boolean binarySearch(int[] arr, int val, int index){
        int s = 0;
        int e = arr.length - 1;
        while(s <= e){
            int mid = (s + e)/2;
            if(arr[mid] == val && index != mid) return true;
            if(arr[mid] > val)
                e = mid - 1;
            else
                s = mid + 1;
        }
        return false;
    }
}
```

#### time Complexity: O(n) Space: O(n)
```java
class Solution {
    public boolean checkIfExist(int[] arr) {
        HashMap<Double,Integer> map = new HashMap<>();
        for(int i:arr)
        {
            double temp = i;
            if(map.containsKey(temp*2))
                return true;
            else if(map.containsKey(temp/2))
                return true;
            map.put(temp,1);
        }
        return false;
    }
}
```