# 栈
栈是很多表达式与符号的运算基础，也是递归的底层实现。基本操作有push(e), pop(), peek(), empty()
## 基于数组实现栈
class Stack(object): 
  def __init__(self): 
    self.items = []

  def is_empty(self): 
    return self.items == []

  def push(self, elem): 
    self.items.append(elem)

  def pop(self): 
    self.items.pop()

  def peek(self): 
    return self.items[-1]

  def size(self): 
    return len(self.items)
