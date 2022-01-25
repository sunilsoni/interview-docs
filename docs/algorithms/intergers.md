---
layout: default
title: Intergers
parent: Data Structures

---

# Intergers
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>


---

## Palindrome Number

An integer is a palindrome when it reads the same backward as forward.

For example, 121 is a palindrome while 123 is not.

###  Problem Statement

Given an integer x, return true if x is palindrome integer.

1. **Example 1**
 Input: x = 121
 Output: true

2. **Example 2**
 Input: x = -121
 Output: false

3. **Example 3**
 Input: x = 10
 Output: false

###  Solution 1
Lets understand the problem statement first. In this problem we are given an integer value as input, our task is to write an algorithm that tells us whether the given number is a palindrome or not. So, what are palindromic numbers? A number is a palindrome if it remains same when its digits are reversed. In other words a number is a palindrome if we get the same sequence of digits whether we read the number from left to right or right to left. For example 121, 99, 2332 etc. are palindromic numbers.

The idea is to do the steps mentioned here to reverse the given number only up to the middle digit in x and then compare x with the reversedNum. Basically what we do here is reverse only half of the given number x and compare x with reversed number.

This algorithm involves the following steps:

1. Reverse half of the digits of the given number x. (Reversing is done using same steps described in solution 1).
2. Once half of the digits in x are reversed, reversedNum will contain the reversed second half of the original input number and x (modified) will contain the first half of the original input number. For example if the given input is x = 123321, then after reversing half of the digits, reversedNum will be 123 and modified x will be 123.
3. Now compare the modified x with the reversedNum.
4. If both x and reversedNum are equal then return true as result, otherwise return false.


Let take one more example to understand this. Consider x = 1221 is the given number, our algorithm reverses the last two digits in x i.e. 21 (until middle digit). So, at the end of our loop x = 12 and reversedNum = 12. Now compare (x, reversedNum) and return the result.

**Note**: If x contains odd number of digits as in x = 12321, at the end of our loop reversedNum = 123 and x = 12. So we need to divide reversedNum by 10 if x contains odd number of digits before comparing x and reversedNum.

###  Implementation

```java
class PalindromeSolution {
 public boolean isPalindrome(int x) {
  // If x is a negative number it is not a palindrome
  // If x % 10 = 0, in order for it to be a palindrome the first digit should also be 0
  if (x < 0 || (x != 0 && x % 10 == 0))
    return false;
  int res = 0;
  while (x > res) {
     res = res * 10 + x % 10;
    x = x / 10;
  }
  // If x is equal to reversed number then it is a palindrome
  // If x has odd number of digits, dicard the middle digit before comparing with x
  // Example, if x = 23132, at the end of for loop x = 23 and reversedNum = 231
  // So, reversedNum/10 = 23, which is equal to x
  return (x == res || x == res / 10);
 }
}
```

###  Complexity Analysis

**Time Complexity**: O(d/2)
d here is the no. of digits in the given input number. Time complexity of this algorithm is O(d/2) because we only have to check half of the digits in the given number x (last to middle) to determine if the given number is a palindrome.

**Space Complexity**: O(1)
No extra space is used.

###  Solution 2

###  Implementation

###  Complexity Analysis



---

## Fizz Buzz

Given an integer n, return a string array answer (1-indexed) where:

- answer[i] == "FizzBuzz" if i is divisible by 3 and 5.
- answer[i] == "Fizz" if i is divisible by 3.
- answer[i] == "Buzz" if i is divisible by 5.
- answer[i] == i (as a string) if none of the above conditions are true.

**Example:**

Input: n = 15
Output: ["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]


###  Solution 



###  Implementation
```java
class FizzBuzzSolution {
    public List<String> fizzBuzz(int n) {
        List<String> ls = new ArrayList<String>();
        for (int i = 1; i <= n; i++) {
            if (i%3 == 0 && i%5 == 0) ls.add("FizzBuzz");
            else if (i%3 == 0) ls.add("Fizz");
            else if (i%5 == 0) ls.add("Buzz");
            else ls.add(Integer.toString(i));
        }
        return ls;
    }
}
```

###  Complexity Analysis

**Time Complexity**: O(n) 1ms time taken.

**Space Complexity**: O(n)




---

## More Details: 
1. [Palindrome Number - Leetcode #9 Short & Simple Solution](https://www.code-recipe.com/post/palindrome-number)


