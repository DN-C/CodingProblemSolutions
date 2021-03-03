## Description

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

**Example 1:**

```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; The number 2 can't find next greater number; The second 1's next greater number needs to search circularly, which is also 2.
```



**Note:** The length of given array won't exceed 10000.

## Thinking

Similar to No. 496, but loop twice. 

A more elegant implement from @lee215 in [Further](#Further).

## Solutions

~~~java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        Stack<Integer> stack = new Stack<Integer>();
        int len = nums.length;
        int res[] = new int[len];
        for(int i = 0; i < len; i++) {
            while(!stack.empty() && nums[i] > nums[stack.peek()]) {
                res[stack.pop()] = nums[i];
            }
            stack.push(i);
        }
        for(int i = 0; i < len; i++) {
            while(!stack.empty() && nums[i] > nums[stack.peek()]) {
                res[stack.pop()] = nums[i];
            }
        }
        while(!stack.empty()) {
            res[stack.pop()] = -1;
        }
        return res;
    }
}
~~~



## Further

https://leetcode.com/problems/next-greater-element-ii/discuss/98270/JavaC%2B%2BPython-Loop-Twice

https://github.com/labuladong/fucking-algorithm/blob/master/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E7%B3%BB%E5%88%97/%E5%8D%95%E8%B0%83%E6%A0%88.md