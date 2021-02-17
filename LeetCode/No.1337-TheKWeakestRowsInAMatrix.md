## Description

Given a `m * n` matrix `mat` of *ones* (representing soldiers) and *zeros* (representing civilians), return the indexes of the `k` weakest rows in the matrix ordered from the weakest to the strongest.

A row ***i*** is weaker than row ***j***, if the number of soldiers in row ***i*** is less than the number of soldiers in row ***j***, or they have the same number of soldiers but ***i*** is less than ***j***. Soldiers are **always** stand in the frontier of a row, that is, always *ones* may appear first and then *zeros*.

 

**Example 1:**

```
Input: mat = 
[[1,1,0,0,0],
 [1,1,1,1,0],
 [1,0,0,0,0],
 [1,1,0,0,0],
 [1,1,1,1,1]], 
k = 3
Output: [2,0,3]
Explanation: 
The number of soldiers for each row is: 
row 0 -> 2 
row 1 -> 4 
row 2 -> 1 
row 3 -> 2 
row 4 -> 5 
Rows ordered from the weakest to the strongest are [2,0,3,1,4]
```

**Example 2:**

```
Input: mat = 
[[1,0,0,0],
 [1,1,1,1],
 [1,0,0,0],
 [1,0,0,0]], 
k = 2
Output: [0,2]
Explanation: 
The number of soldiers for each row is: 
row 0 -> 1 
row 1 -> 4 
row 2 -> 1 
row 3 -> 1 
Rows ordered from the weakest to the strongest are [0,2,3,1]
```

 

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `2 <= n, m <= 100`
- `1 <= k <= m`
- `matrix[i][j]` is either 0 **or** 1.

## Thinking

Heap + Binary Search

(Btw, this question should be a medium...)

## Solutions

~~~java
class Solution {
    public int[] kWeakestRows(int[][] mat, int k) {
        int len = mat.length;
        if(len == 1) {
            return new int[]{0};  
        } 
        PriorityQueue<int[]> heap = new PriorityQueue<int[]>((a, b) -> a[0] == b[0] ? b[1] - a[1] : b[0] - a[0]);
        for(int i = 0; i < len; i++) {
            heap.offer(new int[] {numOfOne(mat[i]), i});
            if(heap.size() > k) {
                heap.poll();   
            }
        }
        int res[] = new int[k];
        for(int i = k - 1; i >= 0; i--) {
            res[i] = heap.poll()[1];
        }
        return res;
    }
    
    public int numOfOne(int row[]) {
        int left = 0, right = row.length;
        while(left < right) {
            int mid = left + (right - left) / 2;
            if(row[mid] == 1) {
                ++left;
            } else if(row[mid] != 1) {
                right = mid;
            }
        }
        return left + 1;
    }
}
~~~



## Further

https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/discuss/496555/Java-Best-Solution-100-TimeSpace-Binary-Search-%2B-Heap