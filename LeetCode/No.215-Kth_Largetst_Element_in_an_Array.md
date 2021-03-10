## Description

Given an integer array `nums` and an integer `k`, return *the* `kth` *largest element in the array*.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

 

**Example 1:**

```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

**Example 2:**

```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

 

**Constraints:**

- `1 <= k <= nums.length <= 104`
- `-104 <= nums[i] <= 104`

## Thinking

1. Quick Sort
2. Quick Select

## Solutions

~~~java
//Solution 1
class Solution {
    public int findKthLargest(int[] nums, int k) {
        quickSort(nums, 0, nums.length - 1);
        return nums[nums.length - k];
    }
    
    public void quickSort(int[] nums, int left, int right) {
        if(left >= right) return;
        int index = partition(nums, left, right);
        
        quickSort(nums, left, index - 1);
        quickSort(nums, index + 1, right);
    }
    
    public int partition(int[] nums, int left, int right) {
        int pivot = left;
        int slow = left, fast = left + 1;
        while(fast <= right) {
            if(nums[fast] < nums[pivot]) {
                ++slow;
                swap(nums, slow, fast);
            }
            ++fast;
        }
        swap(nums, pivot, slow);
        return slow;
    }
    
    public void swap(int[] nums, int m, int n){
        int temp = nums[m];
        nums[m] = nums[n];
        nums[n] = temp;
    }
}

// Solution 2
class Solution {
    public int findKthLargest(int[] nums, int k) {
        return nums[quickSelect(nums, 0, nums.length - 1, nums.length - k)];
    }
    
    public int quickSelect(int[] nums, int left, int right, int k) {
        if(left >= right) return left;
        int index = partition(nums, left, right);
        if(index == k) return index;
        else if(index > k) return quickSelect(nums, left, index - 1, k);
        else return quickSelect(nums, index + 1, right, k);
    }
    
    public int partition(int[] nums, int left, int right) {
        int pivot = left;
        int slow = left, fast = left + 1;
        while(fast <= right) {
            if(nums[fast] < nums[pivot]) {
                ++slow;
                swap(nums, slow, fast);
            }
            ++fast;
        }
        swap(nums, pivot, slow);
        return slow;
    }
    
    public void swap(int[] nums, int m, int n){
        int temp = nums[m];
        nums[m] = nums[n];
        nums[n] = temp;
    }
}
~~~



## Further

https://www.geeksforgeeks.org/quickselect-algorithm/

https://www.geeksforgeeks.org/quick-sort/

https://leetcode.com/problems/kth-largest-element-in-an-array/discuss/60294/Solution-explained