## Description

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete at most *two* transactions.

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

 

**Example 1:**

```
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```

**Example 2:**

```
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3:**

```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

**Example 4:**

```
Input: prices = [1]
Output: 0
```

 

**Constraints:**

- `1 <= prices.length <= 105`
- `0 <= prices[i] <= 105`

## Thinking

DP Table of the f course

## Solutions

~~~java
// Solution 1
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length <= 1) return 0;
        int dptable[][][] = new int[prices.length][3][2];
        
        for (int i = 0, len = prices.length; i < len; i++) {
            if (i == 0) {
                dptable[i][0][0] = 0;
                dptable[i][0][1] = -prices[i];
                dptable[i][1][0] = 0;
                dptable[i][1][1] = -prices[i];
                dptable[i][2][0] = 0;
                dptable[i][2][1] = -prices[i];
                continue;
            }
            for (int j = 1; j < 3; j++) {
                dptable[i][j][0] = Math.max(dptable[i - 1][j][0], dptable[i - 1][j][1] + prices[i]);
                if (j == 1) dptable[i][j][1] = Math.max(dptable[i - 1][j][1], -prices[i]);
                else dptable[i][j][1] = Math.max(dptable[i - 1][j][1], dptable[i - 1][j - 1][0] - prices[i]);
            }
        }
        return dptable[prices.length - 1][2][0];
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie-qing-an-shun-xu-yue-du/tuan-mie-gu-piao-wen-ti