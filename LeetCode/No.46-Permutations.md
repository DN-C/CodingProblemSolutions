## Description

Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## Thinking

1. backtrack

## Solutions

~~~java
// Solution 1 
//Really sucks...
class Solution {
    List<List<Integer>> numsList = new ArrayList(); 
    
    public List<List<Integer>> permute(int[] nums) {
        ArrayList<Integer> yANums = new ArrayList<Integer>(nums.length); // yet another nums
        for (int i : nums) yANums.add(i);
        backtrack(yANums, new ArrayList());
        return numsList;
    }
    
    public void backtrack(ArrayList<Integer> nums, List<Integer> numList) {
        if (nums.size() == 1) {
            numList.add(nums.get(0));
            numsList.add(new ArrayList<Integer>(numList));
            numList.remove(numList.size() - 1);
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            int num = nums.get(0);
            numList.add(num);
            nums.remove(0);
            backtrack(nums, numList);
            nums.add(num);
            numList.remove(numList.size() - 1);
        }
    }
}

//Solution 1 from @issac3
//Elegant one
public List<List<Integer>> permute(int[] nums) {
   List<List<Integer>> list = new ArrayList<>();
   // Arrays.sort(nums); // not necessary
   backtrack(list, new ArrayList<>(), nums);
   return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums){
   if(tempList.size() == nums.length){
      list.add(new ArrayList<>(tempList));
   } else{
      for(int i = 0; i < nums.length; i++){ 
         if(tempList.contains(nums[i])) continue; // element already exists, skip
         tempList.add(nums[i]);
         backtrack(list, tempList, nums);
         tempList.remove(tempList.size() - 1);
      }
   }
} 
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hui-su-suan-fa-xiang-jie-xiu-ding-ban

https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning)