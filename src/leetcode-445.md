# leetcode-algorithms-445 Add Two Numbers II

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

### Example:

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        if (l1 == nullptr)
            return l2;
        if (l2 == nullptr)
            return l1;
        
        std::stack<int> s1;
        while (l1 != nullptr) {
            s1.push(l1->val);
            l1 = l1->next;
        }
        
        std::stack<int> s2;
        while (l2 != nullptr) {
            s2.push(l2->val);
            l2 = l2->next;
        }
        
        ListNode *l = nullptr;
        int left = 0;
        while (!s1.empty() || !s2.empty()) {
            int val = left;
            if (!s1.empty()) {
                val += s1.top();
                s1.pop();
            }
            
            if (!s2.empty()) {
                val += s2.top();
                s2.pop();
            }
            
            left = val / 10;
            val %= 10;
            ListNode *n = new ListNode(val);
            n->next = l;
            l = n;            
        }
        
        if (left > 0) {
            ListNode *n = new ListNode(left);
            n->next = l;
            l = n;
        }
        
        return l;        
    }
};
```