---
layout: default
title: Next Greater Element I
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 25
permalink: /problem-88-Next-Greater-Element-I/
---
# Next Greater Element I
The next greater element of some element x in an array is the first greater element that is to the right of x in the same array.

You are given two distinct 0-indexed integer arrays nums1 and nums2, where nums1 is a subset of nums2.

For each 0 <= i < nums1.length, find the index j such that nums1[i] == nums2[j] and determine the next greater element of nums2[j] in nums2. If there is no next greater element, then the answer for this query is -1.

Return an array ans of length nums1.length such that ans[i] is the next greater element as described above.

##### Example 1:
```markdown
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
```

##### Example 2:
```markdown
Input: nums1 = [2,4], nums2 = [1,2,3,4]
Output: [3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,2,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,4]. There is no next greater element, so the answer is -1.
```

##### Constraints:

* 1 <= nums1.length <= nums2.length <= 1000
* 0 <= nums1[i], nums2[i] <= 104
* All integers in nums1 and nums2 are unique.
* All the integers of nums1 also appear in nums2.

Follow up: Could you find an O(nums1.length + nums2.length) solution?

### Solution:
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int[] ans = new int[nums1.length];
        boolean f = false;
        for(int i = 0; i<nums1.length; i++){
            f = false;
            for(int j = 0; j<nums2.length; j++){
                if(nums1[i] == nums2[j]){
                    for(int k = j+1; k<nums2.length; k++){
                        if(nums2[k] > nums2[j]){
                            ans[i] = nums2[k];
                            f = true;
                            break;
                        }
                        if(k == nums2.length) {
                            ans[i] = -1;
                        }
                    }
                    if(f) break;
                    else
                    ans[i] = -1; 
                }
            }
        }
        return ans;
    }
}
```
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        int resGreater[]=new int[nums2.length-1];
        resGreater=nextGreaterElementRight(nums2);
        HashMap<Integer,Integer> hm=new HashMap<Integer,Integer>();
        for(int i=0;i<nums2.length;i++){
            hm.put(nums2[i],resGreater[i]);
        }
        int result[]=new int[nums1.length];
        for(int i=0;i<nums1.length;i++){
            result[i]=hm.get(nums1[i]);
        }
        return result;
        
    }
    
    public int[] nextGreaterElementRight(int[] nums1){
        
        int res[]=new int[nums1.length];
        Stack<Integer> st=new Stack<Integer>();
        st.push(nums1[nums1.length-1]);
        res[nums1.length-1]=-1;
        
        for(int i=nums1.length-2;i>=0;i--){
            int res1=0;
            while(!st.isEmpty()&&nums1[i]>st.peek()){
                st.pop();
            }
            if(!st.isEmpty()&&nums1[i]<st.peek()){
                res1=st.peek();
                res[i]=res1;
                st.push(nums1[i]);
            }
            else if(st.isEmpty()){
                res[i]=-1;
                st.push(nums1[i]);
            }
        }
        
        return res;
        
    }
}
```