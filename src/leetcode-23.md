# leetcode-algorithms-23 Merge k Sorted Lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

## 解法

将所有的list值插入multiset.再申请新的链表重新输出就可以.
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
    ListNode* mergeKLists(vector<ListNode*>& lists)
    {
        std::multiset<int> mset;
        for (auto iter = lists.begin(); iter != lists.end(); ++iter)
        {
            ListNode *l = *iter;
            while(l != NULL)
            {
                mset.insert(l->val);
                l = l->next;
            }
        }
        
        ListNode d(-1);
        ListNode *ld = &d;
        for (auto it = mset.begin(); it != mset.end(); ++it)
        {
            ListNode *n = new ListNode(*it);
            ld->next = n;
            ld = ld->next;            
        }
        
        return d.next;
    }
};
```
时间复杂度: O(n*logn),n是所有list的长度,logn是插入multiset的时间.

空间复杂度: O(n).