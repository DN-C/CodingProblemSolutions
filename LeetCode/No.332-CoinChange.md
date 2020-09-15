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

1. DP + Bottom-up
2. recursive + reminder

## Solutions

~~~java
// Solution 1
// DO NOT USE HASHMAP HERE! I SHOULDN'T USE IT, AN ARRAY IS ENOUGH! 
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
            coinCounts = Integer.MAX_VALUE;
            for(int coin : coins) {
                if (sum - coin < 0) continue;
                if (cache.get(sum - coin) == Integer.MAX_VALUE) continue;
                coinCounts = coinCounts < cache.get(sum - coin) + 1 ? coinCounts : cache.get(sum - coin) + 1;
            }
            cache.put(sum, coinCounts);
            sum++;
        }
        if (cache.get(amount) == Integer.MAX_VALUE) return -1;
        return cache.get(amount);
    }
}

// Solution 2 from @ElementNotFoundException
public class Solution {
public int coinChange(int[] coins, int amount) {
    if(amount<1) return 0;
    return helper(coins, amount, new int[amount]);
}

private int helper(int[] coins, int rem, int[] count) { // rem: remaining coins after the last step; count[rem]: minimum number of coins to sum up to rem
    if(rem<0) return -1; // not valid
    if(rem==0) return 0; // completed
    if(count[rem-1] != 0) return count[rem-1]; // already computed, so reuse
    int min = Integer.MAX_VALUE;
    for(int coin : coins) {
        int res = helper(coins, rem-coin, count);
        if(res>=0 && res < min)
            min = 1+res;
    }
    count[rem-1] = (min==Integer.MAX_VALUE) ? -1 : min;
    return count[rem-1];
}
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/dong-tai-gui-hua-xiang-jie-jin-jie

[AND HERE](https://leetcode.com/problems/coin-change/discuss/77368/*Java*-Both-iterative-and-recursive-solutions-with-explanations)