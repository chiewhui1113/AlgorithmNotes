# 栈的高频算法题
## 有效的括号（LeetCode 20）
```Python
def isValid(s):
  if len(s) <= 1: 
      return False
  stk = []
  smap = {
      '(' : ')', 
      '[' : ']', 
      '{' : '}'
  }
  for ch in s: 
      if ch in smap: 
          stk.append(ch)
      else: 
          if stk: 
              cur = stk.pop()
              if ch != smap[cur]: 
                  return False
          else: 
              return False
  return True
```
## 最小栈（LeetCode 155）
```Python
class MinStack(object):

    def __init__(self):
        self.stk = []
        self.minStk = []
        self.minStk.append(float('inf'))

    def push(self, val):
        """
        :type val: int
        :rtype: None
        """
        self.stk.append(val)
        self.minStk.append(min(self.minStk[-1], val))
        

    def pop(self):
        """
        :rtype: None
        """
        self.stk.pop()
        self.minStk.pop()

    def top(self):
        """
        :rtype: int
        """
        return self.stk[-1]
        

    def getMin(self):
        """
        :rtype: int
        """
        return self.minStk[-1]
```
