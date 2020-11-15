## Description

Given an array `nums` of *n* integers and an integer `target`, are there elements *a*, *b*, *c*, and *d* in `nums` such that *a* + *b* + *c* + *d* = `target`? Find all unique quadruplets in the array which gives the sum of `target`.

**Notice** that the solution set must not contain duplicate quadruplets.

 

**Example 1:**

```
Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**Example 2:**

```
Input: nums = [], target = 0
Output: []
```

 

**Constraints:**

- `0 <= nums.length <= 200`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`

## Thinking

Nearly same as No.15 3Sum, but just one more loop

## Solutions

~~~java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        if (nums.length <= 3) return new ArrayList<>();
        Arrays.sort(nums);
        int len = nums.length;
        HashSet<List<Integer>> set = new HashSet<>();
        for (int i = 0; i < len; i++) {
            for(int j = i + 1; j < len; j++) {
                int tempTarget = target - nums[i] - nums[j], left = j + 1, right = len - 1;
                while(left < right) {
                    if (nums[left] + nums[right] == tempTarget) {
                        set.add(Arrays.asList(nums[left], nums[right], nums[i], nums[j]));
                        while (left < len - 1 && nums[left] == nums[left + 1]) left++;
                        while (right > 0 && nums[right] == nums[right - 1]) right--;
                        left++; right--;
                    } else if ( nums[left] + nums[right] > tempTarget) right--;
                    else left++;
                }
            }
        }
        List<List<Integer>> lists = new ArrayList<>();
        lists.addAll(set);
        return lists;
    }
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie-qing-an-shun-xu-yue-du/nsum