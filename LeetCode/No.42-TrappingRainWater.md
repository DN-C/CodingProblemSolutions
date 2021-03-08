## Description

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

 

**Example 1:**

![img](../Resources/Images/No.42-TrappingRainWater/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

 

**Constraints:**

- `n == height.length`
- `0 <= n <= 3 * 104`
- `0 <= height[i] <= 105`

## Thinking

1. Two pointers, one record the highest index from left to right, the other record the highest from right to left.
2. Use 2 extra array to record the left highest and the right highest at index i.
3. Use stack to record a decreasing height, go check further part.

## Solutions

~~~java
//Solution 1
class Solution {
    public int trap(int[] height) {
        int len = height.length;
        if(len < 2) return 0;
        int res = 0, left = 0, right = len - 1, leftMax = 0, rightMax = 0;
        while(left < right) {
            leftMax = Math.max(leftMax, height[left]);
            rightMax = Math.max(rightMax,height[right]);
            
            if(leftMax < rightMax) {
                res += leftMax - height[left];
                ++left;
            } else {
                res += rightMax - height[right];
                --right;
            }
        }
        return res;
    }
}

//Solution 2
class Solution {
    public int trap(int[] height) {
        int len = height.length;
        if(len < 2) return 0;
        int res = 0;
        int leftMax[] = new int[len];
        int rightMax[] = new int[len];
        leftMax[0] = height[0];
        rightMax[len - 1] = height[len - 1];
        for(int i = 1; i < len; ++i) {
            leftMax[i] = Math.max(leftMax[i - 1], height[i]);
        }
        for(int i = len - 2; i >= 0; --i) {
            rightMax[i] = Math.max(rightMax[i + 1], height[i]);
        }
        for(int i = 1; i < len - 1; ++i) {
            res += Math.min(leftMax[i], rightMax[i]) - height[i]; 
        }
        return res;
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E6%8E%A5%E9%9B%A8%E6%B0%B4.md

https://leetcode.com/problems/trapping-rain-water/discuss/17391/Share-my-short-solution.

https://leetcode.com/problems/trapping-rain-water/discuss/17414/A-stack-based-solution-for-reference-inspired-by-Histogram