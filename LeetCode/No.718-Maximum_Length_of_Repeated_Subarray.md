## Description

Given two integer arrays `A` and `B`, return the maximum length of an subarray that appears in both arrays.

**Example 1:**

```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

 

**Note:**

1. 1 <= len(A), len(B) <= 1000
2. 0 <= A[i], B[i] < 100

## Thinking

DP, dp[i] [j] represent the length of max sub array end with A[i] and B[j]

## Solutions

~~~java
class Solution {
    public int findLength(int[] A, int[] B) {
        int[][] dp = new int[A.length][B.length];
        int maxLen = 0;
        for(int i = 0 ; i < A.length; ++i) {
            for(int j = 0; j < B.length; ++j) {
                if(i == 0 || j == 0) dp[i][j] = A[i] == B[j] ? 1 : 0;
                else dp[i][j] = A[i] == B[j] ? dp[i - 1][j - 1] + 1 : 0;
                maxLen = Math.max(dp[i][j], maxLen);
            }
        }
        return maxLen;
    }
}
~~~



## Further

