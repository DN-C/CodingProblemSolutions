## Description

Given a string `s`, return *the longest palindromic substring* in `s`.

 

**Example 1:**

```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: s = "cbbd"
Output: "bb"
```

**Example 3:**

```
Input: s = "a"
Output: "a"
```

**Example 4:**

```
Input: s = "ac"
Output: "a"
```

 

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters (lower-case and/or upper-case),

## Thinking

Iterate every element in the string, for each element, find the longest palindrome with the element as the middle element, or as one of the two middle elements. Save the longest substring, return it.

A dynamic programing solution in further part.

## Solutions

~~~java
class Solution {
    public String longestPalindrome(String s) {
        String res = "";
        for(int i = 0; i < s.length(); ++i) {
            String res1 = palindrome(s, i, i);
            String res2 = palindrome(s, i, i + 1);
            
            res = res.length() > res1.length() ? res : res1;
            res = res.length() > res2.length() ? res : res2;
        }
        return res;
    }
    
    public String palindrome(String s, int lp, int rp) {
        while(lp >= 0 && rp < s.length() && s.charAt(lp) == s.charAt(rp)) {
            --lp;
            ++rp;
        }
        if(rp - lp == 0) return s.substring(lp, rp + 1);
        else if(rp - lp == 1) return "";
        return s.substring(lp + 1, rp);
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E6%9C%80%E9%95%BF%E5%9B%9E%E6%96%87%E5%AD%90%E4%B8%B2.md

https://leetcode.com/problems/longest-palindromic-substring/discuss/2921/Share-my-Java-solution-using-dynamic-programming