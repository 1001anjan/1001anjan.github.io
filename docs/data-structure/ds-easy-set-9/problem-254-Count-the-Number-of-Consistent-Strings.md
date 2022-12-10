---
layout: default
title: Count the Number of Consistent Strings
parent: Data Structure Easy Set 9
grand_parent: Data Structure
nav_order: 4
permalink: /problem-254-Count-the-Number-of-Consistent-Strings/
---
# Count the Number of Consistent Strings
You are given a string allowed consisting of distinct characters and an array of strings words. A string is consistent if all characters in the string appear in the string allowed.

Return the number of consistent strings in the array words.

##### Example 1:
```markdown
Input: allowed = "ab", words = ["ad","bd","aaab","baa","badab"]
Output: 2
Explanation: Strings "aaab" and "baa" are consistent since they only contain characters 'a' and 'b'.
```
##### Example 2:
```markdown
Input: allowed = "abc", words = ["a","b","c","ab","ac","bc","abc"]
Output: 7
Explanation: All strings are consistent.
```
##### Example 3:
```markdown
Input: allowed = "cad", words = ["cc","acd","b","ba","bac","bad","ac","d"]
Output: 4
Explanation: Strings "cc", "acd", "ac", and "d" are consistent.
```
##### Constraints:
* 1 <= words.length <= 104
* 1 <= allowed.length <= 26
* 1 <= words[i].length <= 10
* The characters in allowed are distinct.
* words[i] and allowed contain only lowercase English letters.

### Solution:
```java
class Solution {
    public int countConsistentStrings(String allowed, String[] words) {
        boolean[] a = new boolean[26];
        for(char c : allowed.toCharArray()) a[c - 'a'] = true;
        
        int count = 0;
        for(String str : words){
            boolean f = true;
            for(char c : str.toCharArray()){
                if(!a[c - 'a']){
                    f = false;
                    break;
                }
            }
            if(f) count++;
        }
        return count;
    }
}
```
```java
class Solution {
	public int countConsistentStrings(String allowed, String[] words) {
    int mask =0;
    
    for (int i =0; i<allowed.length(); i++) {
        mask |= 1 << (allowed.charAt(i) - 'a');
    }
    
    int count = 0; 
    
    outer:
    for (int i =0; i< words.length; i++)  {
        for (int j = 0; j<words[i].length(); j++)   {
            if ((mask & (1 << words[i].charAt(j) - 'a')) == 0)
                continue outer;
        }
        
        count ++;
    }
    
    return count; 
}
}
```