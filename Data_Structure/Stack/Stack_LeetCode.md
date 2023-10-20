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
## 计算机问题（LeetCode 227）
```C++
int calculate(string s) {
  stack<int> stk;
  int num = 0;
  char sign = '+';
  for (int i = 0; i < s.length(); i++) {
      char c = s[i];
      if (isdigit(c)) {
          num = num * 10 + (c - '0');
      } 
      if (!isdigit(c) && c != ' ' || i == s.length() - 1) {
          if (sign == '+') {
              stk.push(num);
          } else if (sign == '-') {
              stk.push(-num);
          } else if (sign == '*') {
              int preNum = stk.top();
              stk.pop();
              stk.push(preNum * num);
          } else if (sign == '/') {
              int preNum = stk.top();
              stk.pop();
              stk.push(preNum / num);
          }
          sign = c;
          num = 0;
      }
  }
  int res = 0;
  while(!stk.empty()) {
      res += stk.top();
      stk.pop();
  }
  return res;
}
```
## 逆波兰表达式（LeetCode 150）
```Python
def evalRPN(tokens):
        stack = []

        for token in tokens :
            if token == '+' :
                a , b = stack.pop() , stack.pop()
                stack.append( a + b ) 
            elif token == '-':
                a , b = stack.pop() , stack.pop()
                stack.append( b - a ) 
            elif token == '*':
                a , b = stack.pop() , stack.pop()
                stack.append( b * a ) 
            elif token == '/':
                a , b = stack.pop() , stack.pop()
                stack.append( int(b / a) ) 
            else:
                stack.append(int(token)) 
        return stack.pop()                   
```
