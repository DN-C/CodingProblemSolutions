## Description

Given a list of daily temperatures `T`, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put `0` instead.

For example, given the list of temperatures `T = [73, 74, 75, 71, 69, 72, 76, 73]`, your output should be `[1, 1, 4, 2, 1, 1, 0, 0]`.

**Note:** The length of `temperatures` will be in the range `[1, 30000]`. Each temperature will be an integer in the range `[30, 100]`.

## Thinking

Similar to No.496, but push index in stack instead of value.

## Solutions

~~~java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        Stack<Integer> stack = new Stack<Integer>();
        int len = T.length;
        int res[] = new int[len];
        for(int i = 0; i < len; i++) {
            while(!stack.empty() && T[i] > T[stack.peek()]) {
                int tempIndex = stack.pop();
                res[tempIndex] = i - tempIndex; 
            }
            stack.push(i);
        }
        return res;
    }
}
~~~



## Further

Go check No.496's Further part, it's same.