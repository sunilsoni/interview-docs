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

###  Solution 1

Two-pointers solution no trim( ), no split( ), no StringBuilder


####  Implementation

```java
 public class Solution {

    public String reverseWords(String s) {
        if (s == null) return null;

        char[] a = s.toCharArray();
        int n = a.length;

        // step 1. reverse the whole string
        reverse(a, 0, n - 1);
        // step 2. reverse each word
        reverseWords(a, n);
        // step 3. clean up spaces
        return cleanSpaces(a, n);
    }

    void reverseWords(char[] a, int n) {
        int i = 0, j = 0;

        while (i < n) {
            while (i < j || i < n && a[i] == ' ') i++; // skip spaces
            while (j < i || j < n && a[j] != ' ') j++; // skip non spaces
            reverse(a, i, j - 1);                      // reverse the word
        }
    }

    // trim leading, trailing and multiple spaces
    String cleanSpaces(char[] a, int n) {
        int i = 0, j = 0;

        while (j < n) {
            while (j < n && a[j] == ' ') j++;             // skip spaces
            while (j < n && a[j] != ' ') a[i++] = a[j++]; // keep non spaces
            while (j < n && a[j] == ' ') j++;             // skip spaces
            if (j < n) a[i++] = ' ';                      // keep only one space
        }

        return new String(a).substring(0, i);
    }

    // reverse a[] from a[i] to a[j]
    private void reverse(char[] a, int i, int j) {
        while (i < j) {
            char t = a[i];
            a[i++] = a[j];
            a[j--] = t;
        }
    }

}
```

####  Runtime


####  Memory


####  Complexity Analysis

**Time Complexity**:

**Space Complexity**:


---

## First Unique or Non Repeated Character in a String

Find First Non Repeated Character in a String

Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

**Example 1:**

Input: s = "leetcode"
Output: 0

**Example 2:**

Input: s = "loveleetcode"
Output: 2

**Example 3:**

Input: s = "aabb"
Output: -1

###  Solution 1

####  Implementation

```java
class Solution{
    public int firstUniqChar(String s) {
        for(char c : s.toCharArray()){
            int index = s.indexOf(c);
            int lastIndex = s.lastIndexOf(c);
            if(index == lastIndex)
                return index;
        }
        return -1;
    }
}

```

####  Runtime
20 ms

####  Memory
39.5 MB

####  Complexity Analysis

**Time Complexity**:
O(n^2)

**Space Complexity**:
O(1)


###  Solution 2

####  Implementation

```java
 class Solution {
    public int firstUniqChar(String s) {
        int ans = Integer.MAX_VALUE;
        for (char i = 'a'; i <= 'z';i++) {
            int ind = s.indexOf (i);
            if (ind != -1 && ind == s.lastIndexOf (i))
                ans = Math.min (ans,ind);
        }
        if (ans == Integer.MAX_VALUE)
            return -1;
        return ans;
    }
}
```


###  Solution 3

Using LinkedHashMap to find first non repeated character of String Algorithm :
**Step 1:** get character array and loop through it to build a hash table with char and their count.
**Step 2:** loop through LinkedHashMap to find an entry with value 1, that's your first non-repeated character, as LinkedHashMap maintains insertion order.

####  Implementation

```java
 class Solution {
    public static char getFirstNonRepeatedChar(String str) {
        Map<Character,Integer> counts = new LinkedHashMap<>(str.length());

        for (char c : str.toCharArray()) {
            counts.put(c, counts.containsKey(c) ? counts.get(c) + 1 : 1);
        }

        for (Entry<Character,Integer> entry : counts.entrySet()) {
            if (entry.getValue() == 1) {
                return entry.getKey();
            }
        }
        throw new RuntimeException("didn't find any non repeated Character");
    }
 }

```


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
2. [3 ways to Find First Non Repeated Character in a String](https://javarevisited.blogspot.com/2014/03/3-ways-to-find-first-non-repeated-character-String-programming-problem.html)


