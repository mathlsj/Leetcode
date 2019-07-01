# leetcode-algorithms-147 Insertion Sort List

Sort a linked list using insertion sort.

A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.
With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list
 

Algorithm of Insertion Sort:

+ Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
+ At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
+ It repeats until no input elements remain.

Example 1:
```
Input: 4->2->1->3
Output: 1->2->3->4
```
Example 2:
```
Input: -1->5->3->4->0
Output: -1->0->3->4->5
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
    ListNode* insertionSortList(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
            return head;
        
        ListNode * d = new ListNode(-1);
        d->next = head;
        ListNode* current = head->next;
        ListNode* pre = head;
        
        while(current)
        {
            ListNode *find = d;
            if(pre->val > current->val)
            {
                while(find != pre && current->val > find->next->val)
                {
                    find = find->next;
                }
                ListNode * temp = find->next;
                find->next = current;
                pre->next = current->next;
                current->next = temp;
                current = pre->next;
  
            }
            else
            {
                pre = current;
                current = current->next;
            }
        }
        head = d->next;
        delete(d);
        d = nullptr;
        return head;   
    }
};
```