## Description

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

 

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

 

**Constraints:**

- `1 <= nums.legth <= 105`
- `k` is in the range `[1, the number of unique elements in the array]`.
- It is **guaranteed** that the answer is **unique**.

 

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Thinking

Use buckets to store numbers with different frequencies. Start from bucket with highest frequency, put numbers in that bucket to result array.

Some other solutions with heap(priorityQueue) and treeMap in further part.

## Solutions

~~~java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        ArrayList<ArrayList<Integer>> buckets = new ArrayList<ArrayList<Integer>>();
        HashMap<Integer, Integer> frequency = new HashMap<Integer, Integer>();
        int[] res = new int[k];
        
        //Calculate frequency
        for(int i = 0; i < nums.length; ++i){
            frequency.put(nums[i], frequency.getOrDefault(nums[i], 0) + 1);
        }
        
        //Put to frequency buckets
        for(int key : frequency.keySet()) {
            int freq = frequency.get(key);
            while(buckets.size() < freq + 1) {
                buckets.add(new ArrayList<Integer>());
            }
            buckets.get(freq).add(key);
        }
        
        //Put numbers to result array.
        for(int i = buckets.size() - 1, count = 0; i >= 0 && count < k; --i) {
            ArrayList<Integer> list = buckets.get(i);
            for(int l = 0; l < list.size(); ++l) {
                if(count < k) res[count] = list.get(l);
                count++;
            }
        }
        
        return res;
    }
}
~~~



## Further

https://leetcode.com/problems/top-k-frequent-elements/discuss/81602/Java-O(n)-Solution-Bucket-Sort

https://leetcode.com/problems/top-k-frequent-elements/discuss/81635/3-Java-Solution-using-Array-MaxHeap-TreeMap