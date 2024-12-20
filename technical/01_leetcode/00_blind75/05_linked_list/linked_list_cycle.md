# [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle)

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be
reached again by continuously following the `next` pointer. Internally, `pos` is
used to denote the index of the node that tail's `next` pointer is connected to.
**Note that `pos` is not passed as a parameter**.

Return `true` *if there is a cycle in the linked list*. Otherwise, return
`false`.

Constraints:

* The number of the nodes in the list is in the range `[0, 10^4]`.
* `-10^5 <= Node.val <= 10^5`
* `pos` is `-1` or a valid index in the linked-list.

## Solution

```c++
/*
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        // Slow and fast pointers.
        // Slow will traverse each node, one by one.
        // Fast will traverse every other node.
        ListNode* slowPtr = head;
        ListNode* fastPtr = head;

        // Traverse the list.
        // If there is a cycle, it is guaranteed that the fast pointer will
        // eventually cycle around and meet with the slow pointer.
        // Otherwise, it will reach the end of the list.
        while (fastPtr && fastPtr->next) {
            slowPtr = slowPtr->next;
            fastPtr = fastPtr->next->next;
            if (slowPtr == fastPtr) {
                return true;
            }
        }

        return false;
    }
};
```

## Analysis

Time complexity is `O(n)` due to having to traverse the list once.

Space complexity is `O(1)` since we do not need to allocate additional memory
with respect to input size.
