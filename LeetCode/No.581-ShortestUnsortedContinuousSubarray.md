## Description

Given an integer array `nums`, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order.

Return *the shortest such subarray and output its length*.

 

**Example 1:**

```
Input: nums = [2,6,4,8,10,9,15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```

**Example 2:**

```
Input: nums = [1,2,3,4]
Output: 0
```

**Example 3:**

```
Input: nums = [1]
Output: 0
```

 

**Constraints:**

- `1 <= nums.length <= 104`
- `-105 <= nums[i] <= 105`

 

**Follow up:** Can you solve it in `O(n)` time complexity?

## Thinking

Fully credited to @compton_scatter at link in [Further](#Further), fxxking genius idea.

From left to right, find the rightmost number which is smaller than the max number in the array. From right to left, find the leftmost number which is bigger than the min number in the array, then return right - left + 1.

## Solutions

~~~java
class Solution {
    public int findUnsortedSubarray(int[] nums) {
        int len = nums.length;
        if(len == 1) return 0;
        int start = -1, end = -2, max = nums[0], min = nums[len - 1];
        for(int i = 1; i < len; i++) {
            max = Math.max(max, nums[i]);
            min = Math.min(min, nums[len - i - 1]);
            
            if(nums[i] < max) end = i;
            if(nums[len - i - 1] > min) start = len - i - 1;
        }
        return end - start + 1;
    }
}
~~~



## Further

https://leetcode.com/problems/shortest-unsorted-continuous-subarray/discuss/103057/Java-O(n)-Time-O(1)-Space