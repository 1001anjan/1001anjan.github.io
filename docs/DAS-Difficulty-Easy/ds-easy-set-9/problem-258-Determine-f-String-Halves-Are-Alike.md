---
layout: default
title: Determine if String Halves Are Alike
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 7
permalink: /problem-257-Determine-if-String-Halves-Are-Alike/
---
# Determine if String Halves Are Alike
You are given a string s of even length. Split this string into two halves of equal lengths, and let a be the first half and b be the second half.

Two strings are alike if they have the same number of vowels ('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'). Notice that s contains uppercase and lowercase letters.

Return true if a and b are alike. Otherwise, return false.

##### Example 1:
```markdown
Input: s = "book"
Output: true
Explanation: a = "bo" and b = "ok". a has 1 vowel and b has 1 vowel. Therefore, they are alike.
```
##### Example 2:
```markdown
Input: s = "textbook"
Output: false
Explanation: a = "text" and b = "book". a has 1 vowel whereas b has 2. Therefore, they are not alike.
Notice that the vowel o is counted twice.
```
##### Constraints:
* 2 <= s.length <= 1000
* s.length is even.
* s consists of uppercase and lowercase letters.

### Solution
```java
class Solution {
    public boolean halvesAreAlike(String s) {
        int c = 0;
        
        for(int i = 0; i < s.length() / 2; i++){
           if(isVowel(s.charAt(i))) c++; 
        }
        
        for(int i = s.length() / 2; i < s.length(); i++){
           if(isVowel(s.charAt(i))) c--; 
        }
        
        return c == 0;
    }
    
    public boolean isVowel(char c){
        if(c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u' 
          || c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U') return true;
        return false;
    }
}
```

#### Faster execution approach
```java
class Solution {
    public boolean halvesAreAlike(String s) {
        String s1 = s.substring(0, s.length() / 2);
        String s2 = s.substring(s.length() / 2);

        return helper(s1) == helper(s2);
    }

    private static int helper(String s) {
        int count = 0;
        for (char c : s.toCharArray()){
            if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u' ||
                    c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U') count++;
        }
        return count;
    }
}
```