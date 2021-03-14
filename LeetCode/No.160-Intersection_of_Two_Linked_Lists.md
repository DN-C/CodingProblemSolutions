## Description

Given the heads of two singly linked-lists `headA` and `headB`, return *the node at which the two lists intersect*. If the two linked lists have no intersection at all, return `null`.

For example, the following two linked lists begin to intersect at node `c1`:

![img](../Resources/Images/No.160-Intersection_of_Two_Linked_Lists/160_statement.png)

It is **guaranteed** that there are no cycles anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original structure** after the function returns.

 

**Example 1:**

![img](../Resources/Images/No.160-Intersection_of_Two_Linked_Lists/160_example_1_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
Output: Intersected at '8'
Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

**Example 2:**

![img](../Resources/Images/No.160-Intersection_of_Two_Linked_Lists/160_example_2.png)

```
Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Intersected at '2'
Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [1,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

**Example 3:**

![img](../Resources/Images/No.160-Intersection_of_Two_Linked_Lists/160_example_3.png)

```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: No intersection
Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

 

**Constraints:**

- The number of nodes of `listA` is in the `m`.
- The number of nodes of `listB` is in the `n`.
- `0 <= m, n <= 3 * 104`
- `1 <= Node.val <= 105`
- `0 <= skipA <= m`
- `0 <= skipB <= n`
- `intersectVal` is `0` if `listA` and `listB` do not intersect.
- `intersectVal == listA[skipA + 1] == listB[skipB + 1]` if `listA` and `listB` intersect.

 

**Follow up:** Could you write a solution that runs in `O(n)` time and use only `O(1)` memory?

## Thinking

Go check the first link. 

The brief idea is use two pointers, each one loop two linked list individually. The first one loop from linked list 1 first, the second one loop from linked list 2 first. When they meet the end of the linked list, point it to the other linked list's head. They will always move same steps and meet null if there is no intersection, because the will always move the sum of both linked lists' length.

If there is intersection, they will always meet at intersection point after they both switch linked list. Because with intersection, it means that the final part of their loop is same. When they are at intersection point, they need the same amounts of steps to move to the end, so they will always meet at intersection points. 

## Solutions

~~~java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null) return null;
        ListNode loopA = headA;
        ListNode loopB = headB;
        while(loopA != loopB) {
            loopA = loopA == null ? headB : loopA.next;
            loopB = loopB == null ? headA : loopB.next;
        }
        return loopA;
    }
}
~~~



## Further

https://leetcode.com/problems/intersection-of-two-linked-lists/discuss/49785/Java-solution-without-knowing-the-difference-in-len!

https://leetcode.com/problems/intersection-of-two-linked-lists/discuss/49792/Concise-JAVA-solution-O(1)-memory-O(n)-time