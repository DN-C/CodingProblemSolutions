## Description

Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

**Example 1:**
Input:

```
"bbbab"
```

Output:

```
4
```

One possible longest palindromic subsequence is "bbbb".

 

**Example 2:**
Input:

```
"cbbd"
```

Output:

```
2
```

One possible longest palindromic subsequence is "bb".

 

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consists only of lowercase English letters.

## Thinking

dp

## Solutions

~~~java
class Solution {
    public int longestPalindromeSubseq(String s) {
        int len = s.length();
        int dp[][] = new int[len][len];
        for(int i = 0; i < len; i++) {
            dp[i][i] = 1;
        }
        for(int i = len - 1;i >= 0; i--) {
            for(int j = i + 1; j < len; j++) {
                if(s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i + 1][j]);
                }
            }
        }
        return dp[0][len - 1];
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E5%AD%90%E5%BA%8F%E5%88%97%E9%97%AE%E9%A2%98%E6%A8%A1%E6%9D%BF.md