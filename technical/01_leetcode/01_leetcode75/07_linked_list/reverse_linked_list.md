# [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)

Given the `head` of a singly linked list, reverse the list, and return the
*reversed list*.

Constraints:

* The number of nodes in the list is the range `[0, 5000]`.
* `-5000 <= Node.val <= 5000`

## Solution

```c++
/*
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* n = head;
        ListNode* c = head;
        ListNode* t = nullptr;
        while (c != nullptr) {
            n = c->next;
            c->next = t;
            t = c;
            c = n;
        }

        return t;
    }
};
```

## Analysis

Time complexity is `O(n)` since we're iterating over the entire list, flipping
the `next` pointers along the way.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to the input.
