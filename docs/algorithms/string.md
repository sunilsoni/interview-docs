---
layout: default
title: String
parent: Data Structures

---

# String
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

---

## Reverse String

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

**Example:**

Input: s = ["h","e","l","l","o"]

Output: ["o","l","l","e","h"]

###  Solution1

Two pointers i and j, pointing to the beginning and end, respectively. While i < j, swap.
Using a helper swap function severely impacts runtime and memory, so we swap in the loop.

####  Implementation

```java
class Solution {
    public void reverseString(char[] s) {
        int len = s.length;
        int left = 0;
        int right = s.length - 1;
        while(left < right) {
            char tmp = s[left];
            s[left] = s[right];
            s[right] = tmp;
            left++;
            right--;
        }
    }
}
```

####  Runtime
3 ms

####  Memory
52.6 MB

####  Complexity Analysis


**Time Complexity**: 

We are iterating  half array hence it will take O(n/2) which will become O(n).

**Space Complexity**: 

O(1)

###  Solution2

Using for loop swap.

####  Implementation
```java
 class Solution {
    public void reverseString(char[] s) {
        for (int i = 0; i < s.length / 2; i++) {    //Do it half the number of String length
            char tmp = s[i];
            s[i] = s[s.length - 1 - i];     //Front swap with other End side 
            s[s.length - 1 - i] = tmp;      //End swap with other Front side
        }
    }
}
```

####  Runtime
1 ms

####  Memory
52.7 MB

####  Complexity Analysis


**Time Complexity**:

We are iterating  half array hence it will take O(n/2) which will become O(n).

**Space Complexity**:

O(1)


###  Solution3

Add to extra space from rear to front then  Set reversed 'str' into char array 's'

####  Implementation
```java
 class Solution {
    public void reverseString(char[] s) {
        String str = "";                   //Allocate extra space

        for (int i = s.length - 1; i >= 0; i--)   /*Add to extra space from rear to front */
            str += s[i];

        for (int i = 0; i < s.length; i++)      /*Set reversed 'str' into char array 's' */
            s[i] = str.charAt(i);
    }
}
```



###  Solution4

Using StringBuilder reverse method.

####  Implementation

```java
return new StringBuilder(s).reverse().toString();

```



---

## Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

Iif there is no common prefix, return an empty string "".

**Example 1:**

- Input: strs = ["flower","flow","flight"]
- Output: "fl"


**Example 2:**

- Input: strs = ["dog","racecar","car"]
- Output: ""
- Explanation: There is no common prefix among the input strings.

###  Solution1

1. Take the first(index=0) string in the array as prefix.
2. Iterate from second(index=1) string till the end.
3. Use the indexOf() function to check if the prefix is there in the strs[i] or not. If the prefix is there the function returns 0 else -1.
4. Use the substring function to chop the last letter from prefix each time the function return -1.

```log
**Example :**
strs=["flower", "flow", "flight"]
prefix=flower

**index=1**
while(strs[index].indexOf(prefix) != 0) means while("flow".indexOf("flower")!=0)
Since flower as a whole is not in flow, it return -1 and  prefix=prefix.substring(0,prefix.length()-1) reduces prefix to "flowe"
Again while(strs[index].indexOf(prefix) != 0) means while("flow".indexOf("flowe")!=0)
Since flowe as a whole is not in flow, it return -1 and  prefix=prefix.substring(0,prefix.length()-1) reduces prefix to "flow"
Again while(strs[index].indexOf(prefix) != 0) means while("flow".indexOf("flow")!=0)
Since flow as a whole is in flow, it returns 0 so now prefix=flow

**index=2**
while(strs[index].indexOf(prefix) != 0) means while("flight".indexOf("flow")!=0)
Since flow as a whole is not in flight, it return -1 and  prefix=prefix.substring(0,prefix.length()-1) reduces prefix to "flo"
Again while(strs[index].indexOf(prefix) != 0) means while("flight".indexOf("flo")!=0)
Since flo as a whole is not in flight, it return -1 and  prefix=prefix.substring(0,prefix.length()-1) reduces prefix to "fl"
Again while(strs[index].indexOf(prefix) != 0) means while("flight".indexOf("fl")!=0)
Since fl as a whole is in flight, it returns 0 so now prefix=fl

**index=3** 
for loop terminates and we return prefix which is equal to fl
```

####  Implementation

```java
 class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) return "";
        String prefix = strs[0];
        for(int i=1; i< strs.length; i++ ) {
            while(strs[i].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length()-1);
            }
        }

        return prefix;
    }
}
```

####  Runtime
1 ms

####  Memory
39.2 MB

####  Complexity Analysis

**Time Complexity**:
O(n)

**Space Complexity**:
O(1)


###  Solution2

####  Implementation

```java
 class Solution {
 public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0)
            return "";
        
        Arrays.sort(strs);
        String first = strs[0];
        String last = strs[strs.length - 1];
        int c = 0;
        while(c < first.length())
        {
            if (first.charAt(c) == last.charAt(c))
                c++;
            else
                break;
        }
        return c == 0 ? "" : first.substring(0, c);
    }
}
}   
```




---

## Reverse Words in a String

Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.



**Example 1:**

- Input: s = "the sky is blue"
- Output: "blue is sky the"

**Example 2:**

Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.

**Example 3:**

Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.

####  Implementation

```java
 
```

####  Runtime


####  Memory


####  Complexity Analysis

**Time Complexity**:

**Space Complexity**:


---

## Test


####  Implementation

```java
 
```

####  Runtime


####  Memory


####  Complexity Analysis

**Time Complexity**:

**Space Complexity**:

---

## More Details: 
1. [Reverse-string Java, Simple Multiple solutions w/explanations!](https://leetcode.com/problems/reverse-string/discuss/275116/Java-Simple-Multiple-solutions-wexplanations!)


