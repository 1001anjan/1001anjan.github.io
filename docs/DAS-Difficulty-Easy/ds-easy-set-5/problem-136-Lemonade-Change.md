---
layout: default
title: Lemonade Change
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 6
permalink: /problem-136-Lemonade-Change/
---
# Lemonade Change
At a lemonade stand, each lemonade costs $5. Customers are standing in a queue to buy from you and order one at a time (in the order specified by bills). Each customer will only buy one lemonade and pay with either a $5, $10, or $20 bill. You must provide the correct change to each customer so that the net transaction is that the customer pays $5.

Note that you do not have any change in hand at first.

Given an integer array bills where bills[i] is the bill the ith customer pays, return true if you can provide every customer with the correct change, or false otherwise.

##### Example 1:
```markdown
Input: bills = [5,5,5,10,20]
Output: true
Explanation:
From the first 3 customers, we collect three $5 bills in order.
From the fourth customer, we collect a $10 bill and give back a $5.
From the fifth customer, we give a $10 bill and a $5 bill.
Since all customers got correct change, we output true.
```
##### Example 2:
```markdown
Input: bills = [5,5,10,10,20]
Output: false
Explanation:
From the first two customers in order, we collect two $5 bills.
For the next two customers in order, we collect a $10 bill and give back a $5 bill.
For the last customer, we can not give the change of $15 back because we only have two $10 bills.
Since not every customer received the correct change, the answer is false.
```
##### Constraints:
* 1 <= bills.length <= 105
* bills[i] is either 5, 10, or 20.

### Solution:
```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int count5 = 0;
        int count10 = 0;
        int count20 = 0;
        
        for(int i=0; i<bills.length; i++){
            if(bills[i] == 5) {
                count5++;
            }else if(bills[i] == 10){
                if(count5 == 0) return false;
                count5--;
                count10++;
            }else if(bills[i] == 20){
                if(count5 == 0) return false;
                if(count10>=1){
                    count10--;
                    count5--;
                }else{
                    if(count5>=3) count5 = count5 - 3;
                    else return false;
                }
            }
        }
        return true;
    }
}
```