## Description

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

 

**Example 1:**

```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

 

**Constraints:**

- `1 <= n <= 45`

## Thinking

DP, similar to [No.509-FibonacciNumber](./No.509-FibonacciNumber.md)

## Solutions

~~~java
//O(n) space
class Solution {
    public int climbStairs(int n) {
        if(n == 1) return 1;
        if(n == 2) return 2;
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for(int i = 3; i <= n; ++i) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
        
    }
}

//O(1) space
class Solution {
    public int climbStairs(int n) {
        if(n == 1) return 1;
        if(n == 2) return 2;
        int dp_1 = 1;
        int dp_2 = 2;
        int dp_3 = 0;
        for(int i = 3; i <= n; ++i) {
            dp_3 = dp_1 + dp_2;
            dp_1 = dp_2;
            dp_2 = dp_3;
        }
        return dp_3;
        
    }
}
~~~



## Further

[link](https://leetcode.com/problems/climbing-stairs/discuss/25299/Basically-it's-a-fibonacci.)