---
layout: default
title: Intergers
parent: Data Structures
resource: true
desc: "Intergers interview questions and answers."
categories: [Intergers]

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

####  Implementation

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

####  Complexity Analysis

**Time Complexity**: O(d/2)
d here is the no. of digits in the given input number. Time complexity of this algorithm is O(d/2) because we only have to check half of the digits in the given number x (last to middle) to determine if the given number is a palindrome.

**Space Complexity**: O(1)
No extra space is used.


###  Solution 2

####  Implementation

####  Complexity Analysis



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

## Prime Numbers

A prime number is a natural number greater than one that has no positive divisors other than one and itself.

For example, 7 is prime because 1 and 7 are its only positive integer factors, whereas 12 is not because it has the divisors 3 and 2 in addition to 1, 4 and 6.

###  Generating Prime Numbers

The method checks each numbers divisibility by the numbers in a range from 2 till number-1.

If at any point we encounter a number that is divisible, we return false. At the end when we find that number is not divisible by any of its prior number, we return true indicating its a prime number.

####  Implementation

```java
class Solution {
 public static List<Integer> primeNumbersBruteForce(int n) {
  List<Integer> primeNumbers = new LinkedList<>();
  for (int i = 2; i <= n; i++) {
   if (isPrimeBruteForce(i)) {
    primeNumbers.add(i);
   }
  }
  return primeNumbers;
 }
 public static boolean isPrimeBruteForce(int number) {
  for (int i = 2; i < number; i++) {
   if (number % i == 0) {
    return false;
   }
  }
  return true;
 }    
}

```



####  Complexity Analysis

**Time Complexity**:
O(n^2)
**Space Complexity**:
O(n)

###  Efficiency and Optimization

When a number is not a prime, this number can be factored into two factors namely a and b i.e. number = a * b. If both a and b were greater than the square root of n, a*b would be greater than n.

So at least one of those factors must be less than or equal the square root of a number and to check if a number is prime, we only need to test for factors lower than or equal to the square root of the number being checked.

Additionally, prime numbers can never be an even number as even numbers are all divisible by 2.

Keeping in mind above ideas, let's improve the algorithm:

####  Implementation

```java
 class Solution {
 public static List<Integer> primeNumbersBruteForce(int n) {
  List<Integer> primeNumbers = new LinkedList<>();
  if (n >= 2) {
   primeNumbers.add(2);
  }
  for (int i = 3; i <= n; i += 2) {
   if (isPrimeBruteForce(i)) {
    primeNumbers.add(i);
   }
  }
  return primeNumbers;
 }
 private static boolean isPrimeBruteForce(int number) {
  for (int i = 2; i*i <= number; i++) {
   if (number % i == 0) {
    return false;
   }
  }
  return true;
 }
 }
```


###  Using Java 8
```java
 class Solution {
 public static List<Integer> primeNumbersTill(int n) {
  return IntStream.rangeClosed(2, n)
          .filter(x -> isPrime(x)).boxed()
          .collect(Collectors.toList());
 }
 private static boolean isPrime(int number) {
  return IntStream.rangeClosed(2, (int) (Math.sqrt(number)))
          .allMatch(n -> x % n != 0);
 }
}
```


---

## Add Two Numbers

