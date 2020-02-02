# leetcode-algorithms-206 Reverse Linked List

Reverse a singly linked list.

### Example:

Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL

### Follow up: 

A linked list can be reversed either iteratively or recursively. Could you implement both?

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
    ListNode* reverseList(ListNode* head) {
        ListNode d(-1);
        d.next = nullptr;
        
        ListNode *p = head;
        while (p != nullptr) {
            ListNode *t = d.next;
            d.next = p;
            
            ListNode *p1 = p->next;
            p->next = t;
            
            p = p1;
        }
        
        return d.next;
    }
};
```