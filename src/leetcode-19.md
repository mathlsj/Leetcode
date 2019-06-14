# leetcode-algorithms-19 Remove Nth Node From End of List

Given a linked list, remove the n-th node from the end of list and return its head.

Example:
```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```
Note:

Given n will always be valid.

Follow up:

Could you do this in one pass?

## 解法

O(n)内删除倒序第n个结点要一个循环找到第n个结点,可用两个链表指针,第一个比第二个多n个结点,当第一个到达末尾时,第二个就是倒序的n个结点.
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
    ListNode* removeNthFromEnd(ListNode* head, int n)
    {
        if (head == nullptr) return nullptr;
        
        ListNode d(-1);
        d.next = head;
        
        ListNode *first = &d;
        ListNode *second = &d;
        for(int i = 0; i < n; ++i) first = first->next;
        
        while(first->next)
        {
            first = first->next;
            second = second->next;
        }
        
        ListNode *del = second->next;
        second->next = second->next->next;
        delete del;
        
        return d.next;        
    }
};
```
空间复杂度: O(n).

时间复杂度: O(1).