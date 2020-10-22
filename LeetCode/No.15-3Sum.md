## Description

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

Notice that the solution set must not contain duplicate triplets.

 

**Example 1:**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**Example 2:**

```
Input: nums = []
Output: []
```

**Example 3:**

```
Input: nums = [0]
Output: []
```

 

**Constraints:**

- `0 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`

## Thinking

1. (It can't pass all tests!) Reuse the code in No.1 2Sum. Loop in the given array, and take every -nums[i] as target, then use 2Sum code to find any two numbers sums to -nums[i].
2. Same logic as the first one. But use two pointer instead of HashMap to find 2 numbers sums to -nums[i]

## Solutions

~~~java
// Solution 1
// Once again, it can't pass all tests!!!
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if (nums.length <= 2) return new ArrayList<>(); 
        int len = nums.length;
        Arrays.sort(nums);
        HashSet<ArrayList<Integer>> lists = new HashSet<>();
        for(int i = 0; i < len; i++) {
            int target = -nums[i];
            HashSet<Integer> set = new HashSet<Integer>();
            for (int j = 0; j < len; j++) {
                if (j == i) continue;
                if (set.contains(target - nums[j])) {
                    ArrayList<Integer> tempList = new ArrayList<Integer>(Arrays.asList(nums[i], target - nums[j], nums[j])); 
                    Collections.sort(tempList);
                    lists.add(tempList); 
                }
                set.add(nums[j]);
            }
        }
        List<List<Integer>> res = new ArrayList<>();
        for(ArrayList<Integer> list : lists) {
            res.add(list);
        }
        return res;
    }
}

//Solution 2
~~~



## Further

https://beginnersbook.com/2013/12/how-to-sort-arraylist-in-java/

https://blog.csdn.net/fdl123456/article/details/107194517