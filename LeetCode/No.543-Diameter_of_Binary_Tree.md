## Description

Given the `root` of a binary tree, return *the length of the **diameter** of the tree*.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

 

**Example 1:**

![img](../Resources/Images/No.543-Diameter_of_Binary_Tree/diamtree.jpg)

```
Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3is the length of the path [4,2,1,3] or [5,2,1,3].
```

**Example 2:**

```
Input: root = [1,2]
Output: 1
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-100 <= Node.val <= 100`

## Thinking

Use maxLength to store max diameter, calculate depth of left node and right node, then Math.max(leftDepth + rightDepth, maxLength), return Math.max(leftDepth, rigthDepth).

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
    public int maxLength = 0;
    
    public int diameterOfBinaryTree(TreeNode root) {
        calculateLength(root);
        return maxLength;
    }
    
    public int calculateLength(TreeNode root) {
        if(root == null) return 0;
        int rightDepth = calculateLength(root.right);
        int leftDepth = calculateLength(root.left);
        this.maxLength = Math.max(this.maxLength, rightDepth + leftDepth);
        return Math.max(rightDepth, leftDepth) + 1;
    }
}
~~~



## Further

