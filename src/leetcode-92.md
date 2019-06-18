# leetcode-algorithms-92. Reverse Linked List II

Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

Example:

```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

## 解法

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        ListNode d(-1);
        d.next = head;
        ListNode *pre_first = &d;
        for (int i = 1; i < m; ++i) {
            pre_first = pre_first->next;
        }
        
        ListNode *first = pre_first->next;
        ListNode *second;
        ListNode *second_last;
        if (first->next != nullptr)
            second = first->next;
        
        for (int i = 0; i < n - m; ++i) {
            second_last = second->next;
            second->next = pre_first->next;
            pre_first->next = second;
            first->next = second_last;
            second = second_last;
        }
        
        return d.next;  
    }
};
```

时间复杂度： O(n)，n 反转的的结点 index 值。

空间复杂度： O(1)。