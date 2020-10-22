## Description

Given a list of `intervals`, remove all intervals that are covered by another interval in the list.

Interval `[a,b)` is covered by interval `[c,d)` if and only if `c <= a` and `b <= d`.

After doing so, return *the number of remaining intervals*.

 

**Example 1:**

```
Input: intervals = [[1,4],[3,6],[2,8]]
Output: 2
Explanation: Interval [3,6] is covered by [2,8], therefore it is removed.
```

**Example 2:**

```
Input: intervals = [[1,4],[2,3]]
Output: 1
```

**Example 3:**

```
Input: intervals = [[0,10],[5,12]]
Output: 2
```

**Example 4:**

```
Input: intervals = [[3,10],[4,10],[5,11]]
Output: 2
```

**Example 5:**

```
Input: intervals = [[1,2],[1,4],[3,4]]
Output: 1
```

 

**Constraints:**

- `1 <= intervals.length <= 1000`
- `intervals[i].length == 2`
- `0 <= intervals[i][0] < intervals[i][1] <= 10^5`
- All the intervals are **unique**.

## Thinking

Sort the given arrays' left in ascending, and if left equals, sort by right in descending. With the sorted arrays, any array would not be covered by any other one on its right side., it can be only covered by arrays on its left. 

Set an Integer to memorize the right border, default -1. If one arrays' right border larger than that, it can be considered as uncovered one, then add 1 in result, and update the right value.

## Solutions

~~~java
class Solution {
    public int removeCoveredIntervals(int[][] intervals) {
        if (intervals.length == 0) return 0;
        int right = -1, res = 0;
        Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? b[1] - a[1] : a[0] - b[0]);
        for (int intv[] : intervals) {
            if (intv[1] > right) {
                res++;
                right = intv[1];
            }
        }
        return res;
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie-qing-an-shun-xu-yue-du/qu-jian-wen-ti-he-ji

https://leetcode.com/problems/remove-covered-intervals/discuss/451277/JavaC%2B%2BPython-Sort-Solution