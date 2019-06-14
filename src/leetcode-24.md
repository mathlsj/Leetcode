# leetcode-algorithms-24 Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

Example:
```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```
Note:

Your algorithm should use only constant extra space.
You may not modify the values in the list's nodes, only nodes itself may be changed.

## 解法

一个链表指针指向链表的首地址,这个用来改变node的值,且将指针后移.
再申明两个链表指针,其中一个指针b是另个指针a的下个值(b = a->next).
现在循环处理.
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
    ListNode* swapPairs(ListNode* head)
    {        
        ListNode **l = &head;
        ListNode *a = nullptr;
        ListNode *b = nullptr;
        while((a = *l) && (b = a->next))
        {
            a->next = b->next;
            b->next = a;
            *l = b;
            l = &(a->next);
        }
        return head;
    }
};
```
时间复杂度: O(n).

空间复杂度: O(1).