[Leetcode URL](https://leetcode.com/problems/add-two-numbers/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

<img src="images/integer/addTwoNumbers.png" width="900" />

```log
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:**

```log
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:**

```log
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

### Solution 1: Elementary Math

**Intuition**

Keep track of the carry using a variable and simulate digits-by-digits sum starting from the head of list, which contains the least-significant digit.

<img src="images/integer/solutionAddTwoNumbers.png" width="900" />

Figure 1. Visualization of the addition of two numbers: 342 + 465 = 807342+4=807.
Each node contains a single digit and the digits are stored in reverse order.


**Algorithm**

Just like how you would sum two numbers on a piece of paper, we begin by summing the least-significant digits, which is the head of l1l1 and l2l2. Since each digit is in the range of 0 \ldots 90…9, summing two digits may "overflow". For example 5 + 7 = 125+7=12. In this case, we set the current digit to 22 and bring over the carry = 1carry=1 to the next iteration. carrycarry must be either 00 or 11 because the largest possible sum of two digits (including the carry) is 9 + 9 + 1 = 199+9+1=19.

The pseudocode is as following:

Initialize current node to dummy head of the returning list.
Initialize carry to 00.
Initialize pp and qq to head of l1 and l2 respectively.
Loop through lists l1 and l2 until you reach both ends.
Set x to node p's value. If p has reached the end of l1, set to 0.
Set y to node q's value. If q has reached the end of l2, set to 0.
Set sum = x + y + carry.
Update carry = sum / 10.
Create a new node with the digit value of (sum mod10) and set it to current node's next, then advance current node to next.
Advance both pp and qq.
1.Check if carry = 1, if so append a new node with digit 11 to the returning list.
2.Return dummy head's next node.

Note that we use a dummy head to simplify the code. Without a dummy head, you would have to write extra conditional statements to initialize the head's value.

Take extra caution of the following cases:


| Test case | Explanation                             |
|-----------|-----------------------------------------|
| l1=[0,1]  | When one list is longer than the other. | 
| l2=[0,1,2] |  When one list is longer than the other.| 
| l1=[]     | When one list is null, which means an empty list.| 
| l2=[0,1]  |  When one list is null, which means an empty list.| 
|   l1=[9,9] | The sum could have an extra carry of one at the end, which is easy to forget.| 
|    l2=[1]|  The sum could have an extra carry of one at the end, which is easy to forget. |   



#### Implementation 

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {

 public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
  ListNode dummyHead = new ListNode(0);
  ListNode p = l1, q = l2, curr = dummyHead;
  int carry = 0;
  while (p != null || q != null) {
   int x = (p != null) ? p.val : 0;
   int y = (q != null) ? q.val : 0;
   int sum = carry + x + y;
   carry = sum / 10;
   curr.next = new ListNode(sum % 10);
   curr = curr.next;
   if (p != null) p = p.next;
   if (q != null) q = q.next;
  }
  if (carry > 0) {
   curr.next = new ListNode(carry);
  }
  return dummyHead.next;
 }
}
```

#### Complexity Analysis

**Time complexity** : O(max(m,n)). Assume that mm and nn represents the length of l1 and l2 respectively, the algorithm above iterates at most  `max(m,n)` times.

**Space complexity** : O(max(m,n)). The length of the new list is at most  max(m,n)+1.

### Solution 2

#### Implementation
```java
public class AddTwoNumbers {

    private static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // Head of the new linked list - this is the head of the resultant list
        ListNode head = null;
        // Reference of head which is null at this point
        ListNode temp = null;
        // Carry
        int carry = 0;
        // Loop for the two lists
        while (l1 != null || l2 != null) {
            // At the start of each iteration, we should add carry from the last iteration
            int sum = carry;
            // Since the lengths of the lists may be unequal, we are checking if the
            // current node is null for one of the lists
            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }
            // At this point, we will add the total sum % 10 to the new node
            // in the resultant list
            ListNode node = new ListNode(sum % 10);
            // Carry to be added in the next iteration
            carry = sum / 10;
            // If this is the first node or head
            if (temp == null) {
                temp = head = node;
            }
            // For any other node
            else {
                temp.next = node;
                temp = temp.next;
            }
        }
        // After the last iteration, we will check if there is carry left
        // If it's left then we will create a new node and add it
        if (carry > 0) {
            temp.next = new ListNode(carry);
        }
        return head;
    }
}
```

#### Complexity Analysis

**Time Complexity** : Since we are iterating both the lists only once, the time complexity would be O(m + n). Here m and n are the numbers of nodes in the two linked lists.

**Space Complexity** : Since we are using extra space only for our variables, our space complexity would be O(1). One might argue that we are using another list to store our result so the space complexity should also be O(m + n).


---

## Fibonacci Number

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,
```log
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

Given n, calculate F(n).

**Example 1:**
```log
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

**Example 2:**
```log
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

**Example 3:**
```log
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

**Constraints:**

```log
0 <= n <= 30
```

### Solution 1 : Recursion

**Intuition**

Use recursion to compute the Fibonacci number of a given integer.

<img src="images/integer/recursion.png" width="500" height="200"/>

             Figure 1. An example tree representing what fib(5) would look like

**Algorithm**

* Check if the provided input value, N, is less than or equal to 1. If true, return N.

* Otherwise, the function `fib(int N)` calls itself, with the result of the 2 previous numbers being added to each other, passed in as the argument. This is derived directly from the `recurrence relation`: F_{n} = F_{n-1} + F_{n-2}
  
* Do this until all numbers have been computed, then return the resulting answer.

#### Implementation

```java
public class Solution {
    public int fib(int N) {
        if (N <= 1) {
            return N;
        }
        return fib(N - 1) + fib(N - 2);
    }
}
```
#### Complexity Analysis

* **Time complexity:** O(2^N). This is the slowest way to solve the Fibonacci Sequence because it takes exponential time. The amount of operations needed, for each level of recursion, grows exponentially as the depth approaches N.

* **Space complexity:** O(N). We need space proportional to N to account for the max size of the stack, in memory. This stack keeps track of the function calls to `fib(N)`. This has the potential to be bad in cases that there isn't enough physical memory to handle the increasingly growing stack, leading to a StackOverflowError. The Java docs have a good explanation of this, describing it as an error that occurs because an application recurses too deeply.

### Solution 2 : Bottom-Up Approach using Tabulation

**Intuition**

Improve upon the recursive approach by using iteration, still solving for all of the sub-problems and returning the answer for N, using already computed Fibonacci values. While using a bottom-up approach, we can iteratively compute and store the values, only returning once we reach the result.

**Algorithm**

* If N is less than or equal to 1, return N
* Otherwise, iterate through N, storing each computed answer in an array along the way.
* Use this array as a reference to the 2 previous numbers to calculate the current Fibonacci number.
* Once we've reached the last number, return it's Fibonacci number.

#### Implementation

```java
class Solution {
    public int fib(int N) {
        if (N <= 1) {
            return N;
        }
                  
        int[] cache = new int[N + 1];
        cache[1] = 1;
        for (int i = 2; i <= N; i++) {
            cache[i] = cache[i - 1] + cache[i - 2];
        }
    
        return cache[N];
    }
}
```
#### Complexity Analysis

**Time complexity:** O(N). Each number, starting at 2 up to and including N, is visited, computed and then stored for O(1) access later on.

**Space complexity:** O(N). The size of the data structure is proportional to N.

### Solution 3 : Top-Down Approach using Memoization

**Intuition**

Solve for all of the sub-problems, use memoization to store the pre-computed answers, then return the answer for N. We will leverage recursion, but in a smarter way by not repeating the work to calculate existing values.

**Algorithm**

* At first, create a map with 0 -> 0 and 1 -> 1 pairs.
* Call `fib(N)` function.
     1. At every recursive call of `fib(N)`, if N exists in the map, return the cached value for N.
     2. Otherwise, set the key N, in our mapping, to the value of fib(N - 1) + fib(N - 2) and return the computed value.

#### Implementation
```java
class Solution {
    // Creating a hash map with 0 -> 0 and 1 -> 1 pairs
    private Map<Integer, Integer> cache = new HashMap<>(Map.of(0, 0, 1, 1));

    public int fib(int N) {
        if (cache.containsKey(N)) {
            return cache.get(N);
        }
        cache.put(N, fib(N - 1) + fib(N - 2));
        return cache.get(N);
    }
}
```

#### Complexity Analysis

**Time complexity:** O(N). Each number, starting at 2 up to and including N, is visited, computed and then stored for O(1) access later on.

**Space complexity:** O(N). The size of the stack in memory is proportional to N. Also, the memoization hash table is used, which occupies O(N) space.

### Solution 4 : Iterative Bottom-Up Approach

**Intuition**

Let's get rid of the need to use all of that space and instead use the minimum amount of space required. Notice that during each recursive call in the top-down approach and each iteration in the bottom-up approach, we only needed to look at the results of `fib(N-1)` and `fib(N-2)` to determine the result of `fib(N)`. Therefore, we can achieve O(1) space complexity by only storing the value of the two previous numbers and updating them as we iterate to N.

**Algorithm**

* Check if N <= 1, if it is, then we should return N.
* We need 3 variables to store each state `fib(N), fib(N-1), and fib(N-2)`.
* Preset the initial values:
   - Initialize current with 0.
   - Initialize prev1 with 1, since this will represent `fib(N-1)` when computing the current value.
   - Initialize prev2 with 0, since this will represent `fib(N-2)` when computing the current value.
* Iterate, incrementally by 1, all the way up to and including N. Starting at 2, since 0 and 1 are pre-computed.
* Set the current value to prev1 + prev2 because that is the value we are currently computing.
* Set the prev2 value to prev1.
* Set the prev1 value to current.
* When we reach N+1, we will exit the loop and return the previously set current value.

#### Implementation


```java
class Solution {
    public int fib(int N) {
        if (N <= 1) {
            return N;
        }

        int current = 0;
        int prev1 = 1;
        int prev2 = 0;

        for (int i = 2; i <= N; i++) {
            current = prev1 + prev2;
            prev2 = prev1;
            prev1 = current;
        }
        return current;
    }
}
```

#### Complexity Analysis

**Time complexity:** O(N). Each value from 2 to N is computed once. Thus, the time it takes to find the answer is directly proportional to N where N is the Fibonacci Number we are looking to compute.

**Space complexity:** O(1). This requires 1 unit of space for the integer N and 3 units of space to store the computed values (current, prev1, and prev2) for every loop iteration. The amount of space used is independent of N, so this approach uses a constant amount of space.

### Solution 5 : Matrix Exponentiation

**Intuition**

Use Matrix Exponentiation to get the Fibonacci number from the element at (0, 0) in the resultant matrix.

In order to do this we can rely on the matrix equation for the Fibonacci sequence, to find the `Nth` Fibonacci number:

 <img src="images/integer/MatrixExponentiation.png" width="200" height="100" />

**Algorithm**

* Check if N is less than or equal to 1. If it is, return N.
* Use a recursive function, matrixPower, to calculate the power of a given matrix A. The power will be N-1, where N is the `Nth` Fibonacci number.
* The matrixPower function will be performed for N/2 of the Fibonacci numbers.
* Within matrixPower, call the multiply function to multiply 2 matrices.
* Once we finish doing the calculations, return A[0][0] to get the Nth Fibonacci number.

#### Implementation

```java
//TODO: 

```
#### Complexity Analysis

**Time complexity:** O(logN). By halving the N value in every matrixPower's call to itself, we are halving the work needed to be done.

**Space complexity:** O(logN). The size of the stack in memory is proportional to the function calls to matrixPower plus the memory used to account for the matrices which use constant space.

### Solution 6 : Math

**Intuition**

<img src="images/integer/mathFibonacci.png" width="500" height="50" />

Here's a link to find out more about how the Fibonacci sequence and the `golden ratio` work.

We can derive the most efficient solution to this problem using only constant space!

**Algorithm**

Use the `golden ratio` formula to calculate the `Nth` Fibonacci number.

#### Implementation

```java
class Solution {
    public int fib(int N) {
        double goldenRatio = (1 + Math.sqrt(5)) / 2;
        return (int) Math.round(Math.pow(goldenRatio, N) / Math.sqrt(5));
    }
}
```

#### Complexity Analysis

**Time complexity:** O(logN). We do not use loops or recursion, so the time required equals the time spent performing the calculation using Binet's formula. However, raising the golden_ratio to the power of N requires O(logN) time.

**Space complexity:** O(1). The space used is the space needed to create the variable to store the `golden ratio`.

### Solution 7 : Alternative methods 

#### Implementation 1 : Iterative

```java
class Solution 
{
    public int fib(int N)
    {
        if(N <= 1)
            return N;
        
		int a = 0, b = 1;
		
		while(N-- > 1)
		{
			int sum = a + b;
			a = b;
			b = sum;
		}
        return b;
    }
}
```

**Time complexity:**  O(n).

**Space complexity:** O(1).

#### Implementation 2 : Recursive

```java
class Solution 
{
    public int fib(int N)
    {
        if(N <= 1)
            return N;
        else
            return fib(N - 1) + fib(N - 2);
    }
}
```
**Time complexity:** O(2^n)- since T(n) = T(n-1) + T(n-2)is an exponential time.

**Space complexity:** O(n) - space for recursive function call stack

#### Implementation 3 : Dynamic Programming - Top Down Approach

```java
class Solution 
{
    int[] fib_cache = new int[31];
	
	public int fib(int N)
    {
        if(N <= 1)
            return N;
        else if(fib_cache[N] != 0)
            return fib_cache[N];
		else 
            return fib_cache[N] = fib(N - 1) + fib(N - 2);
    }
}
```
**Time complexity:** O(n).

**Space complexity:** O(n).

#### Implementation 4 : Dynamic Programming - Bottom Up Approach

```java
class Solution 
{
    public int fib(int N)
    {
        if(N <= 1)
            return N;

		int[] fib_cache = new int[N + 1];
		fib_cache[1] = 1;

		for(int i = 2; i <= N; i++)
		{
			fib_cache[i] = fib_cache[i - 1] + fib_cache[i - 2];
		}
		return fib_cache[N];
    }
}
```
**Time complexity:** O(n).

**Space complexity:** O(n).




---

## Perfect Number

A `perfect number` is a **positive integer** that is equal to the sum of its **positive divisors**, excluding the number itself. A divisor of an integer `x` is an integer that can divide `x` evenly.

Given an integer `n`, return `true` if `n` is a `perfect number`, otherwise return `false`.


**Example 1:**

```log
Input: num = 28
Output: true
Explanation: 28 = 1 + 2 + 4 + 7 + 14
1, 2, 4, 7, and 14 are all divisors of 28.
```

**Example 2:**

```log
Input: num = 7
Output: false
```

**Constraints:**

```log
1 <= num <= 108
```

### Solution 1 : Brute Force [Time Limit Exceeded]

**Algorithm**

In brute force approach, we consider every possible number to be a divisor of the given number `num`, by iterating over all the numbers lesser than `num`. Then, we add up all the factors to check if the given number satisfies the `Perfect Number` property. This approach obviously fails if the number `num` is very large.

#### Implementation

```java

public class Solution {
    public boolean checkPerfectNumber(int num) {
        if (num <= 0) {
            return false;
        }
        int sum = 0;
        for (int i = 1; i < num; i++) {
            if (num % i == 0) {
                sum += i;
            }

        }
        return sum == num;
    }
}
```

#### Complexity Analysis

**Time complexity** : O(n). We iterate over all the numbers lesser than `n`.

**Space complexity** : O(1). Constant extra space is used.

### Solution 2 : Better Brute Force [Time Limit Exceeded]

**Algorithm**

We can little optimize the brute force by breaking the loop when the value of `sum` increase the value of `num`. In that case, we can directly return `false`.

#### Implementation

```java

public class Solution {
    public boolean checkPerfectNumber(int num) {
        if (num <= 0) {
            return false;
        }
        int sum = 0;
        for (int i = 1; i < num; i++) {
            if (num % i == 0) {
                sum += i;
            }
            if(sum>num) {
                return false;
            }
        }
        return sum == num;
    }
}
```
#### Complexity Analysis

**Time complexity** : O(n). In worst case, we iterate over all the numbers lesser than `n`.

**Space complexity** : O(1). Constant extra space is used.

### Solution 3 : Optimal Solution [Accepted]

**Algorithm**

 <img src="images/integer/PerfectNumOptimalSol.png" width="1000" height="200" />

#### Implementation

```java

    public boolean checkPerfectNumber(int num) {
        if (num <= 0) {
            return false;
        }
        int sum = 0;
        for (int i = 1; i * i <= num; i++) {
            if (num % i == 0) {
                sum += i;
                if (i * i != num) {
                    sum += num / i;
                }

            }
        }
        return sum - num == num;
    }
}
```
#### Complexity Analysis

**Time complexity** : O(sqrt{n}). We iterate only over the range 1 < i ≤ \sqrt{num}.

**Space complexity** : O(1). Constant extra space is used.

### Solution 4 : Euclid-Euler Theorem [Accepted]

**Algorithm**

Euclid proved that 2^{p−1}(2^p − 1) is an even perfect number whenever 2^p − 1 is prime, where *p* is prime.

For example, the first four perfect numbers are generated by the formula 2^{p−1}(2^p − 1), with *p* a prime number, as follows:

```log
for p = 2:   21(22 − 1) = 6
for p = 3:   22(23 − 1) = 28
for p = 5:   24(25 − 1) = 496
for p = 7:   26(27 − 1) = 8128.
```

Prime numbers of the form 2^p − 1 are known as Mersenne primes. For 2^p − 1 to be prime, it is necessary that *p* itself be prime. However, not all numbers of the form 2^p − 1 with a prime *p* are prime; for example, 2^{11} − 1 = 2047 = 23 × 89 is not a prime number.

You can see that for small value of *p*, its related perfect number goes very high. So, we need to evaluate perfect numbers for some primes (2, 3, 5, 7, 13, 17, 19, 31) only, as for bigger prime its perfect number will not fit in 64 bits.

#### Implementation

```java
public class Solution {
    public int pn(int p) {
        return (1 << (p - 1)) * ((1 << p) - 1);
    }
    public boolean checkPerfectNumber(int num) {
        int[] primes=new int[]{2,3,5,7,13,17,19,31};
        for (int prime: primes) {
            if (pn(prime) == num)
                return true;
        }
        return false;
    }
}
```

#### Complexity Analysis

**Time complexity** : O(logn). Number of primes will be in order log *num*.

**Space complexity** : O(logn). Space used to store primes.

---

## Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

**Example 1:**

```log
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```log
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```log
Input: nums = [3,3], target = 6
Output: [0,1]
```

**Constraints:**

```log
2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
```

### Solution 1 : Brute Force

**Algorithm**

The brute force approach is simple. Loop through each element *x* and find if there is another value that equals to target - x.

#### Implementation

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] == target - nums[i]) {
                    return new int[] { i, j };
                }
            }
        }
        // In case there is no solution, we'll just return null
        return null;
    }
}
```

#### Complexity Analysis

**Time complexity:** O(n^2). For each element, we try to find its complement by looping through the rest of the array which takes O(n) time. Therefore, the time complexity is O(n^2).

**Space complexity:** O(1). The space required does not depend on the size of the input array, so only constant space is used.

### Solution 2 : Two-pass Hash Table

**Intuition**

To improve our runtime complexity, we need a more efficient way to check if the complement exists in the array. If the complement exists, we need to get its index. What is the best way to maintain a mapping of each element in the array to its index? A hash table.

We can reduce the lookup time from O(n) to O(1) by trading space for speed. A hash table is well suited for this purpose because it supports fast lookup in near constant time. I say "near" because if a collision occurred, a lookup could degenerate to O(n) time. However, lookup in a hash table should be amortized O(1) time as long as the hash function was chosen carefully.

**Algorithm**

A simple implementation uses two iterations. In the first iteration, we add each element's value as a key and its index as a value to the hash table. Then, in the second iteration, we check if each element's complement *(target - nums[i])* exists in the hash table. If it does exist, we return current element's index and its complement's index. Beware that the complement must not be nums[i] itself!

#### Implementation

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement) && map.get(complement) != i) {
                return new int[] { i, map.get(complement) };
            }
        }
        // In case there is no solution, we'll just return null
        return null;
    }
}
```

