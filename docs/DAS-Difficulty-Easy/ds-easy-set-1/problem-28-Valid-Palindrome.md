---
layout: default
title: Valid Palindrome
parent: Easy Set 1
grand_parent: DSA Easy
nav_order: 28
permalink: /problem-27-Valid-Palindrome/
---
# Valid Palindrome

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

##### Example 1:

```markdown
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

##### Example 2:
```markdown
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

##### Example 3:

```markdown
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

##### Constraints:
* 1 <= s.length <= 2 * 105
* s consists only of printable ASCII characters.

### Solution
```java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuffer sb = new StringBuffer();
        s = s.toLowerCase().trim();
        for(int i=0; i<s.length(); i++){
            if(Character.isLetter(s.charAt(i)) || Character.isDigit(s.charAt(i)))
                sb.append(s.charAt(i));
        }
        String str = sb.toString();
        if(str.equals(" ")) return true;
        return str.equals(sb.reverse().toString());
    }
}
```
