## Description

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of *every* node differ in height by no more than 1.

 

**Example 1:**

![img](../Resources/Images/No.110-Balanced_binary_Tree/balance_1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

**Example 2:**

![img](../Resources/Images/No.110-Balanced_binary_Tree/balance_2.jpg)

```
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```

**Example 3:**

```
Input: root = []
Output: true
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `-104 <= Node.val <= 104`

## Thinking

1. Ugly solution. Calculate the depth of left node and right node in every node, which means it have a large amount of repeated calculation. O(n^2) time complexity.
2. A more elegant solution, avoid repeated calculation. From @mingyuan. O(n) time complexity. And other solutions in Further part.

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
//Solution 1
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        boolean res = true;
        int leftDepth = root.left == null ? 0 : countDepth(root.left);
        int rightDepth = root.right == null ? 0 : countDepth(root.right);
        if(Math.abs(leftDepth - rightDepth) > 1) return false;
        res = isBalanced(root.left) & isBalanced(root.right) & res;
        return res;
    }
    
    public int countDepth(TreeNode root) {
        if(root.left == null && root.right == null) {
            return 1;
        }
        int leftDepth = root.left == null ? -1 : countDepth(root.left);
        int rightDepth = root.right == null ? -1 : countDepth(root.right);
        return Math.max(leftDepth, rightDepth) + 1;
    }
}

//Solution 2
public boolean isBalanced(TreeNode root) {
    if(root==null){
        return true;
    }
    return height(root)!=-1;
    
}
public int height(TreeNode node){
    if(node==null){
        return 0;
    }
    int lH=height(node.left);
    if(lH==-1){
        return -1;
    }
    int rH=height(node.right);
    if(rH==-1){
        return -1;
    }
    if(lH-rH<-1 || lH-rH>1){
        return -1;
    }
    return Math.max(lH,rH)+1;
}
~~~



## Further

https://leetcode.com/problems/balanced-binary-tree/discuss/35686/Java-solution-based-on-height-check-left-and-right-node-in-every-recursion-to-avoid-further-useless-search

https://leetcode.com/problems/balanced-binary-tree/discuss/35943/JAVA-O(n)-solution-based-on-Maximum-Depth-of-Binary-Tree

