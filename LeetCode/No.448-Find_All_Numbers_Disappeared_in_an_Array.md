## Description

Share

Given an array of integers where 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear twice and others appear once.

Find all the elements of [1, *n*] inclusive that do not appear in this array.

Could you do it without extra space and in O(*n*) runtime? You may assume the returned list does not count as extra space.

**Example:**

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

## Thinking

Really easy if use additional space.

If not use, we can use values in the array as index, change the value in index, like make them negative or add a value(you can check first and second link below to find these two options. The point is making them can be restored to previous value easily.). Then we loop again, find any index which points to a normal value, those indexes are what we need to return.

## Solutions

~~~java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<Integer>();
        for(int i = 0; i < nums.length; ++i) nums[Math.abs(nums[i]) - 1] = - Math.abs(nums[Math.abs(nums[i]) - 1]);
        for(int i = 0; i < nums.length; ++i) if(nums[i] > 0) res.add(i + 1);
        return res;
    }
}
~~~



## Further

https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/discuss/92955/Python-4-lines-with-short-explanation

https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/discuss/92980/5-line-Java-Easy-understanding

https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/discuss/93007/Simple-Java-In-place-sort-solution