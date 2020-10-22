## Description

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

- You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
- After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

**Example:**

```
Input: [1,2,3,0,2]
Output: 3 
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

## Thinking

DP Table

## Solutions

~~~java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length <= 1) return 0;
        int len = prices.length;
        int dptable[][] = new int[len][2];
        for (int i = 0; i < len; i++) {
            if (i - 1 == -1) {
                dptable[i][0] = 0;
                dptable[i][1] = -prices[i];
            } else {
                dptable[i][0] = Math.max(dptable[i - 1][0], dptable[i - 1][1] + prices[i]);
                if (i - 2 == -1) dptable[i][1] = Math.max(dptable[i - 1][1], -prices[i]);
                else dptable[i][1] = Math.max(dptable[i - 1][1], dptable[i - 2][0] - prices[i]);
            }
        }
        return dptable[len - 1][0];
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie-qing-an-shun-xu-yue-du/tuan-mie-gu-piao-wen-ti