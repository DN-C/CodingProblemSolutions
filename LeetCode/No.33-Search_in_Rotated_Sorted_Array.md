## Description

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the rotation and an integer `target`, return *the index of* `target` *if it is in* `nums`*, or* `-1` *if it is not in* `nums`.

 

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

**Example 3:**

```
Input: nums = [1], target = 0
Output: -1
```

 

**Constraints:**

- `1 <= nums.length <= 5000`
- `-104 <= nums[i] <= 104`
- All values of `nums` are **unique**.
- `nums` is guaranteed to be rotated at some pivot.
- `-104 <= target <= 104`

 

**Follow up:** Can you achieve this in `O(log n)` time complexity?

## Thinking

Binary search.

Judge if nums[mid] and target are in same side(if nums[mid] < nums[0] && target < nums[0] || nums[mid] > nums[0] && target > nums[0]). if so, treat it as normal BS. Otherwise, narrow the search range by find the new low or high bound.

## Solutions

~~~java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0, high = nums.length;
        while(low < high) {
            int mid = low + (high - low) / 2;
            if(nums[mid] == target) return mid;
            if((nums[0] > target) == (nums[mid] < nums[0])) {
               // System.out.println(low + "  " + mid + "  " + high);
                if(nums[mid] > target) {
                    high = mid;
                } else {
                    low = mid + 1;
                }
                continue;
            }
            
            if(nums[mid] < target) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return -1;
    }
}
~~~



## Further

https://leetcode.com/problems/search-in-rotated-sorted-array/discuss/14435/Clever-idea-making-it-simple

https://leetcode.com/problems/search-in-rotated-sorted-array/discuss/14436/Revised-Binary-Search

https://leetcode.com/problems/search-in-rotated-sorted-array/discuss/14425/Concise-O(log-N)-Binary-search-solution