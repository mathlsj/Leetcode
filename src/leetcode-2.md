## leetcode-algorithms-2 Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## 解法

同时遍历两个链表,对值进行相加.得到的值%10就是新的链表的值,同时存下/10(只可能是1)的值,用于下个位数的增值.

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2)
    {
        ListNode *l = nullptr;
        ListNode *lt = nullptr;
        ListNode *node1 = l1;
        ListNode *node2 = l2;
        int lastaddval = 0;
        while(true)
        {
            if (node1 == nullptr && node2 == nullptr) break;

            int nodeval1 = 0;
            int nodeval2 = 0;
            if (node1 != nullptr)
            {
                nodeval1 = node1->val;
                node1 = node1->next;
            }
            if (node2 != nullptr)
            {
                nodeval2 = node2->val;
                node2 = node2->next;
            }
            int sumval = nodeval1 + nodeval2 + lastaddval;
            lastaddval = sumval / 10;
            if (l == nullptr)
            {
                l = new ListNode(sumval % 10);
                lt = l;
            }
            else
            {
                ListNode *n = new ListNode(sumval % 10);
                lt->next = n;
                lt = n;
            }
        }
        if (lastaddval != 0)
        {
            ListNode *n = new ListNode(lastaddval);
            lt->next = n;
            lt = n;
        }
        return l;
    }
};
```

时间复杂度: O(max(m,n)).m和n分别是l1和l2的长度.

空间复杂度: O(max(m,n)).