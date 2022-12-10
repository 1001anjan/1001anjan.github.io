---
layout: default
title: Finding 3-Digit Even Numbers
parent: Data Structure Easy Set 11
grand_parent: Data Structure
nav_order: 14
permalink: /problem-324-Finding 3-Digit Even Numbers/
---
# Finding 3-Digit Even Numbers
You are given an integer array digits, where each element is a digit. The array may contain duplicates.

You need to find all the unique integers that follow the given requirements:

* The integer consists of the concatenation of three elements from digits in any arbitrary order.
* The integer does not have leading zeros.
* The integer is even.
For example, if the given digits were [1, 2, 3], integers 132 and 312 follow the requirements.

Return a sorted array of the unique integers.

##### Example 1:
```markdown
Input: digits = [2,1,3,0]
Output: [102,120,130,132,210,230,302,310,312,320]
Explanation: All the possible integers that follow the requirements are in the output array.
Notice that there are no odd integers or integers with leading zeros.
```
##### Example 2:
```markdown
Input: digits = [2,2,8,8,2]
Output: [222,228,282,288,822,828,882]
Explanation: The same digit can be used as many times as it appears in digits.
In this example, the digit 8 is used twice each time in 288, 828, and 882.
```
##### Example 3:
```markdown
Input: digits = [3,7,5]
Output: []
Explanation: No even integers can be formed using the given digits.
```
##### Constraints:
* 3 <= digits.length <= 100
* 0 <= digits[i] <= 9

### Solution:
```java
class Solution {
	public int[] findEvenNumbers(int[] digits) {
		int[] digitsCount = new int[10];
		for(int i : digits) digitsCount[i]++;

		List<Integer> list = new ArrayList<>();

		for(int i=100; i<=998; i=i+2) {
			if(checkNum(i, digitsCount)) list.add(i);
		} 
		return list.stream().mapToInt(x -> x).toArray();
	}

	public boolean checkNum(int num, int[] digitsCount) {
		int[] numCount = new int[10];

		while(num != 0) {
			numCount[num%10]++;
			num/=10;
		}

		for(int i=0; i<10; i++)
			if(numCount[i] > digitsCount[i]) return false;
		return true;
	}
}
```
