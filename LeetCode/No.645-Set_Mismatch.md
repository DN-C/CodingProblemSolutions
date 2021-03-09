## Description

You have a set of integers `s`, which originally contains all the numbers from `1` to `n`. Unfortunately, due to some error, one of the numbers in `s` got duplicated to another number in the set, which results in **repetition of one** number and **loss of another** number.

You are given an integer array `nums` representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return *them in the form of an array*.

 

**Example 1:**

```
Input: nums = [1,2,2,4]
Output: [2,3]
```

**Example 2:**

```
Input: nums = [1,1]
Output: [1,2]
```

 

**Constraints:**

- `2 <= nums.length <= 104`
- `1 <= nums[i] <= 104`

## Thinking

Quite similar to No.448

## Solutions

~~~java
class Solution {
    public int[] findErrorNums(int[] nums) {
        int res[] = new int[2];
        for(int i = 0; i < nums.length; ++i) {
            int index = Math.abs(nums[i]) - 1;
            if(nums[index] < 0) res[0] = index + 1;
            else nums[index] = -nums[index];
        }
        for(int i = 0; i < nums.length; ++i) {
            if(nums[i] > 0) res[1] = i + 1;
        }
        return res;
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E7%BC%BA%E5%A4%B1%E5%92%8C%E9%87%8D%E5%A4%8D%E7%9A%84%E5%85%83%E7%B4%A0.md

[No.448](No.448-Find_All_Numbers_Disappeared_in_an_Array.md)

