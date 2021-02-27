## Description

There are some spherical balloons spread in two-dimensional space. For each balloon, provided input is the start and end coordinates of the horizontal diameter. Since it's horizontal, y-coordinates don't matter, and hence the x-coordinates of start and end of the diameter suffice. The start is always smaller than the end.

An arrow can be shot up exactly vertically from different points along the x-axis. A balloon with `xstart` and `xend` bursts by an arrow shot at `x` if `xstart ≤ x ≤ xend`. There is no limit to the number of arrows that can be shot. An arrow once shot keeps traveling up infinitely.

Given an array `points` where `points[i] = [xstart, xend]`, return *the minimum number of arrows that must be shot to burst all balloons*.

 

**Example 1:**

```
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: One way is to shoot one arrow for example at x = 6 (bursting the balloons [2,8] and [1,6]) and another arrow at x = 11 (bursting the other two balloons).
```

**Example 2:**

```
Input: points = [[1,2],[3,4],[5,6],[7,8]]
Output: 4
```

**Example 3:**

```
Input: points = [[1,2],[2,3],[3,4],[4,5]]
Output: 2
```

**Example 4:**

```
Input: points = [[1,2]]
Output: 1
```

**Example 5:**

```
Input: points = [[2,3],[2,3]]
Output: 1
```

 

**Constraints:**

- `0 <= points.length <= 104`
- `points[i].length == 2`
- `-231 <= xstart < xend <= 231 - 1`

## Thinking

Greedy, similar to No.435

Notice that one specific test case( [[-2147483646,-2147483645],[2147483646,2147483647]] ) lead to the difference of Arrays.sort part between this solution and the one from No.435

## Solutions

~~~java
class Solution {
    public int findMinArrowShots(int[][] points) {
        if(points == null || points.length == 0) return 0;
        Arrays.sort(points, (a,b) -> a[1] > b[1] ? 1 : -1);
        int len = points.length;
        int count = 0, tmp = 0;
        for(int i = 1; i < len; i++) {
            if(points[i][0] <= points[tmp][1]) count++;
            else tmp = i;
        }
        return len - count;
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95%E4%B9%8B%E5%8C%BA%E9%97%B4%E8%B0%83%E5%BA%A6%E9%97%AE%E9%A2%98.md