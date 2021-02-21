## Description

Given two strings *s* and *t* , write a function to determine if *t* is an anagram of *s*.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

## Thinking

Iterate triple times, first time to save all characters of s in array, second time to deduct all characters of t from array, third time to check if there is unmatchable result in array.

## Solutions

~~~java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s == null && s == null) return true;
        if((s == null && t != null) || (s != null && t == null)) return false;
        int[] array = new int[26]; 
        for(char c : s.toCharArray()) {
            array[c - 'a'] = array[c - 'a'] + 1;
        }
        for(char c : t.toCharArray()) {
            array[c - 'a'] = array[c - 'a'] - 1;
            if(array[c - 'a'] < 0) return false;
        }
        for(int i : array) {
            if(i != 0) return false;
        }
        return true;
    }
}
~~~



## Further
