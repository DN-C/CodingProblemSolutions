## Description

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Design an algorithm to find the maximum profit. You may complete at most `k` transactions.

**Notice** that you may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

 

**Example 1:**

```
Input: k = 2, prices = [2,4,1]
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
```

**Example 2:**

```
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
```

 

**Constraints:**

- `0 <= k <= 109`
- `0 <= prices.length <= 104`
- `0 <= prices[i] <= 1000`

## Thinking

DP Table, when k > n / 2, just consider n == inf

## Solutions

~~~java
class Solution {
    public int maxProfit(int k, int[] prices) {
        if (prices.length <= 1 || k == 0) return 0;
        int len = prices.length;
        if (k >= (len >> 1)) {
            int price = 0;
            for(int i = 1; i < len; i++) {
                if (prices[i] - prices[i - 1] > 0) price += prices[i] - prices[i - 1];
            }
            return price;
        }
        int dptable[][][] = new int[len][k + 1][2];
        for(int i = 0; i < len; i++) {
            if (i == 0) {
                for(int j = 1; j <= k; j++) {
                    dptable[i][j][0] = 0;
                    dptable[i][j][1] = -prices[i];
                }
                continue;
            }
            for(int j = 1; j <= k; j++) {
                dptable[i][j][0] = Math.max(dptable[i - 1][j][0], dptable[i - 1][j][1] + prices[i]);
                if (j == 1) dptable[i][j][1] = Math.max(dptable[i - 1][j][1], -prices[i]);
                else dptable[i][j][1] = Math.max(dptable[i - 1][j][1], dptable[i - 1][j - 1][0] - prices[i]);
            }
        }
         return dptable[len - 1][k][0];
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie-qing-an-shun-xu-yue-du/tuan-mie-gu-piao-wen-ti

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/discuss/54113/A-Concise-DP-Solution-in-Java