## Description

Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.



 

**Example 1:**

```
Input: [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of intervals are non-overlapping.
```

**Example 2:**

```
Input: [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to make the rest of intervals non-overlapping.
```

**Example 3:**

```
Input: [[1,2],[2,3]]
Output: 0
Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
```

 

**Note:**

1. You may assume the interval's end point is always bigger than its start point.
2. Intervals like [1,2] and [2,3] have borders "touching" but they don't overlap each other.

## Thinking

Greedy

## Solutions

~~~java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        if(intervals == null || intervals.length == 0) return 0;
        Arrays.sort(intervals, (a,b) -> a[1] - b[1]);
        int len = intervals.length;
        int i = 0, count = 0;
        while(i < len - 1) {
            int tmp = i;
            while(i < len - 1 && intervals[++i][0] < intervals[tmp][1]) ++count;
        }
        return count;
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95%E4%B9%8B%E5%8C%BA%E9%97%B4%E8%B0%83%E5%BA%A6%E9%97%AE%E9%A2%98.md

https://leetcode.com/problems/non-overlapping-intervals/discuss/282743/Java-updated-solution-based-on-the-top-voted-post