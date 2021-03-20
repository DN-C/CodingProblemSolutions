## Description

Given the `root` of a binary tree and an integer `targetSum`, return all **root-to-leaf** paths where each path's sum equals `targetSum`.

A **leaf** is a node with no children.

 

**Example 1:**

![img](../Resources/Images/No.113-Path_Sum_II/pathsumii1.jpg)

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
```

**Example 2:**

![img](../Resources/Images/No.113-Path_Sum_II/pathsum2.jpg)

```
Input: root = [1,2,3], targetSum = 5
Output: []
```

**Example 3:**

```
Input: root = [1,2], targetSum = 0
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`

## Thinking

DFS

A more elegant backtrack solution in Further part.

## Solutions

~~~java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) {
            return res;
        }
        countPath(res, new ArrayList<Integer>(), 0, targetSum, root);
        return res;
    }
    
    public void countPath(List<List<Integer>> res, List<Integer> path, int currentSum, int targetSum, TreeNode root) {
        if(root == null) {
            return;
        }
        path.add(root.val);
        currentSum += root.val;
        if(root.left == null && root.right == null) {
            if(currentSum == targetSum) {
                res.add(path);
            }
            return;
        }
        countPath(res, new ArrayList<Integer>(path), currentSum, targetSum, root.left);
        countPath(res, new ArrayList<Integer>(path), currentSum, targetSum, root.right);
        
    }
}
~~~



## Further

https://leetcode.com/problems/path-sum-ii/discuss/36683/DFS-with-one-LinkedList-accepted-java-solution

https://leetcode.com/problems/path-sum-ii/discuss/36695/Java-Solution%3A-iterative-and-recursive