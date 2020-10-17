## Description

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

**Example 2:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

## Thinking

Dynamic Programing(dp table)

## Solutions

~~~java
//Solution 1
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0 ) return 0;
        int dptable[][][] = new int[prices.length][2][2];
        
        
        for(int i = 0; i < prices.length; i++) {
            for(int j = 1; j > 0; j--) {
                if (i - 1 < 0) {
                    dptable[i][j][0] = 0;
                    dptable[i][j][1] = -prices[i];
                    continue;
                }
                dptable[i][j][0] = Math.max(dptable[i - 1][j][0], dptable[i - 1][j][1] + prices[i]);
                dptable[i][j][1] = Math.max(dptable[i - 1][j][1], dptable[i - 1][j - 1][0] - prices[i]);
            }
        }
        return dptable[prices.length - 1][1][0];
    }
}

//Solution 2
//Basically the same one as Solution 1, but Space O(1)
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0 ) return 0;
        int dp_i_0 = 0, dp_i_1 = Integer.MIN_VALUE;
        
        for(int i = 0; i < prices.length; i++) {
            dp_i_0 = Math.max(dp_i_0, dp_i_1 + prices[i]);
            dp_i_1 = Math.max(dp_i_1, -prices[i]);
        }
        return dp_i_0;
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/tuan-mie-gu-piao-wen-ti