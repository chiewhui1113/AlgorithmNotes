# Hash散列表
## 基础概念
假设要在长度7的Hash表中存1-15的数字，存储公式是index=num%7 
<br><br>
<img width="500" alt="image" src="https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/9bbfd82a-64de-459e-bd27-375a67e8b67b">
<br><br>
<img width="507" alt="image (1)" src="https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/5ea7a84a-96be-43cc-8661-116899a98ff2">
<br><br>
假如要测试一个数字在不在数组里，只要取余数并且访问就可以。举例来说，要查看13在不在数组里，13 % 7 = 6。只要访问arr[6]的位置查看存不存在13即可。

## 碰撞处理方法
由于Hash中的每个位置可能存储多个元素，单纯的数组无法存储，常见的解决方法有：<br>
1. 开放定址法<br>
一旦发生了冲突，就去寻找下一个空的散列地址。相关信息可以深究Java的ThreadLocal
<br><br>
<img width="523" alt="image" src="https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/df89146c-c707-4f67-b15d-3f5bf96a6bbf">
<br><br>
3. 链地址法<br>
哈希表中的每个单元为链表的头节点。假如发生了冲突，就把新元素添加到链表尾部。Hash的数组长度必须是2的n次幂，且size小于数组的75%
<br><br>

# 队列
## 基本概念和实现
队列采用了FIFO（First In First Out），可以用数组和链表实现
```Python
class Queue(object):
  def __init__(self):
    self.items = []

  def isEmpty(self):
    return self.items == []

  def enqueue(self, item):
    self.items.insert(0, item)

  def dequeue(self):
    self.items.pop()

  def size(self):
    return len(self.items)
```
