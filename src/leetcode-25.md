# leetcode-algorithms-25 Reverse Nodes in k-Group

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

Example:
```
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5
```
Note:

Only constant extra memory is allowed.
You may not alter the values in the list's nodes, only nodes itself may be changed.

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
    ListNode* reverseKGroup(ListNode* head, int k)
    {
        ListNode d(-1);
        d.next = head;
        
        int count = 0;
        ListNode *pre_first = &(d);
        ListNode *first = pre_first;
        ListNode *second;
        ListNode *second_last;
        //count the list
        while(first = first->next) count++;
        while(count >= k)
        {
            first = pre_first->next; 
            second = first->next;
            //reverse the K node
            for (int i = 1; i < k; ++i)
            {
                second_last = second->next;
                second->next = pre_first->next;
                pre_first->next = second;
                first->next = second_last;
                second = second_last;
            }
            pre_first = first;
            count -= k;
        }
        
        return d.next;
    }
};
```
时间复杂度: O(n + k*(n/k)),n是链表的长度.

空间复杂度: O(1).