## 19.Remove Nth Node From End of List
>    
Given a linked list, remove the n-th node from the end of list and return its head.   
Example:    
Given linked list: 1->2->3->4->5, and n = 2.   
After removing the second node from the end, the linked list becomes 1->2->3->5.   
Note:   
Given n will always be valid.

删除链表中某个节点，就需要获取此节点的上一个节点。   
对于这个题目，我们可以设置一个虚拟头结点来降低代码的复杂度，然后定义两个指针`p`和`q`,`q`指针先往前移动`n+1`个节点，之后`p`指针和`q`指针同时往前移动，当`q`指针到达链表的尾节点的时候，`p`指针指向的节点恰好时第`n`个节点的上一个节点，此时再进行删除操作
```
ListNode* removeNthFromEnd(ListNode* head, int n) {
    assert( n > = 0 )

    ListNode* dummyHead = new ListNode(0);
    dummyHead->next = head;

    ListNode* p = dummyHead;
    ListNode* q = dummyHead;

    for( int i = 0; i < n + 1; i ++ ) {
        assert(q);
        q = q->next;
    }

    while( q != NULL ) {
        p = p->next;
        q = q->next;
    }

    ListNode* delNode = p->next;
    p->next = delNode->next;
    delete delNode;

    ListNode* retNode = dummyHead->next;
    delete dummyHead;

    return retNode;

}
```
## 24.Swap Nodes in Pairs
>    
Given a linked list, swap every two adjacent nodes and return its head.    
Example:    
Given 1->2->3->4, you should return the list as 2->1->4->3.   
Note:    
Your algorithm should use only constant extra space.
You may not modify the values in the list's nodes, only nodes itself may be changed.

依然使用设置虚拟头结点的方法来解此题
```
ListNode* swapPairs(ListNode* head) {
    ListNode* dummyHead = new ListNode(0);
    dummyHead->next = head;

    ListNode* p = dummyHead;
    while( p->next && p->next->next ) {
        ListNode* node1 = p->next;
        ListNode* node2 = node1->next;
        ListNode* next = node2->next;

        node2->next = node1;
        node1->next = next;
        p->next = node2;

        p = node1;
    }

    ListNode* retNode = dummyHead->next;
    delete dummyHead;

    return retNode;
}
```
## 203.Remove Linked List Elements
>    
Remove all elements from a linked list of integers that have value val.    
Example:    
Input:  1->2->6->3->4->5->6, val = 6    
Output: 1->2->3->4->5

通常删除链表中的一个节点，需要获取当前要删除节点`cur`的上一个节点`pre`,然后将`pre->next = cur->next`, 再删除`cur`节点即可。而如果要删除的节点是头结点，那么我们还需要重新写一段逻辑来处理，考虑的情况会比较复杂。   
此时我们可以设置一个虚拟的头结点来处理，删除完需要删除的节点之后再将虚拟的头结点删除即可。
```
ListNode* removeElements(ListNode* head, int val) {
    ListNode* dummyHead = new ListNode(0);
    dummyHead->next = head;

    ListNode* cur = dummyHead;
    while( cur->next != NULL ) {
        if( cur->next->val == val ) {
            ListNode* delNode = cur->next;
            cur->next = delNode->next;
            delete delNode;
        }
        else
            cur = cur->next;
    }

    ListNode* retNode = dummyHead->next;
    delete dummyHead;

    return retNode;
}
```
## 206.Reverse Linked List
>  
Reverse a singly linked list.   
Example:   
Input: 1->2->3->4->5->NULL  
Output: 5->4->3->2->1->NULL   

反转链表是非常常见的一道算法题,也非常简单。需要当前节点，当前的上一个节点以及当前节点的下一个节点来进行反转操作
```
ListNode* reverseList(ListNode* head) {
    ListNode* pre = NULL;
    ListNode* cur = head;

    while( cur->next != NULL ) {
        ListNode* next = cur->next;

        cur->next = pre;
        pre = cur;
        cur = next;
    }

    return pre;
}

```

## 237.Delete Node in a Linked List
>   
Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.   
Given linked list -- head = [4,5,1,9], which looks like following:   
4 -> 5 -> 1 -> 9   
Example 1:    
Input: head = [4,5,1,9], node = 5
Output: [4,1,9]
Explanation: You are given the second node with value 5, the linked list
             should become 4 -> 1 -> 9 after calling your function.                 
Example 2:    
Input: head = [4,5,1,9], node = 1   
Output: [4,5,9]    
Explanation: You are given the third node with value 1, the linked list
             should become 4 -> 5 -> 9 after calling your function.   
Note:    
The linked list will have at least two elements.
All of the nodes' values will be unique.
The given node will not be the tail and it will always be a valid node of the linked list.
Do not return anything from your function.

通常删除链表中的一个节点，需要获取当前要删除节点`cur`的上一个节点`pre`,然后将`pre->next = cur->next`, 再删除`cur`节点即可。但是这道题只给出了当前要删除的节点，因为是单向链表，就不能得到当前要删除节点的上一个节点。当然如果遍历一遍链表是能找到的，但是时间复杂度是O(n)。有更好的方法：  
我们要删除节点`cur`，先把`cur`下一个节点`next`的内容复制给`cur`，然后把`cur`的指针指向节点`next`的下一个节点。此时再删除节点`next`，其效果刚好是把节点`cur`删除了。    
时间复杂度为O(1)
```
void deleteNode(ListNode* node) {
    if( node == NULL ) {
        return;
    }

    if( node->next == NULL ) {
        delete node;
        node = NULL;
        return;
    }

    node->val = node->next->val;
    ListNode* delNode = node->next;
    node->next = delNode->next;

    delete delNode;

    return;
}
```  
