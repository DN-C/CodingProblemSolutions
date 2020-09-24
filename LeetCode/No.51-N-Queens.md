## Description

The *n*-queens puzzle is the problem of placing *n* queens on an *n*×*n* chessboard such that no two queens attack each other.

![](../Resources/Images/No.51-1.png)

Given an integer *n*, return all distinct solutions to the *n*-queens puzzle.

Each solution contains a distinct board configuration of the *n*-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space respectively.

**Example:**

```
Input: 4
Output: [
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above.
```



## Thinking

1. Backtrack

## Solutions

~~~java
// Solution 1 
class Solution {
    List<List<String>> result = new ArrayList<>();
    
    public List<List<String>> solveNQueens(int n) {
        char[][] rows = new char[n][];
        backtrack(rows, n, 0);
        return result;
    }
    
    public void backtrack(char[][] rows, int n, int size) {
        if (size == n) {
            List<String> oneSolution = new ArrayList<String>();
            for (char[] row : rows) {
                String rowString = new String(row);
                oneSolution.add(rowString);
            }
            result.add(oneSolution);
            return;
        }
        
        char[] row = new char[n];
        Arrays.fill(row, '.');
        
        if (size == 0) {
            for(int i = 0; i < n; i++) {
                row[i] = 'Q';
                char[] tempRow = row.clone();
                rows[size] = tempRow;
                backtrack(rows, n, size + 1);
                row[i] = '.';
            }
        } else {
            HashSet<Integer> set = new HashSet<Integer>();
            for(int i = 0; i < size ; i++) {
                String rowString = new String(rows[i]);
                int index = rowString.indexOf('Q');
                int temp = size - i;
                set.add(index);
                if (index + temp <= n - 1) set.add(index + temp);
                if (index - temp >= 0) set.add(index - temp);
                
            }
            for(int i = 0; i < n; i++) {
                if (set.contains(i)) continue;
                row[i] = 'Q';
                char[] tempRow = row.clone();
                rows[size] = tempRow;
                backtrack(rows, n, size + 1);
                row[i] = '.';
            }
        }
        
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hui-su-suan-fa-xiang-jie-xiu-ding-ban