# leetcode-algorithms-234 Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

### Example 1:

```
Input: 1->2
Output: false
```

### Example 2:

```
Input: 1->2->2->1
Output: true
```

### Follow up:

Could you do it in O(n) time and O(1) space?

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
    bool isPalindrome(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
            return true;
        
        ListNode *slow = head;
        ListNode *fast = head;
        ListNode *pre = nullptr;
        ListNode *last = nullptr;
        // 找中间结点，将前半部分反转。
        while (fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            last = slow->next;
            slow->next = pre;
            pre = slow;
            slow = last;
        }
        
        // 如果是奇数个，去除最中间的结点。
        if (fast != nullptr)
            slow = slow->next;
        
        while (slow != nullptr) {
            if (slow->val != pre->val)
                return false;
            slow = slow->next;
            pre = pre->next;
        }
        
        return true;
    }
};
```