# leetcode-algorithms-142 Linked List Cycle II

Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

Note: Do not modify the linked list.

 

Example 1:
```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![circularlinkedlist](../image/circularlinkedlist.png)

Example 2:
```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![circularlinkedlist_test2](../image/circularlinkedlist_test2.png)

Example 3:
```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

![circularlinkedlist_test3](../image/circularlinkedlist_test3.png) 

Follow-up:
Can you solve it without using extra space?

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
    ListNode *detectCycle(ListNode *head) {        
        ListNode *one_step = head;   
        ListNode *two_step = head;
        while(one_step != nullptr && two_step != nullptr) {
            one_step = one_step->next;
            two_step = (two_step->next == nullptr) ? nullptr : two_step->next->next; 
            if (two_step == nullptr)
                return nullptr;
            
            // found cycle
            if (one_step == two_step)
                break;
        }
        
        two_step = head;
        while (one_step != two_step) {
            one_step = one_step->next;
            two_step = two_step->next;
        }
        return one_step;
    }
};
```