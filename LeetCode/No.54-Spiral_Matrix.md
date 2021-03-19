## Description

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

 

**Example 1:**

![img](../Resources/Images/No.54-Spiral_Matrix/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

![img](../Resources/Images/No.54-Spiral_Matrix/spiral.jpg)

```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

 

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

## Thinking

Iterate the matrix in required order, then return it.

## Solutions

~~~java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int m = matrix.length, n = matrix[0].length, i = 0, j = 0;
        int dir = 0; // 0-right, 1-down, 2-left, 3-up
        boolean[][] visited = new boolean[m][n];
        List<Integer> res = new ArrayList<Integer>();
        res.add(matrix[0][0]);
        visited[0][0] = true;
        while(res.size() < m * n) {
            switch(dir) {
                case 0:
                    if(j + 1 >= n || visited[i][j + 1]) {
                        dir = 1;
                        break;
                    }
                    res.add(matrix[i][j + 1]);
                    visited[i][j + 1] = true;
                    ++j;
                    break;
                case 1:
                    if(i + 1 >= m || visited[i + 1][j]) {
                        dir = 2;
                        break;
                    }
                    res.add(matrix[i + 1][j]);
                    visited[i + 1][j] = true;
                    ++i;
                    break;
                case 2:
                    if(j - 1 < 0 || visited[i][j - 1]) {
                        dir = 3;
                        break;
                    }
                    res.add(matrix[i][j - 1]);
                    visited[i][j - 1] = true;
                    --j;
                    break;
                case 3:
                    if(i - 1 < 0 || visited[i - 1][j]) {
                        dir = 0;
                        break;
                    }
                    res.add(matrix[i - 1][j]);
                    visited[i - 1][j] = true;
                    --i;
                    break;
                default:
                    break;
            }
        }
        return res;
    }
}
~~~



## Further

https://leetcode.com/problems/spiral-matrix/discuss/20599/Super-Simple-and-Easy-to-Understand-Solution