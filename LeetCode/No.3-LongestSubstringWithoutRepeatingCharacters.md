## Description

Given a string `s`, find the length of the **longest substring** without repeating characters.

 

**Example 1:**

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Example 4:**

```
Input: s = ""
Output: 0
```

 

**Constraints:**

- `0 <= s.length <= 5 * 104`
- `s` consists of English letters, digits, symbols and spaces.

## Thinking

1. 使用Hashmap储存，key为字符，value为position，然后额外储存当前最大长度。从头到尾遍历字符串，不重复的放入hashmap，同时视情况决定是否更新当前最大长度。出现重复后，将hashmap内重复字符以及所有position在此之前的字符全部清除，然后put新的字符与位置进入。
2. 1的改良，若出现重复，直接更新hashmap，同时用一个int j储存重复字符的旧有位置，好处是不需要清楚之前的字符，可以通过i与j对比得出当前长度，然后与当前最大长度对比。
3. Sliding Window

## Solutions

~~~java


// Solution 2 from cbmbbz
   public int lengthOfLongestSubstring(String s) {
        if (s.length()==0) return 0;
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        int max=0;
        for (int i=0, j=0; i<s.length(); ++i){
            if (map.containsKey(s.charAt(i))){
                j = Math.max(j,map.get(s.charAt(i))+1);
            }
            map.put(s.charAt(i),i);
            max = Math.max(max,i-j+1);
        }
        return max;
    }

// Solution 3 (Actually it is a complex version of Solution 2)
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s.length() == 0) return 0;
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        int start = 0, end = 0, maxLength = 0;
        for (char c :s.toCharArray()) {
            map.put(c, 1);
        }
        
        while(end < s.length()) {
            char c1 = s.charAt(end);
            map.put(c1, map.get(c1) - 1);
            end++;
            
            while (map.get(c1) < 0) {
                char c2 = s.charAt(start);
                map.put(c2, map.get(c2) + 1);
                start++;
            }
            if (end - start > maxLength) maxLength = end - start;
        }
        
        return maxLength;
        
    }
}
~~~



## Further

