# leetcode-algorithms-141. Linked List Cycle

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

### Example 1:
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![](circularlinkedlist_141.png)

### Example 2:
```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![](circularlinkedlist_test2_141.png)

### Example 3:
```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

![](circularlinkedlist_test3_141.png)

### Follow up:

Can you solve it using O(1) (i.e. constant) memory?


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
    bool hasCycle(ListNode *head) {
        if (head == nullptr)
            return false;
        
        ListNode *one_step = head;   
        ListNode *two_step = head->next;
        while(one_step != two_step) {
            if (two_step == nullptr || two_step->next == nullptr)
                return false;
            one_step = one_step->next;
            two_step = two_step->next->next;
        }
        
        return true;
    }
};
```