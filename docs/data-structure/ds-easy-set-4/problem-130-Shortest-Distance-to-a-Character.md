---
layout: default
title: Shortest Distance to a Character
parent: Data Structure Easy Set 4
grand_parent: Data Structure
nav_order: 30
permalink: /problem-130-Shortest-Distance-to-a-Character/
---
# Shortest Distance to a Character
Given a string s and a character c that occurs in s, return an array of integers answer where answer.length == s.length and answer[i] is the distance from index i to the closest occurrence of character c in s.

The distance between two indices i and j is abs(i - j), where abs is the absolute value function.

##### Example 1:
```markdown
Input: s = "loveleetcode", c = "e"
Output: [3,2,1,0,1,0,0,1,2,2,1,0]
Explanation: The character 'e' appears at indices 3, 5, 6, and 11 (0-indexed).
The closest occurrence of 'e' for index 0 is at index 3, so the distance is abs(0 - 3) = 3.
The closest occurrence of 'e' for index 1 is at index 3, so the distance is abs(1 - 3) = 2.
For index 4, there is a tie between the 'e' at index 3 and the 'e' at index 5, but the distance is still the same: abs(4 - 3) == abs(4 - 5) = 1.
The closest occurrence of 'e' for index 8 is at index 6, so the distance is abs(8 - 6) = 2.
```
##### Example 2:
```markdown
Input: s = "aaab", c = "b"
Output: [3,2,1,0]
```
##### Constraints:
* 1 <= s.length <= 104 
* s[i] and c are lowercase English letters.
* It is guaranteed that c occurs at least once in s.

### Solution:
```java
class Solution {
    public int[] shortestToChar(String s, char c) {
        int[] ans = new int[s.length()];
        int index = Integer.MAX_VALUE;
        // Scan left to right
        for(int i=0; i<s.length(); i++){
            if(s.charAt(i) == c) index = i;
            ans[i] = Math.abs(index - i);
        }
        
        // Scan right to left
        for(int i = s.length()-1; i>=0; i--){
            if(s.charAt(i) == c) index = i;
            ans[i] = Math.min(ans[i], Math.abs(index - i));
        }
        return ans;
    }
}
```
```java
class Solution {
    public int[] shortestToChar(String S, char C) {
      TreeSet<Integer> set = new TreeSet<>();
    
        //add all indexes of C into tree set
      for(int i = 0;i < S.length();i++)  if(S.charAt(i) == C) set.add(i);

        
      int[] result = new int[S.length()];
      for(int i = 0;i < S.length();i++){
          if(!set.contains(i)){
              
              Integer left = set.floor(i);
              Integer right = set.ceiling(i);
              
              if(left == null) left = Integer.MAX_VALUE;
              if (right == null) right = Integer.MAX_VALUE;
              
              result[i] = Math.min(Math.abs(left - i),Math.abs(right -i ));
              
          }else{
            result[i] = 0;  
          }
      }
        return result;
    }
}
```