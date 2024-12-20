# [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists)

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by
splicing together the nodes of the first two lists.

Return *the head of the merged linked list*.

Constraints:

* The number of nodes in both lists is in the range `[0, 50]`.
* `-100 <= Node.val <= 100`
* Both `list1` and `list2` are sorted in **non-decreasing** order.

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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        // If one list is empty, return head of list that isn't empty.
        if (!list1 || !list2) {
            return list1 ? list1 : list2;
        }

        // Add the next call to the call stack based on which value is less,
        // returning the minimum node.
        if (list1->val <= list2->val) {
            list1->next = mergeTwoLists(list1->next, list2);
            return list1;
        } else {
            list2->next = mergeTwoLists(list1, list2->next);
            return list2;
        }
    }
};
```

## Analysis

Say we have the following lists:

* `list1 = 1->2->3->/`
* `list2 = 2->4->6->/`

Call stack (read bottom to top):

* `return list2` list1==nullptr
* `list1->next = mergeTwoLists(list1->next, list2)` 3<=4
* `list2->next = mergeTwoLists(list1, list2->next)` 3>2
* `list1->next = mergeTwoLists(list1->next, list2)` 2<=2
* `list1->next = mergeTwoLists(list1->next, list2)` 1<=2
* `ans = mergeTwoLists(list1, list2)` initial call

Calls result in:

* `list1->next = list2 = 4->6`
* `list2->next = list1 = 3->4->6`
* `list1->next = list2 = 2->3->4->6`
* `list1->next = list1 = 2->2->3->4->6`
* `ans = list1 = 1->2->2->3->4->6`

Order of elements:

```txt
list1 = 1->2->   3->
list2 =       2->   4->6->/
```

Time complexity is `O(m+n)` where `m` is the size of `list1` and `n` is the size
of `list2` as we have to traverse both lists.

Space complexity is `O(1)` due to not needing to allocate additional memory with
respect to the input.
