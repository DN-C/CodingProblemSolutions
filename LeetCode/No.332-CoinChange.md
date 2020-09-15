## Description

You are given coins of different denominations and a total amount of money *amount*. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example 1:**

```
Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1
```

**Note**:
You may assume that you have an infinite number of each kind of coin.

## Thinking



## Solutions

~~~java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins.length == 0 || amount < 0) return -1;
        int sum = 0;
        int coinCounts = Integer.MAX_VALUE;
        HashMap<Integer, Integer> cache = new HashMap<Integer, Integer>();
        while (sum <= amount) {
            if (sum == 0) {
                cache.put(sum, 0); 
                sum++;
                continue;
            }
            coinCounts = Integer.MAX_VALUE - 1;
            for(int coin : coins) {
                if (sum - coin < 0) {
                    coinCounts++;
                    continue;
                }
                coinCounts = coinCounts < cache.get(sum - coin) + 1 ? coinCounts : cache.get(sum - coin) + 1;
            }
            cache.put(sum, coinCounts);
            sum++;
        }
        if (cache.get(amount) == Integer.MAX_VALUE) return -1;
        return cache.get(amount);
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/dong-tai-gui-hua-xiang-jie-jin-jie