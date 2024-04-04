---
layout: default
title: Prime Number of Set Bits in Binary Representation
parent: Easy Set 4
grand_parent: DSA Easy
nav_order: 28
permalink: /problem-128-Prime-Number-of-Set-Bits-in-Binary-Representation/
---
# Prime Number of Set Bits in Binary Representation

Given two integers left and right, return the count of numbers in the inclusive range [left, right] having a prime number of set bits in their binary representation.

Recall that the number of set bits an integer has is the number of 1's present when written in binary.

For example, 21 written in binary is 10101, which has 3 set bits.

##### Example 1:
```markdown
Input: left = 6, right = 10
Output: 4
Explanation:
6  -> 110 (2 set bits, 2 is prime)
7  -> 111 (3 set bits, 3 is prime)
8  -> 1000 (1 set bit, 1 is not prime)
9  -> 1001 (2 set bits, 2 is prime)
10 -> 1010 (2 set bits, 2 is prime)
4 numbers have a prime number of set bits.
```
##### Example 2:
```markdown
Input: left = 10, right = 15
Output: 5
Explanation:
10 -> 1010 (2 set bits, 2 is prime)
11 -> 1011 (3 set bits, 3 is prime)
12 -> 1100 (2 set bits, 2 is prime)
13 -> 1101 (3 set bits, 3 is prime)
14 -> 1110 (3 set bits, 3 is prime)
15 -> 1111 (4 set bits, 4 is not prime)
5 numbers have a prime number of set bits.
```
##### Constraints:
* 1 <= left <= right <= 106
* 0 <= right - left <= 104

### Solution:
```java
class Solution {
    public int countPrimeSetBits(int left, int right) {
        int count = 0;
        for(int i = left; i<=right; i++){
            int count1s = countBits(i);
            if(count1s>0 && isPrime(count1s)){
              count++;  
            }
        }
        return count;
    }
    
    public int countBits(int k){
        int answer=0;
        while(k!=0){
            answer++;
            k=k&(k-1);
        }
        return answer;
    }
    
    public boolean isPrime(int num){
        if(num == 1) return false;
        if(num == 2 || num == 3) return true;
        for(int i = 2; i<=Math.sqrt(num); i++){
            if(num%i == 0) return false;
        }
        return true;
    }
}
```
```java
class Solution {
    
    public int countPrimeSetBits(int left, int right) {
        int ans=0;
        Integer[]arr=new Integer[]{2,3,5,7,11,13,17,19};
        Set<Integer>set=new HashSet<>(Arrays.asList(arr));
        //System.out.println(set);
        for(int i=left;i<=right;i++){
            int count=count(i);
            if(set.contains(count))ans++;
        }
        return ans;
    }
    
    int count(int x){
        int count=0;
        while(x!=0){
            x-=(x&-x);
            count++;
        }
        return count;
    }
}
```
```java
class Solution {
    public int countPrimeSetBits(int left, int right) {
       int cnt=0;
       for(int i=left;i<=right;i++)
         if(isPrime(Integer.bitCount(i)))
           cnt++;
       return cnt;
    }
    
    public static boolean isPrime(int num)
    {
        if(num<=1)
	      return false;
        
        for(int i=2;(i*i)<=num;i++)
          if((num%i)==0)
            return false;  
	    
        return true; 
    }
}
```
```java
class Solution {
    public int countPrimeSetBits(int left, int right) {
        HashSet<Integer>prime=new HashSet<>();
        prime.add(2);
        prime.add(3);
        prime.add(5);
        prime.add(7);
        prime.add(11);
        prime.add(13);
        prime.add(17);
        prime.add(19);
	    prime.add(23);
        prime.add(29);
        prime.add(31);
        
        int cnt=0;
        for(int i=left;i<=right;i++)
          if(prime.contains(Integer.bitCount(i)))
             cnt++;
        
        return cnt;        
    }
}
```