# leetcode-algorithms-707. Design Linked List

Design your implementation of the linked list. You can choose to use the singly linked list or the doubly linked list. A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node. If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement these functions in your linked list class:

+ get(index) : Get the value of the index-th node in the linked list. If the index is invalid, return -1.
+ addAtHead(val) : Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
+ addAtTail(val) : Append a node of value val to the last element of the linked list.
+ addAtIndex(index, val) : Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
+  deleteAtIndex(index) : Delete the index-th node in the linked list, if the index is valid.
 

### Example:

```
Input: 
["MyLinkedList","addAtHead","addAtTail","addAtIndex","get","deleteAtIndex","get"]
[[],[1],[3],[1,2],[1],[1],[1]]
Output:  
[null,null,null,null,2,null,3]

Explanation:
MyLinkedList linkedList = new MyLinkedList(); // Initialize empty LinkedList
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1, 2);  // linked list becomes 1->2->3
linkedList.get(1);            // returns 2
linkedList.deleteAtIndex(1);  // now the linked list is 1->3
linkedList.get(1);            // returns 3
```

### Constraints:

+ 0 <= index,val <= 1000
+ Please do not use the built-in LinkedList library.
+ At most 2000 calls will be made to get, addAtHead, addAtTail,  addAtIndex and deleteAtIndex.

## solution

```
class MyLinkedList {
    struct node {
        int val;
        node *next;
    };
private:
    node *head;
    node *tail;
    int size;
public:
    /** Initialize your data structure here. */
    MyLinkedList() {
        head = nullptr;
        tail = nullptr;
        size = 0;
    }
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    int get(int index) {
        if (index >= size) {
            return -1;
        }
        
        int currIndex = 0;
        node * p = head;
        while (p != nullptr) {
            if (currIndex == index) {
                return p->val;
            }
            currIndex++;
            p = p->next;
        }
        return -1;
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    void addAtHead(int val) {
        node *p = new(node);
        p->val = val;
        p->next = head;
        head = p;
        if (size == 0) {
            tail = p;
        }
        size += 1;
    }
    
    /** Append a node of value val to the last element of the linked list. */
    void addAtTail(int val) {
        node *p = new(node);
        p->val = val;
        p->next = nullptr;
        tail->next = p;
        tail = p;
        if (size == 0) {
            head = p;
        }
        size += 1;
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }
        
        if (index == 0) {
            addAtHead(val);
            return;
        }
        
        if (index == size) {
            addAtTail(val);
            return;
        }
        
        node *p = new(node);
        p->val = val;
        
        int currIndex = 0;
        node *curr = head;
        while (curr != nullptr) {
            if (currIndex == index -1) {
                node *temp = curr->next;
                curr->next = p;
                p->next = temp;
                size += 1;
                return;
            }
            currIndex++;
            curr = curr->next;
        }
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    void deleteAtIndex(int index) {
        if (index >= size) {
            return;
        }
        
        if (index == 0) {
            node *p = head;
            head = head->next;
            size -= 1;
            if (size == 0) {
                tail = nullptr;
            }
            delete p;
            p = nullptr;
            return;
        }
        
        node *curr = head;
        int currIndex = 0;
        while (curr != nullptr) {
            if (currIndex == index - 1) {
                node *temp = curr->next;
                curr->next = temp->next;
                delete temp;
                temp = nullptr;
                size -= 1;
                if (currIndex == size - 1) {
                    tail = curr;
                }
                return;
            }
            curr = curr->next;
            currIndex++;
        }
    }
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```
