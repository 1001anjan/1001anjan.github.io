---
layout: default
title: Number of Segments in a String
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 15
permalink: /problem-78-Number-of-Segments-in-a-String/
---
# Number of Segments in a String

Given a string s, return the number of segments in the string.

A segment is defined to be a contiguous sequence of non-space characters.

##### Example 1:
````markdown
Input: s = "Hello, my name is John"
Output: 5
Explanation: The five segments are ["Hello,", "my", "name", "is", "John"]
````
##### Example 2:

```markdown
Input: s = "Hello"
Output: 1
```
##### Constraints:
* 0 <= s.length <= 300
* s consists of lowercase and uppercase English letters, digits, or one of the following characters "!@#$%^&*()_+-=',.:".
* The only space character in s is ' '.

### Solution
```java
class Solution {
    public int countSegments(String s) {
        if(s.length() == 0) return 0;
        String[] ar =  s.split(" ");
        int len = ar.length;
        for(String st : ar){
            if(st.length() == 0)
                len--;
        }
        return len;
    }
}
```