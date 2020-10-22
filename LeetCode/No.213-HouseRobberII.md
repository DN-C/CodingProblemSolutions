## Description

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

 

**Example 1:**

```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
```

**Example 2:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

**Example 3:**

```
Input: nums = [0]
Output: 0
```

 

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

## Thinking

DP Table, check house robber (No.198) first.

you can rob the final house or not depends on if you rob the first house, so you rob the first one and don't rob the final one, or you don't rob the first one and rob the final one. The max profit is the max one of the above two way.

## Solutions

~~~java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if (len == 0) return 0;
        if (len == 1) return nums[0];
        if (len == 2) return Math.max(nums[0], nums[1]);
        return Math.max(robSub(0, len - 2, nums), robSub(1, len - 1, nums));    
    }
    
    public int robSub(int low, int high, int nums[]) {
        int dptable[] = new int[high + 1];
        for (int i = low; i <= high; i++) {
            if (i - 1 == low -1) dptable[i] = nums[i];
            else if (i - 2 == low -1) dptable[i] = Math.max(nums[i - 1], nums[i]);
            else dptable[i] = Math.max(dptable[i - 1], dptable[i - 2] + nums[i]);
        }
        return dptable[high];
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E6%8A%A2%E6%88%BF%E5%AD%90.md

https://leetcode.com/problems/house-robber-ii/discuss/59934/Simple-AC-solution-in-Java-in-O(n)-with-explanation