#### Complexity Analysis

**Time complexity:** O(n). We traverse the list containing nn elements exactly twice. Since the hash table reduces the lookup time to O(1), the overall time complexity is O(n).

**Space complexity:** O(n). The extra space required depends on the number of items stored in the hash table, which stores exactly nn elements.

### Solution 3 : One-pass Hash Table

**Algorithm**

It turns out we can do it in one-pass. While we are iterating and inserting elements into the hash table, we also look back to check if current element's complement already exists in the hash table. If it exists, we have found a solution and return the indices immediately.

#### Implementation

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }
        // In case there is no solution, we'll just return null
        return null;
    }
}
```

#### Complexity Analysis

**Time complexity:** O(n). We traverse the list containing n elements only once. Each lookup in the table costs only O(1) time.

**Space complexity:** O(n). The extra space required depends on the number of items stored in the hash table, which stores at most *n* elements.

### Solution 4 : O(nlogn), beats  98.85%

**Algorithm**

step1 : copy an array, and sort it using quick sort, O(nlogn)

step2 : using start and end points to find a, b which satifys a+b==target, O(n)

step3 : find the index of a, b from origin array, O(n)

note: in step3, you should judge whethour a==b, if true, you must find the second index of b.

#### Implementation

```java
public int[] twoSum_n2(int[] nums, int target) {
	    	if(nums == null)
	    		return null;
	    	int[] nums2 = Arrays.copyOf(nums, nums.length);
	    	Arrays.sort(nums2);
	    	int a = 0, b = 0;
	    	int start = 0, end = nums2.length-1;
	    	//find two nums
	    	while(start<end){
	    		int sum = nums2[start] + nums2[end];
	    		if(sum < target)
	    			start++;
	    		else if(sum > target)
	    			end--;
	    		else{
	    			a = nums2[start]; b = nums2[end];
	    			break;
	    		}
	    	}
	    	//find the index of two numbers
	    	int[] res = new int[2];
	    	for(int i = 0; i < nums.length; i++){
	    		if(nums[i] == a){
	    			res[0] = i;
	    			break;
	    		}
	    	}
	    	if(a != b){
	    		for(int i = 0; i < nums.length; i++){
		    		if(nums[i] == b){
		    			res[1] = i;
		    			break;
		    		}
		    	}
	    	} else{
	    		for(int i = 0; i < nums.length; i++){
		    		if(nums[i] == b && i != res[0]){
		    			res[1] = i;
		    			break;
		    		}
		    	}
	    	}
	    	
	    	return res;
	    }
