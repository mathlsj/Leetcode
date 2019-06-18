# leetcode-algorithms-109. Convert Sorted List to Binary Search Tree

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:

```
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
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
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* converListToBST(std::vector<int> &v, int left, int right) {
        if (left > right)
            return nullptr;
        
        int mid = (left + right) / 2;
        TreeNode* node = new TreeNode(v[mid]);
        
        if (left == right)
            return node;
        
        node->left = converListToBST(v, left, mid - 1);
        node->right = converListToBST(v, mid + 1, right);
        return node;
    }
    
    TreeNode* sortedListToBST(ListNode* head) {
        std::vector<int> v;
        while(head != nullptr) {
            v.push_back(head->val);
            head = head->next;
        }
        
        return converListToBST(v, 0, v.size() - 1);
    }
    
};
```