---
layout: default
title: Palindrome Partitioning
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 13
permalink: /problem-63-Palindrome Partitioning/
---
# Palindrome Partitioning
Given a string s, partition s such that every substring of the partition is a palindrome . Return all possible palindrome partitioning of s.

##### Example 1:
```markdown
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```
##### Example 2:
```markdown
Input: s = "a"
Output: [["a"]]
```
##### Constraints:
* 1 <= s.length <= 16
* s contains only lowercase English letters.

### Solution:
```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> ans = new ArrayList<>();
        processPartition(s, 0, ans, new ArrayList<>());
        return ans;
    }

    public void processPartition(String s, int start, List<List<String>> ans, List<String> list){
        if(start >= s.length() ){
            ans.add(new ArrayList<>(list));
        }
        
        for(int i = start; i < s.length(); i++){
            String str = s.substring(start, i + 1);
            if(isPalindrome(str.toCharArray())){
                list.add(str);
                processPartition(s, i + 1, ans, list);
                list.remove(list.size() - 1);
            }
        }

    }

    public boolean isPalindrome(char[] str){
        int s = 0, e = str.length - 1;

        while(s < e){
            if(str[s++] != str[e--]) return false;
        }
        return true;
    }
}
```