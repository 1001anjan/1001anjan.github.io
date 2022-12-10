---
layout: default
title: Number of Different Integers in a String
parent: Data Structure Easy Set 9
grand_parent: Data Structure
nav_order: 25
permalink: /problem-275-Number-of-Different-Integers-in-a-String/
---
# Number of Different Integers in a String
You are given a string word that consists of digits and lowercase English letters.

You will replace every non-digit character with a space. For example, "a123bc34d8ef34" will become " 123  34 8  34". Notice that you are left with some integers that are separated by at least one space: "123", "34", "8", and "34".

Return the number of different integers after performing the replacement operations on word.

Two integers are considered different if their decimal representations without any leading zeros are different.

##### Example 1:
```markdown
Input: word = "a123bc34d8ef34"
Output: 3
Explanation: The three different integers are "123", "34", and "8". Notice that "34" is only counted once.
```
##### Example 2:
```markdown
Input: word = "leet1234code234"
Output: 2
```
###### Example 3:
```markdown
Input: word = "a1b01c001"
Output: 1
Explanation: The three integers "1", "01", and "001" all represent the same integer because
the leading zeros are ignored when comparing their decimal values.
```
###### Constraints:
* 1 <= word.length <= 1000
* word consists of digits and lowercase English letters.

### Solution:
```java
class Solution {
    public int numDifferentIntegers(String word) {
        Set<String> s = new HashSet<>();
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < word.length(); i++){
            char c = word.charAt(i);
            if(!Character.isLetter(c)){
                sb.append(c);
            }else{
                if(sb.length() != 0) s.add(filterString(sb));
                sb.setLength(0);
            }
        }

        if(sb.length() != 0) s.add(filterString(sb));
        return s.size();
    }

    public String filterString(StringBuilder str){
        if(str.charAt(0) != '0') return str.toString();
        int i = 0;
        int n = str.length();
        while(i < n && str.charAt(i) == '0') i++;
        if(i == n) return "0";
        return str.substring(i,n).toString();
    }
}
```