## Description

Given the `root` of a binary tree, return *the zigzag level order traversal of its nodes' values*. (i.e., from left to right, then right to left for the next level and alternate between).

 

**Example 1:**

![img](../Resources/Images/No.103-Binary_Tree_Zigzag_Level_Order_Traversal/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
```

**Example 2:**

```
Input: root = [1]
Output: [[1]]
```

**Example 3:**

```
Input: root = []
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-100 <= Node.val <= 100`

## Thinking

Use deque and a status sign to simulate.

Some other solutions in further part.

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if(root == null) return res;
        Deque<TreeNode> deque = new LinkedList<TreeNode>();
        boolean isLast = false;
        deque.offerFirst(root);
        while(!deque.isEmpty()) {
            ArrayList<Integer> list = new ArrayList<Integer>();
            int size = deque.size();
            if(isLast) {
                for(int i = 0; i < size; ++i) {
                    TreeNode node = deque.pollLast();
                    list.add(node.val);
                    if(node.right != null) deque.offerFirst(node.right);
                    if(node.left != null) deque.offerFirst(node.left);
                }
            } else {
                for(int i = 0; i < size; ++i) {
                    TreeNode node = deque.pollFirst();
                    list.add(node.val);
                    if(node.left != null) deque.offerLast(node.left);
                    if(node.right != null) deque.offerLast(node.right);
                }
            }
            isLast = !isLast;
            res.add(list);
        }
        return res;
    }
}
~~~



## Further

https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/discuss/33814/A-concise-and-easy-understanding-Java-solution

https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/discuss/33815/My-accepted-JAVA-solution

https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/discuss/33904/JAVA-Double-Stack-Solution