## Description

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

 

**Example 1:**

![img](..\Resources\Images\No.59-SpiralMatrixII\spiraln.jpg)

```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

**Example 2:**

```
Input: n = 1
Output: [[1]]
```

 

**Constraints:**

- `1 <= n <= 20`

## Thinking



## Solutions

~~~java
class Solution {
    public int[][] generateMatrix(int n) {
        int matrix[][] = new int[n][n];
        int count = 1, i = 0, j = 0, dir = 0, end = n * n + 1;
        while(count < end) {
            if(dir == 0) {
                while(j < n && matrix[i][j] == 0) {
                    matrix[i][j] = count;
                    count++;
                    j++;
                }
                j--;
                i++;
                dir = 1;
            }
            
            if(dir == 1) {
                while(i < n && matrix[i][j] == 0) {
                    matrix[i][j] = count;
                    count++;
                    i++;
                }
                i--;
                j--;
                dir = 2;
            }
            
            if(dir == 2) {
                while(j >= 0 && matrix[i][j] == 0) {
                    matrix[i][j] = count;
                    count++;
                    j--;
                }
                j++;
                i--;
                dir = 3;
            }
            
            if(dir == 3) {
                while(i >= 0 && matrix[i][j] == 0) {
                    matrix[i][j] = count;
                    count++;
                    i--;
                }
                i++;
                j++;
                dir = 0;
            }
        }
        return matrix;
    }
}
~~~



## Further

https://leetcode.com/problems/spiral-matrix-ii/discuss/22289/My-Super-Simple-Solution.-Can-be-used-for-both-Spiral-Matrix-I-and-II