---
layout: default
title: Longest Common Prefix
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 4
---
# Longest Common Prefix
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".



### Example 1:
```markdown
Input: strs = ["flower","flow","flight"]
Output: "fl"
```
### Example 2:
```markdown
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

### Constraints:

* 1 <= strs.length <= 200
* 0 <= strs[i].length <= 200
* strs[i] consists of only lowercase English letters.

### Solution:
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
       if(strs == null  || strs.length ==0) return "";
        String str= strs[0];
        int i;
        for(i=0;  i<str.length(); i++){
            for(int  j=0;j<strs.length; j++){
                if(strs[j].length()<=i) return str.substring(0,i);
                if(strs[j].charAt(i) != str.charAt(i))  return str.substring(0,i);
            }
        }
        if(i==0) return "";
        return strs[0];
    }
}
```

### Complexity Analysis

Time complexity : O(S) , where S is the sum of all characters in all strings. In the worst case there will be nn equal strings with length m and the algorithm performs S = m \cdot nS=m⋅n character comparisons. Even though the worst case is still the same as Approach 1, in the best case there are at most n \cdot minLenn⋅minLen comparisons where minLenminLen is the length of the shortest string in the array.
Space complexity : O(1). We only used constant extra space.

#### Solution: Divide and Conquer 
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
       if(strs == null  || strs.length ==0) return "";
       return longestCommonPrefix(strs,0, strs.length-1);
    }
    
    private String longestCommonPrefix(String[] strs, int l, int u){
        if(l == u ) return strs[l];
        
        int mid = (l+u)/2;
        String left = longestCommonPrefix(strs, l, mid);
        String right = longestCommonPrefix(strs, mid+1, u);
        return commonPrefix(left, right);
    }
    
    private String commonPrefix(String left, String right){
        int min = Math.min(left.length(), right.length());
        for(int i=0; i<min; i++){
            if(left.charAt(i) != right.charAt(i)) return left.substring(0, i);
        }
        return left.substring(0,min);
    }
}
```

### Complexity Analysis

In the worst case we have nn equal strings with length m

* Time complexity : O(S), where S is the number of all characters in the array, S = m \cdot nS=m⋅n Time complexity is 2 \cdot T\left ( \frac{n}{2} \right ) + O(m)2⋅T(2
n
)+O(m). Therefore time complexity is O(S)O(S). In the best case this algorithm performs O(minLen \cdot n)O(minLen⋅n) comparisons, where minLenminLen is the shortest string of the array

* Space complexity : O(m \cdot \log n)O(m⋅logn)

There is a memory overhead since we store recursive calls in the execution stack. There are \log nlogn recursive calls, each store need mm space to store the result, so space complexity is O(m \cdot \log n)O(m⋅logn)



