---
layout: default
title: Defanging an IP Address
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 20
permalink: /problem-180-Defanging-an-IP-Address/
---
# Defanging an IP Address

Given a valid (IPv4) IP address, return a defanged version of that IP address.

A defanged IP address replaces every period "." with "[.]".

##### Example 1:
```markdown
Input: address = "1.1.1.1"
Output: "1[.]1[.]1[.]1"
```
##### Example 2:
```markdown
Input: address = "255.100.50.0"
Output: "255[.]100[.]50[.]0"
```
##### Constraints:
* The given address is a valid IPv4 address.

### Solution:
```java
class Solution {
    public String defangIPaddr(String address) {
        StringBuilder sb = new StringBuilder();
        for(char c : address.toCharArray()){
            if(c == '.') sb.append("[.]");
            else
                sb.append(String.valueOf(c));
        }
        return sb.toString();
    }
}
```