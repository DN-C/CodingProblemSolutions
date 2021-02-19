## Description

Given `n` non-negative integers `a1, a2, ..., an` , where each represents a point at coordinate `(i, ai)`. `n` vertical lines are drawn such that the two endpoints of the line `i` is at `(i, ai)` and `(i, 0)`. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

 

**Example 1:**

![img](../Resources/Images/No.11-ContainerWithMostWater/question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

**Example 2:**

```
Input: height = [1,1]
Output: 1
```

**Example 3:**

```
Input: height = [4,3,2,1,4]
Output: 16
```

**Example 4:**

```
Input: height = [1,2,1]
Output: 2
```

 

**Constraints:**

- `n == height.length`
- `2 <= n <= 3 * 104`
- `0 <= height[i] <= 3 * 104`

## Thinking

My initial idea is iterate all possibilities and return the max one. But its time complexity is O(N^N), which is too high. Then I go to Discuss section and learn an O(N) solution. Go check in [Further](#Further).

## Solutions

~~~java
class Solution {
    public int maxArea(int[] height) {
        int len = height.length;
        int left = 0, right = len - 1, water = 0;
        while(left < right) {
            water = Math.max(water, (right - left) * Math.min(height[left], height[right]));
            if(height[left] < height[right]){
                ++left;
            } else {
                --right;
            }
        }
        return water;
    }
}
~~~



## Further

https://leetcode.com/problems/container-with-most-water/discuss/6100/Simple-and-clear-proofexplanation

https://leetcode.com/problems/container-with-most-water/discuss/6099/Yet-another-way-to-see-what-happens-in-the-O(n)-algorithm

https://leetcode.com/problems/container-with-most-water/discuss/6091/Easy-Concise-Java-O(N)-Solution-with-Proof-and-Explanation