```
---

## Subarray Sum Equals K

Given an array of integers `nums` and an integer `k`, return the total number of sub-arrays whose sum equals to `k`.

A sub-array is a contiguous **non-empty** sequence of elements within an array.


**Example 1:**

```log
Input: nums = [1,1,1], k = 2
Output: 2
```

**Example 2:**

```log
Input: nums = [1,2,3], k = 3
Output: 2
```

**Constraints:**

```log
1 <= nums.length <= 2 * 104
-1000 <= nums[i] <= 1000
-107 <= k <= 107
```

### Solution 1 : Brute Force

**Algorithm**

The simplest method is to consider every possible sub-array of the given *nums* array, find the sum of the elements of each of those sub-arrays and check for the equality of the sum obtained with the given *k*. Whenever the sum equals *k*, we can increment the *count* used to store the required result.

#### Implementation

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        for (int start = 0; start < nums.length; start++) {
            for (int end = start + 1; end <= nums.length; end++) {
                int sum = 0;
                for (int i = start; i < end; i++)
                    sum += nums[i];
                if (sum == k)
                    count++;
            }
        }
        return count;
    }
}
```

#### Complexity Analysis

**Time complexity** : O(n^3). Considering every possible sub-array takes O(n^2) time. For each of the sub-array we calculate the sum taking O(n)O(n) time in the worst case, taking a total of O(n^3) time.

