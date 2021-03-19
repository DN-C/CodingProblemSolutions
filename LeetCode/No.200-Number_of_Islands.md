## Description

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

 

**Example 1:**

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

**Example 2:**

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

 

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

## Thinking

1. Iterate all places in grid. When grid[i] [j] == '1', check if it is connected with any exist islands, other create a new island(Use a hashmap to store). CAN NOT PASS ALL TEST CASES.
2. DFS. Credited to @wcyz666
3. BFS.

## Solutions

~~~java
// Can not pass all cases. 47/48. Don't know why...
class Solution {
    public int numIslands(char[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dir = new int[][] {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        List<HashSet<List<Integer>>> list = new ArrayList<>();
        for(int i = 0; i < m; ++i) {
            for(int j = 0; j < n; ++j) {
                int isPut = -1;
                if(grid[i][j] == '0') {
                    continue;
                }
                
                for(int x = 0; x < list.size(); ++x) {
                    for(int y = 0; y < 4; ++y) {
                        int a = i + dir[y][0], b = j + dir[y][1];
                        if(a < 0 || a >= m || b < 0 || b >= n) {
                            continue;
                        }
                        if(grid[a][b] == '0') {
                            continue;
                        }
                        ArrayList<Integer> temp = new ArrayList<Integer>();
                        temp.add(a);
                        temp.add(b);
                        if(list.get(x).contains(temp)) {
                            if(isPut != -1) {
                                if(isPut == x) {
                                    continue;
                                }
                                list.get(x).addAll(list.get(isPut));
                                list.remove(isPut);
                                --x;
                            } else {
                                temp.clear();
                                temp.add(i);
                                temp.add(j);
                                list.get(x).add(temp);
                                isPut = x;
                            }
                        }
                    }
                }
                if(isPut == -1) {
                    ArrayList<Integer> temp = new ArrayList<Integer>();
                    temp.add(i);
                    temp.add(j);
                    list.add(new HashSet<List<Integer>>());
                    list.get(list.size() - 1).add(temp);
                }
            }
        }
        
        return list.size();
    }
}


~~~



## Further

https://leetcode.com/problems/number-of-islands/discuss/56359/Very-concise-Java-AC-solution

https://leetcode.com/problems/number-of-islands/discuss/56338/Java-DFS-and-BFS-solution