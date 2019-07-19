# leetcode-algorithms-203 Remove Linked List Elements

Remove all elements from a linked list of integers that have value val.

Example:
```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode d(-1);
        d.next = head;
        
        ListNode *prev = &d;
        ListNode *p = prev->next;
        while (p != nullptr) {
            if (p->val == val) {
                ListNode *temp = p;
                p = p->next;
                prev->next = p;
                delete temp;
                temp = nullptr;
            } else {
                prev = prev->next;
                p = p->next;
            }
        }
        
        return d.next;
    }
};
```