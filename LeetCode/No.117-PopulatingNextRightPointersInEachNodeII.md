## Description

Given a binary tree

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

 

**Follow up:**

- You may only use constant extra space.
- Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

 

**Example 1:**

![img](..\Resources\Images\No.117-PopulatingNextRightPointersInEachNodeII\117_sample.png)

```
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

 

**Constraints:**

- The number of nodes in the given tree is less than `6000`.
- `-100 <= node.val <= 100`

## Thinking



## Solutions

~~~java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        Node curNode = root;
        Node headNode = null;
        Node prevNode = null;
        while(curNode != null) {
            while(curNode != null) {
                if(curNode.left != null) {
                    if(prevNode != null) {
                        prevNode.next = curNode.left;
                    } else {
                        headNode = curNode.left;
                    }
                    prevNode = curNode.left;
                }
                 
                if(curNode.right != null) {
                    if(prevNode != null) {
                        prevNode.next = curNode.right;
                    } else {
                        headNode = curNode.right;
                    }
                    prevNode = curNode.right;
                }
                curNode = curNode.next;
            }
            curNode = headNode;
            headNode = null;
            prevNode = null;
        }
        return root;
    }
}
~~~



## Further

https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/discuss/37828/O(1)-space-O(n)-complexity-Iterative-Solution