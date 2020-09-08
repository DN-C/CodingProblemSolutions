## Description

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly\* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

 

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

 

**Constraints:**

- `2 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **Only one valid answer exists.**

## Thinking

1. target减去 i 位置的数组元素后，所得结果对比 i 后所有元素，相等则返回[i, j]，空间复杂度O(1)，时间复杂度O(n^2^)
2. 在1的基础上，不需要每次都遍历 i 后的数组元素，使用 HashMap 储存 i 之前的元素，然后检查target - nums[i]是否在map中，有则返回[i, map.get(target - nums(i)]，无则map,put(nums[i], i)

## Solutions

~~~java
// Solutions 1
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int result[] = new int[] {};
        int numsLength = nums.length;
        for(int i = 0; i < numsLength; i++) {
            int tempNum = target - nums[i];
            for (int j = i; j < numsLength; j++) {
                if (nums[j] == tempNum){
                    return new int[] {i, j};
                }
            }
        }
        return result;
    }
}

// Solutions 2
public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for (int i = 0; i < numbers.length; i++) {
        if (map.containsKey(target - numbers[i])) {
            result[1] = i;
            result[0] = map.get(target - numbers[i]);
            return result;
        }
        map.put(numbers[i], i);
    }
    return result;
}
~~~



## Further