**Space complexity** : O(1). Constant space is used.

### Solution 2 : Using Cumulative Sum

**Algorithm**

Instead of determining the sum of elements every time for every new sub-array considered, we can make use of a cumulative sum array , *sum*. Then, in order to calculate the sum of elements lying between two indices, we can subtract the cumulative sum corresponding to the two indices to obtain the sum directly, instead of iterating over the sub-array to obtain the sum.

#### Implementation

We make use of a cumulative sum array, *sum*, such that sum[i] is used to store the cumulative sum of *nums* array up to the element corresponding to the (i-1)^{th} index. Thus, to determine the sum of elements for the sub-array nums[i:j], we can directly use sum[j+1]−sum[i].

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        int[] sum = new int[nums.length + 1];
        sum[0] = 0;
        for (int i = 1; i <= nums.length; i++)
            sum[i] = sum[i - 1] + nums[i - 1];
        for (int start = 0; start < nums.length; start++) {
            for (int end = start + 1; end <= nums.length; end++) {
                if (sum[end] - sum[start] == k)
                    count++;
            }
        }
        return count;
    }
}
```

#### Complexity Analysis

**Time complexity** : O(n^2). Considering every possible sub-array takes O(n^2) time. Finding out the sum of any sub-array takes O(1) time after the initial processing of O(n) for creating the cumulative sum array.

**Space complexity** : O(n). Cumulative sum array *sum* of size `n+1` is used.

### Solution 3 : Without Space

**Algorithm**

Instead of considering all the *start* and *end* points and then finding the sum for each sub-array corresponding to those points, we can directly find the sum on the go while considering different *end* points. i.e. We can choose a particular *start* point and while iterating over the *end* points, we can add the element corresponding to the *end* point to the sum formed till now. Whenever the *sum* equals the required *k* value, we can update the *count* value. We do so while iterating over all the *end* indices possible for every *start* index. Whenever, we update the *start* index, we need to reset the *sum* value to 0.

#### Implementation

```
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        for (int start = 0; start < nums.length; start++) {
            int sum=0;
            for (int end = start; end < nums.length; end++) {
                sum+=nums[end];
                if (sum == k)
                    count++;
            }
        }
        return count;
    }
}
```
#### Complexity Analysis

**Time complexity** : O(n^2). We need to consider every sub-array possible.

**Space complexity** : O(1). Constant space is used.

### Solution 4: Using Hashmap

#### Implementation

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0, sum = 0;
        HashMap < Integer, Integer > map = new HashMap < > ();
        map.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```
