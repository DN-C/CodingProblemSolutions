## Description

You are given `K` eggs, and you have access to a building with `N` floors from `1` to `N`. 

Each egg is identical in function, and if an egg breaks, you cannot drop it again.

You know that there exists a floor `F` with `0 <= F <= N` such that any egg dropped at a floor higher than `F` will break, and any egg dropped at or below floor `F` will not break.

Each *move*, you may take an egg (if you have an unbroken one) and drop it from any floor `X` (with `1 <= X <= N`). 

Your goal is to know **with certainty** what the value of `F` is.

What is the minimum number of moves that you need to know with certainty what `F` is, regardless of the initial value of `F`?

 



**Example 1:**

```
Input: K = 1, N = 2
Output: 2
Explanation: 
Drop the egg from floor 1.  If it breaks, we know with certainty that F = 0.
Otherwise, drop the egg from floor 2.  If it breaks, we know with certainty that F = 1.
If it didn't break, then we know with certainty F = 2.
Hence, we needed 2 moves in the worst case to know what F is with certainty.
```

**Example 2:**

```
Input: K = 2, N = 6
Output: 3
```

**Example 3:**

```
Input: K = 3, N = 14
Output: 4
```

 

**Note:**

1. `1 <= K <= 100`
2. `1 <= N <= 10000`

## Thinking

dp + memo

## Solutions

~~~java
// Time limit exceeded. Need improving
class Solution {
    public int superEggDrop(int K, int N) {
        int memo[][] = new int[K + 1][N + 1];
        return helper(K, N, memo);
    }
    
    public int helper(int K, int N, int memo[][]) {
        if (K == 1) return N;
        if (N == 0) return 0;
        if (memo[K][N] > 0) return memo[K][N];
        int res = Integer.MAX_VALUE;
        for(int j = 1; j <= N; j++) {
            res = Math.min(res, Math.max(helper(K - 1, j - 1, memo), helper(K, N - j, memo)) + 1);
        }
        memo[K][N] = res;
        return res;
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E9%AB%98%E6%A5%BC%E6%89%94%E9%B8%A1%E8%9B%8B%E9%97%AE%E9%A2%98.md