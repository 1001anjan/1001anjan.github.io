---
layout: default
title: Restore IP Addresses
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 3
permalink: /problem-53-Restore IP Addresses/
---
# Restore IP Addresses
A valid IP address consists of exactly four integers separated by single dots. Each integer is between 0 and 255 (inclusive) and cannot have leading zeros.

* For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses, but "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses.
Given a string s containing only digits, return all possible valid IP addresses that can be formed by inserting dots into s. You are not allowed to reorder or remove any digits in s. You may return the valid IP addresses in any order.

##### Example 1:
```markdown
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
```
##### Example 2:
```markdown
Input: s = "0000"
Output: ["0.0.0.0"]
```
##### Example 3:
```markdown
Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```
##### Constraints:
* 1 <= s.length <= 20
* s consists of digits only.

### Solution:
```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> ans = new ArrayList<>();
        processIp(s, 0, 0, ans, new String());
        return ans;
    }

    public void processIp(String s, int start, int count, List<String> ans, String sb){
        if(count > 4) return;
        if(count == 4 && s.length() == start) ans.add(sb);

        for(int i = 1; i < 4; i++){
            if(start + i > s.length()) break;
            String str = s.substring(start, start + i);
            if(str.startsWith("0") && str.length() > 1) continue;
            if(i == 3 && Integer.parseInt(str) > 255) continue;
            processIp(s, start + i, count + 1, ans, sb + str + (count == 3? "" : "."));
        }
    }
}
```
```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> ans = new ArrayList<>();
        processIpAddress(s, 0, new String(), s.length(), 0, ans);
        return ans;
    }

    private void processIpAddress(String s, int start, String sb, int len, int dotCount, List<String> ans){
        if(dotCount > 4) return;
        if(dotCount == 4 && start == len){
            ans.add(sb);
            return;
        }
        for(int i = 1; i < 4; i++){
            if(start + i > len) break;
            String str = s.substring(start, start + i);
            if(str.startsWith("0") && i > 1) continue;
            if(i == 3 && Integer.parseInt(str) > 255) continue;
            if(dotCount < 3) str = str + ".";
            processIpAddress(s, start + i, sb + str, len, dotCount + 1, ans);
        }
    }   
}
```