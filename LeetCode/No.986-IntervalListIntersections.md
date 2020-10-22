## Description

Given two lists of **closed** intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

*(Formally, a closed interval `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`. The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval. For example, the intersection of [1, 3] and [2, 4] is [2, 3].)*

 

**Example 1:**

**![img](../Resources/Images/No.986-1.png)**

```
Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```

 

**Note:**

1. `0 <= A.length < 1000`
2. `0 <= B.length < 1000`
3. `0 <= A[i].start, A[i].end, B[i].start, B[i].end < 10^9`

## Thinking

1.  loot arrays in A, and compare each of them with the whole B to find out intersection. Slow but easy to understand lol 
2. Use to pointer to follow A and B.

## Solutions

~~~java
// Solution 1, dumpest one lol
class Solution {
    public int[][] intervalIntersection(int[][] A, int[][] B) {
        if (A.length == 0 || B.length == 0) return new int[][] {};
        List<int []> res = new ArrayList<int []>();
        for(int range1[] : A) {
            for (int range2[] : B) {
                if (range2[0] > range1[1]) break; 
                if (range2[1] < range1[0]) continue;
                res.add(new int[] {Math.max(range1[0], range2[0]), Math.min(range1[1], range2[1])});
            }
        }
        return res.toArray(new int[res.size()][]);
    }
}

// Solution 2 inspried by I93@LeetCode
class Solution {
    public int[][] intervalIntersection(int[][] A, int[][] B) {
        if (A.length == 0 || B.length == 0) return new int[][] {};
        List<int []> res = new ArrayList<int []>();
        int pointerA = 0, pointerB = 0, lenA = A.length, lenB = B.length;
        while(pointerA < lenA && pointerB < lenB) {
            int left = Math.max(A[pointerA][0], B[pointerB][0]);
            int right = Math.min(A[pointerA][1], B[pointerB][1]); 
            if (left <= right) res.add(new int[] {left, right});
            if (A[pointerA][1] > B[pointerB][1]) pointerB++;
            else pointerA++;
        }
        return res.toArray(new int[res.size()][]);
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie-qing-an-shun-xu-yue-du/qu-jian-wen-ti-he-ji

https://leetcode.com/problems/interval-list-intersections/discuss/276324/Simple-JAVA-two-pointer