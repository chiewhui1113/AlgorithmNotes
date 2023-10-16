# 链表反转
## 反转链表（LeetCode 206）
1. 建立虚拟头节点<br><br>
![算法-7](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/8f264d0c-db06-45fa-8867-abaef997eaec)
```Python
def reverseList(self, head):
  if not head or not head.next: 
      return head 
  dummy = ListNode(-1)
  cur = head
  while cur: 
      next = cur.next 
      cur.next = dummy.next 
      dummy.next = cur
      cur = next 
  return dummy.next 
```
<br>

3. 用三指针<br><br>
![算法-7](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/4c12ea3e-746f-4160-9190-a8bed01fceee)
```Python
def reverseList(self, head):
  if not head or not head.next: 
      return head 
  cur = head.next 
  head.next = None 
  while cur: 
      next = cur.next 
      cur.next = head
      head = cur
      cur = next 
  return head
```
<br>

5. 递归<br><br>
![算法-7](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/cdf508f1-63e0-4b19-8cd1-46aaca5e7dac)
```Python
def reverseList(self, head):
  if not head or not head.next: 
      return head 
  p = self.reverseList(head.next)
  head.next.next = head
  head.next = None
  return p
```
