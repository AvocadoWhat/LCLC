# Day 3 Linked list

## 1. Dummy head
### 203. Remove linked list elements $\color{orange}{\textsf{MEDIUM}}$

> Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, 
> and return the new head.

> Example 1:
> Input: Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        dummy_head = ListNode(next = head)
        
        # 遍历列表并删除值为val的节点
        current = dummy_head
        while current.next:
            if current.next.val == val:
                current.next = current.next.next
            else:
                current = current.next
        
        return dummy_head.next
```

Approach: dummy head. When there is a need to edit/add/remove the element in a linked list, a dummy head is 
recommended. Because by adding a dummy head, the loop can go directly from the real first element in the linked list. 

Key points:
1. only when the pointer (address and value) of an element equals another, the two notes are the same; only the 
   value being the same doesn't mean they are equal
2. in linked list
   - assigning values doesn't change the pointer of a node
   - assigning the pointer DOES change the node completely, so when `current.next = xyz`, the pointer has changed. 
     If the `xyz` is not another node of the linked list, this list has broken; otherwise, it's still linked.
Assigning the next node is often used in swapping nodes, reverse list order, etc.




### 203. Reverse Linked List $\color{orange}{\textsf{MEDIUM}}$

>Given the head of a singly linked list, reverse the list, and return the reversed list.

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
   def reverseList(self, head):
      cur = head # assign first element to cur
      pre = None # assign null to pre
      
      while cur:
         temp = cur.next # save the second element to temp
         
         cur.next = pre # assign pre to the second element (this decides the direction or linkage)
         pre = cur # assign cur to pre
         
         cur = temp # update cur to temp
```

Approach: dummy head -> swap (two pointers)
Key points:
1. create 2 pointers: pre->None, cur->head
2. while loop stops when cur pointer exhausts all nodes
3. create a backup node, temp -> cur.next, so that after swapping cur and pre in each iteration, this list doesn't 
   get lost/broken, and temp is the "head" after swapping (actually dropping cur node)
4. do the swap -> update cur, pre -> enter the next iteration


