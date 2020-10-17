## Description

Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.

 

**Example 1:**

```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**

```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

 

**Constraints:**

- The input strings only contain lower case letters.
- The length of both given strings is in range [1, 10,000].

## Thinking

Sliding Windows of the f course

## Solutions

~~~java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() == 0 || s2.length() == 0) {
            return false;
        }
        
        int map[] = new int[26];
        int count[] = new int[26];
        for (char c : s1.toCharArray()) {
            map[c - 'a']++;
            count[c - 'a'] = 1;
        }
        
        int start = 0, end = 0, counter = s1.length();
        
        while(end < s2.length()) {
            char c1 = s2.charAt(end);
            if (count[c1 - 'a'] == 1 ) {
                if (map[c1 - 'a'] > 0) {
                    counter--;
                }
                map[c1 - 'a']--;
            } 
            end++;
            
            while(counter == 0) {
                if (end - start == s1.length()) return true;
                char c2 = s2.charAt(start);
                if(count[c2 - 'a'] == 1) {
                    if (map[c2 - 'a']  >= 0) {
                        counter++;
                    }
                    map[c2 - 'a']++;
                }
                start++;
            }
        }
        
        return false;
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hua-dong-chuang-kou-ji-qiao-jin-jie

https://leetcode.com/problems/permutation-in-string/discuss/102588/Java-Solution-Sliding-Window