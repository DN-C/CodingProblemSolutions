## Description

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?

## Thinking

DP

## Solutions

~~~java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0) return 0;
        int len = nums.length;
        int dptable[] = new int[len];
        for(int i = 0; i < len; i++) {
            if (i == 0) {
                dptable[i] = 1;
            } else {
                int tempMaxLen = 1;
                for(int j = 0; j < i; j++) {
                    if(nums[j] < nums[i]) {
                        tempMaxLen = Math.max(tempMaxLen, dptable[j] + 1);
                    }
                }
                dptable[i] = tempMaxLen;
            }
        }
        Arrays.sort(dptable);
        return dptable[len - 1];
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AE%BE%E8%AE%A1%EF%BC%9A%E6%9C%80%E9%95%BF%E9%80%92%E5%A2%9E%E5%AD%90%E5%BA%8F%E5%88%97.md