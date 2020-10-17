## Description

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```



**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

## Thinking

Sliding Windows

## Solutions

~~~java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        if (s.length() == 0 || p.length() == 0) return new ArrayList<Integer>();
        
        List<Integer> result = new ArrayList<Integer>();
        int map[] = new int[26];
        int exist[] = new int[26];
        for(char c : p.toCharArray()) {
            map[c - 'a']++;
            exist[c - 'a'] = 1;
        }
        int start = 0, end = 0, counter = p.length();
        
        while(end < s.length()) {
            char c1 = s.charAt(end);
            if (exist[c1 - 'a'] > 0) {
                if (map[c1 - 'a']-- > 0) counter--;
            }
            end++;
            
            while(counter == 0) {
                char c2 = s.charAt(start);
                if (end - start == p.length()) result.add(start);
                if (exist[c2 - 'a'] > 0) {
                    if (map[c2 - 'a']++ >= 0) counter++;
                }
                start++;
            }
        }
        
        return result;
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hua-dong-chuang-kou-ji-qiao-jin-jie