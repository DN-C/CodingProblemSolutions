## Description

Given the `head` of a singly linked list, return `true` if it is a palindrome.

 

**Example 1:**

![img](../Resources/Images/No.234-PalindromeLinkedList/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true
```

**Example 2:**

![img](../Resources/Images/No.234-PalindromeLinkedList/pal2linked-list.jpg)

```
Input: head = [1,2]
Output: false
```

 

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`

 

## Thinking

1. Use a stack to store a reverse linked list, then compare. O(n) space, O(n) time.
2. Use recursion as stack. Go check @labuladong. O(n) space, O(n) time.
3. Use two pointer to find the middle of the linked list, then reverse half of the linked list, compare the original half and the reversed half. O(1) space, O(n) time.

## Solutions

~~~java
//Based on thinking 3
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
    public boolean isPalindrome(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while(fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        if(fast != null) {
            slow = slow.next;
        }
        ListNode right= reverse(slow);
        while(right != null) {
            if(right.val != head.val) return false;
            right = right.next;
            head = head.next;
        }
        return true;
    }
    
    public ListNode reverse(ListNode head) {
        ListNode prev = null;
        ListNode then = null;
        while(head != null) {
            then = head.next;
            head.next = prev;
            prev = head;
            head = then;
        }
        return prev;
    }
    
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E5%88%A4%E6%96%AD%E5%9B%9E%E6%96%87%E9%93%BE%E8%A1%A8.md

https://leetcode.com/problems/palindrome-linked-list/discuss/64501/Java-easy-to-understand