## Description

Given a linked list, reverse the nodes of a linked list *k* at a time and return its modified list.

*k* is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of *k* then left-out nodes, in the end, should remain as it is.

**Follow up:**

- Could you solve the problem in `O(1)` extra memory space?
- You may not alter the values in the list's nodes, only nodes itself may be changed.

 

**Example 1:**

![img](../Resources/Images/No.25-ReverseNodesInk-Group/reverse_ex1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

**Example 2:**

![img](../Resources/Images/No.25-ReverseNodesInk-Group/reverse_ex2.jpg)

```
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

**Example 3:**

```
Input: head = [1,2,3,4,5], k = 1
Output: [1,2,3,4,5]
```

**Example 4:**

```
Input: head = [1], k = 1
Output: [1]
```

 

**Constraints:**

- The number of nodes in the list is in the range `sz`.
- `1 <= sz <= 5000`
- `0 <= Node.val <= 1000`
- `1 <= k <= sz`

## Thinking

Iterative solutions.

A recursive solution in further.

## Solutions

~~~java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if(k == 1) return head;
        int i = 0;
        ListNode realHead = new ListNode(0);
        ListNode loopHead = realHead;
        realHead.next = head;
        ListNode tempHead = realHead;
        ListNode tmp = null;
        while(loopHead != null) {
            if(i == k) {
                tmp = tempHead.next;
                reverse(tempHead, k);
                tempHead = tmp;
                i = 0;
                loopHead = tmp;
                continue;
            }
            ++i;
            loopHead = loopHead.next;
        }
        return realHead.next;
    }
    
    public void reverse(ListNode head, int k) {
        ListNode tail = head.next;
        ListNode prev = head.next;
        ListNode start = prev.next;
        ListNode tmp = start.next;
        for(int i = 0; i < k - 1; i++) {
            tmp = start.next;
            start.next = prev;
            prev = start;
            start = tmp;
        }
        tail.next = start;
        head.next = prev;
    }
}
~~~



## Further

https://leetcode.com/problems/reverse-nodes-in-k-group/discuss/11440/Non-recursive-Java-solution-and-idea

https://leetcode.com/problems/reverse-nodes-in-k-group/discuss/11423/Short-but-recursive-Java-code-with-comments

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/k%E4%B8%AA%E4%B8%80%E7%BB%84%E5%8F%8D%E8%BD%AC%E9%93%BE%E8%A1%A8.md