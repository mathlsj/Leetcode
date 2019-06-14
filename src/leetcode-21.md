# leetcode-algorithms-21 Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
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
class Solution
{
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2)
    {
        if (l1 == nullptr && l2 == nullptr) return nullptr;
        
        ListNode *head = new ListNode(0);
        ListNode *l = head;
        while(l1 != nullptr && l2 != nullptr)
        {
            if (l1->val <= l2->val)
            {
                l->next = l1;
                l1 = l1->next;
            }
            else
            {
                l->next = l2;
                l2 = l2->next;
            }
            l = l->next;
        }
        l->next= l1 ? l1 : l2;
        
        return head->next;
    }
};
```
