# 链表反转
## 反转链表（LeetCode 206）
1. 建立虚拟头节点<br><br>
![算法-7](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/8f264d0c-db06-45fa-8867-abaef997eaec)
```Python
def reverseList(head):
  if not head or not head.next: 
      return head 
  dummy = ListNode(-1, head)
  cur = head
  while cur: 
      next = cur.next 
      cur.next = dummy.next 
      dummy.next = cur
      cur = next 
  return dummy.next 
```
<br>

2. 用三指针<br><br>
![算法-7](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/4c12ea3e-746f-4160-9190-a8bed01fceee)
```Python
def reverseList(head):
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

3. 递归<br><br>
![算法-7](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/cdf508f1-63e0-4b19-8cd1-46aaca5e7dac)
```Python
def reverseList(head):
  if not head or not head.next: 
      return head 
  p = self.reverseList(head.next)
  head.next.next = head
  head.next = None
  return p
```
<br>

### 指定区间反转（LeetCode 92）
1. 头插法<br>
<img width="623" alt="image" src="https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/9b5be559-0be1-4a66-a343-c96688890166">

```Python
def reverseBetween(head, left, right):
  dummy = ListNode(-1, head)
  pre = dummy 
  for _ in range(left - 1): 
      pre = pre.next 
  cur = pre.next 
  for _ in range(right - left): 
      next = cur.next 
      cur.next = next.next 
      next.next = pre.next 
      pre.next = next
  return dummy.next 
```
<br>

2. 裁缝法<br>
<img width="611" alt="image" src="https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/40681aac-62d3-4d3e-81d5-0a39a39079f2">

```Python
def reverseList(head): 
  dummy = ListNode(-1, head)
  cur = head
  while cur: 
      next = cur.next 
      cur.next = dummy 
      dummy = cur
      cur = next 


def reverseBetween(head, left, right):
  dummy = ListNode(-1, head)
  pre = dummy 
  for _ in range(left - 1): 
      pre = pre.next 
  leftNode = pre.next 
  rightNode = leftNode 
  for _ in range(right - left): 
      rightNode = rightNode.next
  cur = rightNode.next 
  pre.next = None 
  rightNode.next = None 
  reverseList(leftNode)
  pre.next = rightNode 
  leftNode.next = cur
```
<br>

### 两两交换链表中的节点（LeetCode 24）
```Python
def swapPairs(head):
  dummy = ListNode(-1, head)
  temp = dummy 
  while temp.next and temp.next.next: 
      node1 = temp.next 
      node2 = temp.next.next 
      node1.next = node2.next 
      temp.next = node2
      node2.next = node1 
      temp = node1
  return dummy.next 
```
<br>

### 单链表加一（LeetCode 369）
1. 栈<br>
```Python
def plusOne1(head):
  stk = []
  while head:
    stk.append(head.val)
    head = head.next

  carry = 0
  adder = 0
  dummy = ListNode(0)
  while stk or carry > 0:
    digit = 0 if not stk else stk.pop()
    sum = digit + carry + adder
    carry = 0 if sum < 10 else 1
    if sum >= 10:
      sum -= 10
    newDigit = ListNode(sum)
    newDigit.next = dummy.next
    dummy.next = newDigit
    adder = 0
  return dummy.next
```
2. 找最后一个9
```Python
def plusOne2(head):
  dummy = ListNode(0, head)
  not_nine = dummy
  while head:
    if head.val != 9:
      not_nine = head
    head = head.next
  not_nine.val += 1
  not_nine = not_nine.next
  while not_nine:
    not_nine.val = 0
    not_nine = not_nine.next
  return dummy if dummy else dummy.next  
```
3. 链表反转
```Python
def reverseList(self, head): 
  if not head or not head.next: 
      return head
  p = self.reverseList(head.next)
  head.next.next = head 
  head.next = None 
  return p

def plusOne(self, head):
  dummy = ListNode(0, self.reverseList(head))
  cur = dummy.next
  if cur.val < 9: 
    cur.val += 1
  else: 
    while cur.val == 9 and cur: 
      cur.val = 0
      cur = cur.next
    if cur: 
      cur.val += 1
    else: 
      cur.val = 1
  return self.reverseList(dummy.next)
