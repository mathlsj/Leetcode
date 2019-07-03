# leetcode-algorithms-148 Sort List

Sort a linked list in O(n log n) time using constant space complexity.

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
    ListNode* sortList(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
            return head;
        
        return mergeSort(head);
    }
  
    ListNode* mergeSort(ListNode* l) {
        if (l == nullptr || l->next == nullptr)
            return l;
        
        ListNode* mid = findMid(l);
        ListNode* last = mid->next;
        mid->next = nullptr;
        
        ListNode* left = mergeSort(l);
        ListNode* right = mergeSort(last);
        return mergeTwo(left, right);
    }
    
    ListNode* mergeTwo(ListNode* left, ListNode* right) {
        if (left == nullptr) return right;
        if (right == nullptr) return left;
        
        ListNode d(-1);
        ListNode* curr = &d;
        while(left != nullptr && right != nullptr) {
            if (left->val < right->val) {
                curr->next = left;
                left = left->next;
            } else {
                curr->next = right;
                right = right->next;
            }
            curr = curr->next;
        }
        
        if (left != nullptr) curr->next = left;
        if (right != nullptr) curr->next = right;
        
        return d.next;       
    }
    
    ListNode* findMid(ListNode* l) {
        ListNode* slow = l;
        ListNode* fast = l;
        ListNode* pre = nullptr;
        while(fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            pre = slow;
            slow = slow->next;         
        }
        
        return pre;
    }
};
```