# 链表高频算法题
## 两个链表第一个公共子节点（LeetCode 160)
1. 哈希/集合<br><br>
把其中一个链表的元素全部存入集合里，遍历另一个链表。假如集合中存在当前节点，则代表两个链表一定有交点。
```Python
def getIntersectionNode1(self, headA, headB):
  s = set() # 创建一个集合
  p, q = headA, headB # 两个临时节点
  while p: # 把headA的链表元素加入集合
    s.add(p)
    p = p.next
  while q: # 查看交点
    if q in s:
      return q # 返回交点
    q = q.next
  return None # 没有交点
```
  
2. 栈<br><br>
先从尾节点循环找出第一个交点，假如两个链表有相交，后面的节点一定是一致的。
```Python
def getIntersectionNode2(self, headA, headB):
  stk1, stk2 = [], [] # 两个栈
  p, q = headA, headB # 两个临时节点
  # 把两个链表的元素加入两个栈
  while p:
    stk1.append(p)
    p = p.next
  while q:
    stk2.append(q)
    q = q.next
  ans = None
  i, j = len(stk1) - 1, len(stk2) - 1
  # 假如元素不相等表示没相交了
  while (i >= 0 and j >= 0 and stk1[i] == stk2[j]):
    ans = stk1[i]
    i, j = i - 1, j - 1
  return ans
```

3. 拼接两个字符串<br>
```Python
def getIntersectionNode3(self, headA, headB):
  nodeA, nodeB = headA, headB
  while nodeA != nodeB: 
      nodeA = nodeA.next if nodeA else headB
      nodeB = nodeB.next if nodeB else headA
  return nodeA
```

4. 差和双指针<br>
```Python
def getIntersectionNode(self, headA, headB):
  s1, s2 = 0, 0
  nodeA, nodeB = headA, headB
  while headA: 
      s1 += 1
      headA = headA.next 
  while headB: 
      s2 += 1
      headB = headB.next 
  for _ in range(s1 - s2): 
      nodeA = nodeA.next 
  for _ in range(s2 - s1): 
      nodeB = nodeB.next 
  while nodeA and nodeB and nodeA != nodeB: 
      nodeA = nodeA.next
      nodeB = nodeB.next 
  return nodeA
```
   
<br>

## 判断列表是否为回文序列（LeetCode 234）
```Python
def isPanlindrome(self, head):
  cur, length = head, 0
  res = []
  # 把链表元素都加入栈并且得到链表长度
  while cur:
    res.append(cur.val)
    length += 1
    cur = cur.next
  left, right = 0, len(res) - 1
  # 比较，假如不相等即不是回文，直接返回False
  while left < right:
    if res[left] != res[right]:
      return False
    left += 1
    right -= 1
  return True
```
<br>

## 合并有序链表（LeetCode 21）
```Python
def mergeTwoLists(self, list1, list2):
  dummy = ListNode(0)
  p = dummy 
  while list1 and list2: 
      if list1.val < list2.val: 
          p.next = list1
          list1 = list1.next
      else: 
          p.next = list2
          list2 = list2.next
      p = p.next
  
  if list1 or list2: # 假如还有未加入的元素
      p.next = list1 if list1 else list2
      
  return dummy.next
```
<br>

## 合并k个链表（LeetCode 23）
```Python
def mergeKLists(self, lists):
  def mergeTwoLists(list1, list2): 
      dummy = ListNode(-1)
      p = dummy

      while list1 and list2: 
          if list1.val <= list2.val: 
              p.next = list1
              list1 = list1.next
          else: 
              p.next = list2
              list2 = list2.next 
          p = p.next 

      p.next = list1 if list1 else list2
      return dummy.next

  if len(lists) == 0: 
      return None
  res = None
  for i in range(len(lists)): 
      res = mergeTwoLists(res, lists[i])
  return res
```
<br>

## 合并两个链表（LeetCode 1669）
```Python
def mergeInBetween(self, list1, a, b, list2):
  dummy = ListNode(-1)
  dummy.next = list1
  tmp1 = tmp2 = dummy 
  lst1, lst2 = a, b + 2
  for i in range(lst1): 
      tmp1 = tmp1.next
  for i in range(lst2): 
      tmp2 = tmp2.next
  tmp1.next = list2
  while list2.next: 
      list2 = list2.next
  list2.next = tmp2
  return dummy.next
```
<br>

## 寻找中间节点（LeetCode 876）
```Python
def findMiddleNode(self, head):
  slow = dummy
  fast = dummy
  # slow指针每次走一步，fast走两步
  while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
  return slow
```
<br>

## 寻找倒数第k的元素
```Python
def getKthFromEnd(self, head, k):
  former, latter = head, head
  for _ in range(k):
    if not former:
      return
    former = former.next
  while former:
    latter = latter.next
    former = former.next
  return latter
```
<br>

## 旋转链表（LeetCode 61）
```Python
def rotateRight(self, head, k):
  temp, fast, slow = head, head, head
  length = 0
  while head: 
      head = head.next 
      length += 1
  # 不需要旋转，结果和当前一样
  if k % length == 0: 
      return 
  while (k % length) > 0: 
      k -= 1
      fast = fast.next 
  while fast.next: 
      slow = slow.next 
      fast = fast.next 
  res = slow.next 
  slow.next = None
  fast.next = temp
  return res
```
<br>

## 删除特定节点（LeetCode 203）
```Python
def removeElements(self, head, val):
  while head and head.val == val: 
      head = head.next 
  if head is None: 
      return head
  dummy = head
  while head and head.next: 
      if head.next.val == val: 
          head.next = head.next.next 
      head = head.next 
  return dummy
```
<br>

## 删除倒数第n个节点（LeetCode 19）
1. 计算链表长度
```Python
def removeNthFromEnd(self, head, n):
  dummy = ListNode(0, head)
  cur = dummy
  def getListLength(head):
      length = 0
      while head: 
          length += 1
          head = head.next 
      return length
  
  length = getListLength(head)
  for _ in range(length - n): 
      cur = cur.next 
  
  cur.next = cur.next.next 
  return dummy.next
```

2. 双指针
```Python
def removeNthFromEnd(self, head, n):
  dummy = ListNode(0, head)
  fast = head
  slow = dummy 
  for _ in range(n): 
      fast = fast.next
  while fast: 
      fast = fast.next 
      slow = slow.next 
  slow.next = slow.next.next 
  return dummy.next
```
<br>

## 删除重复元素
1. 重复元素保留一个（LeetCode 83）
```Python
def deleteDuplicates(self, head):
  dummy = head
  while head: 
      if head.next and head.val == head.next.val:
          head.next = head.next.next 
      else: 
          head = head.next 
  return dummy
```
   
3. 重复元素不保留（LeetCode 82）
```Python
def deleteDuplicates(self, head):
  dummy = ListNode(0, head)
  cur = dummy 
  while cur.next:
      if cur.next.next and cur.next.val == cur.next.next.val: 
          x = cur.next.val
          while cur.next and cur.next.val == x: 
              cur.next = cur.next.next
      else:
          cur = cur.next
  return dummy.next
```
