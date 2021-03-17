## Description

Given two sorted integer arrays `nums1` and `nums2`, merge `nums2` into `nums1` as one sorted array.

The number of elements initialized in `nums1` and `nums2` are `m` and `n` respectively. You may assume that `nums1` has a size equal to `m + n` such that it has enough space to hold additional elements from `nums2`.

 

**Example 1:**

```
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
```

**Example 2:**

```
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
```

 

**Constraints:**

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-109 <= nums1[i], nums2[i] <= 109`

## Thinking

From end to start, put Math,max(nums1[i], nums2[j]) to nums1[i + j].

## Solutions

~~~java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int newEnd = m + n - 1, mEnd = m - 1, nEnd = n - 1;
        while(mEnd >= 0 && nEnd >= 0) {
            int mVal = mEnd >= 0 ? nums1[mEnd] : nums1[0];
            int nVal = nEnd >= 0 ? nums2[nEnd] : nums2[0];
            if(mVal > nVal) {
                nums1[newEnd] = mVal;
                --mEnd;
            } else {
                nums1[newEnd] = nVal;
                --nEnd;
            }
            newEnd--;
        }
        while(nEnd >= 0) {
            nums1[newEnd--] = nums2[nEnd--]; 
        }
        return;
    }
}
~~~



## Further

https://leetcode.com/problems/merge-sorted-array/discuss/29522/This-is-my-AC-code-may-help-you