# 链表中环的问题
## 判断是否有环（LeetCode 141）
1. 集合 <br>
```Python
def hasCycle(self, head):
  seen = set()
  while head: 
      if head.val in seen: 
          return True
      seen.add(head.val)
      head = head.next
  return False  
```

2. 双指针 <br><br>
一个快指针每次都会走两步，慢指针走一步。假如存在环，两个指针一定会在某个位置相遇。<br><br>
在第一种情况，慢指针和快指针只隔了一个位，只需要一步就能相遇<br>
在第二种情况，慢指针和快指针隔了两个位，下一步就会走到第一步的情况，需要两步相遇<br><br>
![level_1 drawio](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/dfc21a36-87b1-484f-ba9b-5a216dcf378e)
<br>

```Python
def hasCycle(self, head):
  if head is None or head.next is None: 
      return False 
  fast, slow = head, head 
  while fast and fast.next: 
      fast = fast.next.next 
      slow = slow.next 
      if fast == slow: 
          return True
  return False  
```

&nbsp;&nbsp; **怎么确定环的入口** <br>
&nbsp;&nbsp; 用fast和slow指针找到了相遇的位置后，把其中一个指针放在链表头。以相同，每次一步前进，再次相遇的位置即是环的入口。<br>
1. **转一圈相遇**：<br>
a. fast指针走了a+b+c+b步在Z点相遇<br>
b. slow指针走了a+b步在Z点相遇<br>
c. fast指针走过的距离是slow指针的两倍，因此 2(a+b) = a+b+c+b，a=c<br>
d. fast指针在起点，slow指针在Z点，两个指针各走一步即会在入口（Y点）相遇<br><br>
2. **转多圈相遇:** <br>
a. fast指针在环里走了n圈在Z点相遇<br>
&nbsp;&nbsp;&nbsp;&nbsp; a+n(b+c)+b = a+(n+1)b+nc<br>
b. slow指针走了a+b步在Z点相遇<br>
c. fast指针走过的距离是slow指针的两倍，因此 2(a+b) = a+(n+1)b+nc，a=c+(n-1)LEN（LEN是b+c，环的长度）<br>
d. fast指针在起点，slow指针在Z点，两个指针会在入口（Y点）相遇，相遇的时候slow指针已经在环里转了n-1圈<br><br>

![level_1_cycle drawio](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/ea1c60fb-38a1-4f7b-af9e-992830cc97a9)

```Python
def detectCycle(self, head):
  pos = 0
  fast, slow = head, head 
  while True: 
      if not (fast.next and fast.next.next): 
          return None
      fast = fast.next.next 
      slow = slow.next 
      if fast == slow: 
          break 
  fast = head 
  while fast != slow:
      pos += 1 
      fast = fast.next 
      slow = slow.next
  return fast
```
3. 三次双指针 <br><br>
a. 用fast和slow指针判断是否有环<br>
b. 用双指针判断环的大小，fast指针在相遇点不动，slow指针一步一步移动，移动的总步数为环的长度K<br>
c. 使用倒数第K个结点的方法来找入口位置<br>

