## Description

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example:**

```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

**Note:**

- If there is no such window in S that covers all characters in T, return the empty string `""`.
- If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

## Thinking

Sliding Window

## Solutions

~~~java
class Solution {
    public String minWindow(String s, String t) {
        if (s.length() == 0 || t.length() == 0) return "";
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        for(char c : t.toCharArray()) {
            if (map.containsKey(c)) map.put(c, map.get(c) + 1);
            else map.put(c, 1);
        }
        
        int start = 0;
        int end = 0;
        int minLength = Integer.MAX_VALUE;
        int minStart = 0;
        int counter = t.length();
        
        while(end < s.length()) {
            char c1 = s.charAt(end);
            if (map.containsKey(c1)) {
                map.put(c1, map.get(c1) - 1);
                if (map.get(c1) >= 0) {
                    counter--;
                }
            }
            end++;
            
            while(counter <= 0) {
                if (end - start < minLength) {
                    minStart = start;
                    minLength = end - start;
                }
                
                char c2 = s.charAt(start);
                if (map.containsKey(c2)) {
                    map.put(c2, map.get(c2) + 1);
                    if (map.get(c2) > 0) {
                        counter++;
                    }
                }
                start++;
            }
        }
        
        return minLength == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLength);
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hua-dong-chuang-kou-ji-qiao-jin-jie

https://leetcode.com/problems/minimum-window-substring/discuss/26825/Can-T-have-characters-repeating

[https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-'substring'-problems](https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-'substring'-problems)

