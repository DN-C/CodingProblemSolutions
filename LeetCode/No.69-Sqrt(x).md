## Description

Given a non-negative integer `x`, compute and return *the square root of* `x`.

Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.

 

**Example 1:**

```
Input: x = 4
Output: 2
```

**Example 2:**

```
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.
```

 

**Constraints:**

- `0 <= x <= 231 - 1`

## Thinking

1. Binary Search'
2. Newton, go check Further part.

## Solutions

~~~java
class Solution {
    public int mySqrt(int x) {
        int left = 1, right = x / 2;
        while(left < right) {
            int mid = left + (right - left) / 2;
            if(Math.floor(x / mid) == mid) return mid;
            else if(Math.floor(x / mid) < mid) right = mid;
            else left = mid + 1;
        }
        return x / left < left ? left - 1 : left;
    }
}
~~~



## Further

https://leetcode.com/problems/sqrtx/discuss/25047/A-Binary-Search-Solution

https://leetcode.com/problems/sqrtx/discuss/25057/3-4-short-lines-Integer-Newton-Every-Language

https://leetcode.com/problems/sqrtx/discuss/25048/Share-my-O(log-n)-Solution-using-bit-manipulation