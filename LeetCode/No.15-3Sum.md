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

1. Reuse the code in No.1 2Sum. Loop in the given array, and take every -nums[i] as target. Then use 2Sum codes to find any two numbers which sums up to -nums[i]. Besides, I used many tricks to improve its speed, like after sorting the array, if nums[0] > 0, it means that it's impossible to take any 3 numbers in array to sums up to 3 since the minimum is larger than 0. What's more, When in loop, jump all the duplicated numbers. But still, it's a slow one with many workarounds.
2. Same logic as the first one. But use two pointer instead of HashMap to find 2 numbers sums to -nums[i]

## Solutions

~~~java
// Solution 1
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if (nums.length <= 2) return new ArrayList<>(); 
        int len = nums.length;
        Arrays.sort(nums);
        if (nums[0] > 0) return new ArrayList<>();
        HashSet<ArrayList<Integer>> lists = new HashSet<>();
        for(int i = 0; i < len; i++) {
            if (i == 0 || nums[i] != nums[i - 1]) {
                int target = -nums[i];
                HashSet<Integer> set = new HashSet<Integer>();
                for (int j = i + 1; j < len; j++) {
                    if (set.contains(target - nums[j])) {
                        ArrayList<Integer> tempList = new ArrayList<Integer>(Arrays.asList(nums[i], target - nums[j], nums[j])); 
                        Collections.sort(tempList);
                        lists.add(tempList); 
                    }
                    set.add(nums[j]);
                }
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
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if (nums.length <= 2) return new ArrayList<>(); 
        int len = nums.length;
        Arrays.sort(nums);
        HashSet<List<Integer>> lists = new HashSet<>();
        for(int i = 0; i < len; i++) {
            int target = -nums[i];
            int start = i + 1, end = len - 1;
            while(start < end) {
                int sum = nums[start] + nums[end]; 
                if (sum < target) start++;
                else if (sum > target) end--;
                else {
                    lists.add(Arrays.asList(nums[start], nums[end], nums[i]));
                    while(start < len - 1 && nums[start] == nums[start + 1]) start++;
                    while(end > 0 && nums[end] == nums[end - 1]) end--;
                    start++; 
                    end--;
                }
            }
        }
        List<List<Integer>> res = new ArrayList<>();
        for(List<Integer> list : lists) {
            res.add(list);
        }
        return res;
    }
}
~~~



## Further

https://beginnersbook.com/2013/12/how-to-sort-arraylist-in-java/

https://blog.csdn.net/fdl123456/article/details/107194517