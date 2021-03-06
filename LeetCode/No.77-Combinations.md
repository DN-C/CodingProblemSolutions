## Description

Given two integers *n* and *k*, return all possible combinations of *k* numbers out of 1 ... *n*.

You may return the answer in **any order**.

 

**Example 1:**

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**Example 2:**

```
Input: n = 1, k = 1
Output: [[1]]
```

 

**Constraints:**

- `1 <= n <= 20`
- `1 <= k <= n`

## Thinking

Backtrack

## Solutions

~~~java
class Solution {
    
    private List<List<Integer>> res;
    
    public List<List<Integer>> combine(int n, int k) {
        res = new ArrayList<List<Integer>>();
        backtrack(1, n + 1, k, new ArrayList<Integer>());
        return res;
    }
    
    public void backtrack(int index, int n, int k, ArrayList<Integer> list) {
        if(k == 0) res.add(new ArrayList<Integer>(list));
        for(int i = index; i < n; i++) {
            list.add(i);
            backtrack(i + 1, n, k - 1, list);
            list.remove(list.size() - 1);
        }
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E5%AD%90%E9%9B%86%E6%8E%92%E5%88%97%E7%BB%84%E5%90%88.md