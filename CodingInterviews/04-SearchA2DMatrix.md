## Description

Write an efficient algorithm that searches for a value in an *m* x *n* matrix. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example:**

Consider the following matrix:

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = `5`, return `true`.

Given target = `20`, return `false`.



## Thinking

从右上角（或者左下角）开始判断，小于则向下，大于则向右，逐渐向中间“挤压”，时间复杂度O(M+N)



## Solutions

~~~java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }
        
        int cow = matrix.length;
        int rol = matrix[0].length;
        int i = 0;
        int j = rol - 1;
        while(j >= 0 && i < cow) {
            int num = matrix[i][j];
            
            if (num == target) {
                return true;
            }
            
            if (num < target) {
                i++;
            } else {
                j--;
            }
        }
        
        return false;
    }
}
~~~





## Further

[空对象模式](https://www.google.com/search?q=空对象模式)