#### Complexity Analysis

**Time complexity** : O(n). The entire *nums* array is traversed only once.

**Space complexity** : O(n). Hashmap *map* can contain up to *n* distinct entries in the worst case.

### Solution 5 : easy to optimized

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        
        // Time Complexity O(sq(n))
        // int count=0;
        // int sum=0;
        // int n=nums.length;
        // for(int i=0;i<n;i++){
        //     sum=nums[i];
        //     if(sum==k){
        //         count++;
        //     }
        //     for(int j=i+1;j<n;j++){
        //         sum=sum+nums[j];
        //          if(sum==k){
        //          count++;
        //     }
        //     }
        // }
        // return count;
        
        // Time Complexity is O(n)
        int n=nums.length;
        int res=0;
        int sum=0;
        Map<Integer,Integer> pre=new HashMap<>();
        
        pre.put(0,1);
        for(int i=0;i<n;i++){
            sum+=nums[i];
            if(pre.containsKey(sum-k)){              
                        res+=pre.get(sum-k);
            }
                 pre.put(sum,(pre.getOrDefault(sum,0)+1));       
                        
        }
        
        
        return res;
        
    }
}
```

---









## More Details: 
1. [Palindrome Number - Leetcode #9 Short & Simple Solution](https://www.code-recipe.com/post/palindrome-number)
2. [Generating Prime Numbers in Java](https://www.baeldung.com/java-generate-prime-numbers)


