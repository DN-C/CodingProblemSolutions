## Description

Given a collection of intervals, merge all overlapping intervals.

**Example 1:**

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

 

**Constraints:**

- `intervals[i][0] <= intervals[i][1]`

## Thinking

Similar to No.1288. Sort the array in ascending. Use two integers left and right to memorize border. Loop arrays. If left border is larger than left value, consider the left and right could be an array in result. Otherwise just merge this array in by changing the right value. When exit the loop, don't forget to add one more array to result.

## Solutions

~~~java
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals.length == 0) return new int[intervals.length][];
        Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        int right = intervals[0][1], left = intervals[0][0];
        List<int []> res = new ArrayList<int []>();
        for(int intv[] : intervals) {
            if (intv[0] > right) {
                res.add(new int[] {left, right});
                left = intv[0];
                right = intv[1];
                continue;
            }
            right = Math.max(right, intv[1]);
        }
        res.add(new int[] {left, right});
        return res.toArray(new int[res.size()][]);
    }
}
~~~



## Further

https://leetcode.com/problems/merge-intervals/discuss/21222/A-simple-Java-solution

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie-qing-an-shun-xu-yue-du/qu-jian-wen-ti-he-ji