## Description

Share

Given an integer array `nums` of **unique** elements, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

 

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

 

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

## Thinking

Backtrack

## Solutions

~~~java
class Solution {
    List<List<Integer>> res;
    
    public List<List<Integer>> subsets(int[] nums) {
        res = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        backtrack(nums, 0, list);
        return res;
    }
    
    public void backtrack(int[] nums, int start, List<Integer> list) {
        res.add(new ArrayList<Integer>(list));
        for(int i = start; i < nums.length; ++i) {
            list.add(nums[i]);
            backtrack(nums, i + 1, list);
            list.remove(list.size() - 1);
        }
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E5%AD%90%E9%9B%86%E6%8E%92%E5%88%97%E7%BB%84%E5%90%88.md

https://leetcode.com/problems/subsets/discuss/27281/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partitioning)