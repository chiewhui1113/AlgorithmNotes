# LRU的设计和实现
## LRU是什么？
LRU（Least Recently Used）是缓存实现的一个方式，当内存满的时候它会淘汰最长时间没被使用的页面。
LeetCode 146会让我们实现LRU，由于数组非常容易超时，Hash+双链表是公认最好的方式。
## Hash+双链表实现LRU
**Get**：key不存在返回-1；存在就用Hash定位该节点在双链表的位置并移动到双链表的头节点，返回该节点的值<br>
**Put**：key存在的操作和get一样；不存在就创建新节点插入头部，满的话就删除尾部节点
```Python
class ListNode: 
  def __init__(self, key=0, val=0): 
      self.key = key 
      self.val = val
      self.next = None
      self.prev = None

class LRUCache(object):
  def __init__(self, capacity):
      """
      :type capacity: int
      """
      self.cache = dict()
      self.head = ListNode()
      self.tail = ListNode()
      self.head.next = self.tail
      self.tail.prev = self.head 
      self.capacity = capacity 
      self.size = 0
      

  def get(self, key):
      """
      :type key: int
      :rtype: int
      """
      if key not in self.cache: 
          return -1
      node = self.cache[key]
      self.moveToHead(node)
      return node.val
      

  def put(self, key, value):
      """
      :type key: int
      :type value: int
      :rtype: None
      """
      if key not in self.cache: 
          node = ListNode(key, value)
          self.cache[key] = node
          self.addToHead(node)
          self.size += 1
          if self.size > self.capacity: 
              removed = self.removeTail()
              self.cache.pop(removed.key)
              self.size -= 1
      else: 
          node = self.cache[key]
          node.val = value 
          self.moveToHead(node)

  def addToHead(self, node): 
      node.prev = self.head
      node.next = self.head.next 
      self.head.next.prev = node 
      self.head.next = node 
  
  def removeNode(self, node): 
      node.prev.next = node.next
      node.next.prev = node.prev

  def moveToHead(self, node): 
      self.removeNode(node)
      self.addToHead(node)

  def removeTail(self): 
      node = self.tail.prev 
      self.removeNode(node)
      return node
```
