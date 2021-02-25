## Description

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

**Example 1:**

```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: 
"apple"
```





**Example 2:**

```
Input:
s = "abpcplea", d = ["a","b","c"]

Output: 
"a"
```



**Note:**

1. All the strings in the input will only contain lower-case letters.
2. The size of the dictionary won't exceed 1,000.
3. The length of all the strings in the input won't exceed 1,000.

## Thinking

To each word in dictionary, judge if all its letters exist in s. Use a String object to store the longest or when have same length, lexicographical smallest one. 

## Solutions

~~~java
class Solution {
    public String findLongestWord(String s, List<String> d) {
        int sLen = s.length();
        if(sLen == 0) return "";
        String longestWord = new String();
        for(String word : d) {
            int wLen = word.length(), count = 0; 
            for(int i = 0; i < sLen; i++) {
                if(count < wLen && s.charAt(i) == word.charAt(count)) {
                    ++count;
                }
            }
            
            if(count == wLen && longestWord.length() <= wLen) {
                if(longestWord.length() < wLen || longestWord.compareTo(word) > 0) {
                    longestWord = word;
                }
            }
        }
        return longestWord;
    }
}
~~~



## Further

https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/discuss/99588/Short-Java-Solutions-Sorting-Dictionary-and-Without-Sorting