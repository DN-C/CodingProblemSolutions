## Description

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

## Thinking

递归，通过根节点判断出左子树与右子树的中序遍历，然后再通过左子树中序遍历的个数判断左子树与右子树的前序遍历。



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
import java.util.Arrays;

class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        TreeNode node, leftNode, rightNode;
        if (preorder == null || inorder == null) {
            node = new TreeNode();
            return node;
        } else if (preorder.length == 1 && inorder.length == 1) {
            node = new TreeNode(preorder[0]);
            return node;
        }
        int firstNodeVal = preorder[0];
        int position = Arrays.binarySearch(inorder, firstNodeVal);
        if (position == -1) {
            node = new TreeNode();
            return node;
        }
        
        if (position != 0) {
            int leftTreeInorder[] = Arrays.copyOfRange(inorder, 0, position);
            int leftTreePreorder[] = Arrays.copyOfRange(preorder, 1, 1 + position);     
            leftNode = buildTree(leftTreePreorder, leftTreeInorder);
        } else {
            leftNode = new TreeNode();
        }

        if (position != inorder.length - 1) {
            int rightTreeInorder[] = Arrays.copyOfRange(inorder, position - 1, inorder.length);
            int rightTreePreorder[] = Arrays.copyOfRange(preorder, 1 + position, preorder.length);
            rightNode = buildTree(rightTreePreorder, rightTreeInorder);
        } else {
            rightNode = new TreeNode();
        }
        
        node = new TreeNode(firstNodeVal, leftNode, rightNode);
        return node;
        
    }
}
~~~



## Further

https://blog.csdn.net/hailushijie/article/details/9199321

https://blog.csdn.net/u012552052/article/details/42649439