```
<br>

### 链表加法（LeetCode 445）
1. 栈
```Python
def addTwoNumbers(self, l1, l2):
  stk1 = []
  stk2 = []
  while l1: 
      stk1.append(l1.val)
      l1 = l1.next 
  while l2: 
      stk2.append(l2.val)
      l2 = l2.next 
  carry = 0
  dummy = ListNode(-1)
  while stk1 or stk2 or carry: 
      num1 = stk1.pop() if stk1 else 0 
      num2 = stk2.pop() if stk2 else 0 
      sum = num1 + num2 + carry 
      carry = 1 if sum >= 10 else 0 
      sum = sum - 10 if sum >= 10 else sum 
      newNode = ListNode(sum)
      newNode.next = dummy.next 
      dummy.next = newNode 
  return dummy.next 
```
2. 反转链表
```Python
def reverseList(self, head): 
    if not head or not head.next: 
        return head 
    p = self.reverseList(head.next)
    head.next.next = head 
    head.next = None 
    return p

def addTwoNumbersI(self, l1, l2): 
    ans = ListNode(0)
    dummy = ans 
    carry = 0
    while l1 or l2 or carry: 
        ans.next = ListNode(0)
        ans = ans.next 
        if l1 and l2: 
            sum = carry + l1.val + l2.val 
            carry = 1 if sum >= 10 else 0 
            sum = sum - 10 if sum >= 10 else sum 
            l1 = l1.next 
            l2 = l2.next 
            ans.val = sum 
        elif l1: 
            sum = carry + l1.val 
            carry = 1 if sum >= 10 else 0 
            sum = sum - 10 if sum >= 10 else sum 
            l1 = l1.next 
            ans.val = sum 
        elif l2: 
            sum = carry + l2.val 
            carry = 1 if sum >= 10 else 0 
            sum = sum - 10 if sum >= 10 else sum 
            l2 = l2.next 
            ans.val = sum 
        else: 
            ans.val = carry 
            carry = 0
    return dummy.next 

def addTwoNumbers(self, l1, l2):
    return self.reverseList(self.addTwoNumbersI(self.reverseList(l1), self.reverseList(l2)))
```
<br>

### 链表回文序列（LeetCode 234）
```Python
def isPalindrome(self, head):
  dummy = ListNode(-1, head)
  fast = slow = dummy 

  while fast and fast.next: 
      slow = slow.next 
      fast = fast.next.next 
  
  post = slow.next 
  slow.next = None 

  rev = None
  while post: 
      next = post.next 
      post.next = rev 
      rev = post 
      post = next 
  
  part1 = head 
  part2 = rev 
  while part1 and part2: 
      if part1.val != part2.val: 
          return False
      part1 = part1.next 
      part2 = part2.next 
  
  return True
```
<br>

### K个一组反转（LeetCode 25）
```Python
def reverseKGroup(head, k):
  dummy = ListNode(0, head)
  pre = tail = dummy 
  while True: 
      count = k
      while count and tail: 
          count -= 1
          tail = tail.next 
      if not tail: 
          break 
      head = pre.next 
      while pre.next != tail: 
          cur = pre.next 
          pre.next = cur.next 
          cur.next = tail.next 
          tail.next = cur
      pre = tail = head
  return dummy.next
```

```Python
def reverseKGroup(self, head, k):
  dummy = ListNode(0, head)
  pre = end = dummy 
  while end.next: 
      i = 0
      while i < k and end: 
          end = end.next 
          i += 1
      if not end: 
          break
      start = pre.next 
      nextNode = end.next 
      end.next = None 
      pre.next = reverse(start)
      start.next = nextNode 
      pre = start 
      end = pre
  return dummy.next
  
def reverse(head): 
  pre = None
  cur = head
  while cur: 
      nextNode = cur.next 
      cur.next = pre
      pre = cur 
      cur = nextNode
  return pre
```
