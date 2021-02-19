## Description

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or `-1` if `needle` is not part of `haystack`.

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

 

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

**Example 3:**

```
Input: haystack = "", needle = ""
Output: 0
```

 

**Constraints:**

- `0 <= haystack.length, needle.length <= 5 * 104`
- `haystack` and `needle` consist of only lower-case English characters.

## Thinking

Brute force is OK and may be better but I still try KMP. And I totally got fxxked up

## Solutions

~~~java
class Solution {
    public int strStr(String haystack, String needle) {
        int len1 = haystack.length(), len2 = needle.length();
        if(len2 == 0) return 0;
        else if(len1 == 0) return -1;
        int[] next = KMP(needle.toCharArray());
        for(int i = 0, j = 0; i < len1 && j < len2; ) {
            if(haystack.charAt(i) == needle.charAt(j)) {
                if(j == len2 - 1) return i - len2 + 1;
                ++i;
                ++j;
            } else if(j != 0) {
                j = next[j - 1];
            } else {
                ++i;
            }
            System.out.println(i  + "   " + j);
        }
        return -1;
    }
    
    public int[] KMP(char[] needleArr) {
        int len = needleArr.length;
        int[] res = new int[len];
        int i = 1, tempLen = 0;
        res[0] = 0;
        while(i < len) {
            if(needleArr[i] == needleArr[tempLen]) {
                res[i++] = ++tempLen;
            } else if(tempLen != 0) {
                tempLen = res[tempLen - 1];
            } else {
                res[i++] = tempLen;
            }
        }
        return res;
    }
}
~~~



## Further

https://leetcode.com/problems/implement-strstr/discuss/12886/Accepted-KMP-solution-in-java-for-reference

https://www.geeksforgeeks.org/java-program-for-kmp-algorithm-for-pattern-searching-2/

http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html

https://leetcode.com/problems/implement-strstr/discuss/12807/Elegant-Java-solution