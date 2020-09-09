## Description

Given a binary tree, each node has value `0` or `1`. Each root-to-leaf path represents a binary number starting with the most significant bit. For example, if the path is `0 -> 1 -> 1 -> 0 -> 1`, then this could represent `01101` in binary, which is `13`.

For all leaves in the tree, consider the numbers represented by the path from the root to that leaf.

Return the sum of these numbers.

 

**Example 1:**

![img](..\Resources\Images\No.1022-1.png)

```
Input: [1,0,1,0,1,0,1]
Output: 22
Explanation: (100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22
```

 

**Note:**

1. The number of nodes in the tree is between `1` and `1000`.
2. node.val is `0` or `1`.
3. The answer will not exceed `2^31 - 1`.

## Thinking

1. DFS遍历所有树节点，然后二进制转十进制相加。

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
    public int sumRootToLeaf(TreeNode root) {
        return dfs(root, 0);
    }
    
    public int dfs(TreeNode root, int value) {
        if (root == null) return 0;
        value = value * 2 + root.val;
        return root.left == root.right ? value : dfs(root.left, value) + dfs(root.right, value);
    }
}
~~~



## Further

参考Discussions