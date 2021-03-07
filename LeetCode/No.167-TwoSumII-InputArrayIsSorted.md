## Description

Given an array of integers `numbers` that is already ***sorted in ascending order\***, find two numbers such that they add up to a specific `target` number.

Return the indices of the two numbers (**1-indexed**) as an integer array `answer` of size `2`, where `1 <= answer[0] < answer[1] <= numbers.length`.

You may assume that each input would have **exactly one solution** and you **may not** use the same element twice.

 

**Example 1:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

**Example 2:**

```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
```

**Example 3:**

```
Input: numbers = [-1,0], target = -1
Output: [1,2]
```

 

**Constraints:**

- `2 <= numbers.length <= 3 * 104`
- `-1000 <= numbers[i] <= 1000`
- `numbers` is sorted in **increasing order**.
- `-1000 <= target <= 1000`
- **Only one valid answer exists.**

## Thinking

Two pointers. 

## Solutions

~~~java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0, right = numbers.length - 1, sum = 0;
        while(left <= right) {
            sum = numbers[left] + numbers[right];
            if(sum == target) return new int[] {left + 1, right + 1};
            else if(sum > target) --right;
            else if(sum < target) ++left;
        }
        return new int[]{};
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/%E5%8F%8C%E6%8C%87%E9%92%88%E6%8A%80%E5%B7%A7.md