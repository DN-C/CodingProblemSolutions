## Description

Given two strings `word1` and `word2`, return *the minimum number of operations required to convert `word1` to `word2`*.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

 

**Example 1:**

```
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

**Example 2:**

```
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

 

**Constraints:**

- `0 <= word1.length, word2.length <= 500`
- `word1` and `word2` consist of lowercase English letters.

## Thinking

DP Table

## Solutions

~~~java
class Solution {
    public int minDistance(String word1, String word2) {
        int len1 = word1.length(), len2 = word2.length();
        int dptable[][] = new int[len1 + 1][len2 + 1];
        for(int i = 1; i <= len1; i++) {
            dptable[i][0] = i;
        }
        for(int i = 1; i <= len2; i++) {
            dptable[0][i] = i;
        }
        
        for(int counter1 = 1; counter1 <= len1; counter1++){
            for(int counter2 = 1; counter2 <= len2; counter2++) {
                if(word1.charAt(counter1 - 1) == word2.charAt(counter2 - 1)) {
                    dptable[counter1][counter2] = dptable[counter1 - 1][counter2 - 1];
                } else {
                    dptable[counter1][counter2] = Math.min(dptable[counter1][counter2 - 1] + 1, Math.min(dptable[counter1 - 1][counter2] + 1, dptable[counter1 - 1][counter2 - 1] + 1));
                }
            }
        }
        
        return dptable[len1][len2];
        
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E7%BC%96%E8%BE%91%E8%B7%9D%E7%A6%BB.md