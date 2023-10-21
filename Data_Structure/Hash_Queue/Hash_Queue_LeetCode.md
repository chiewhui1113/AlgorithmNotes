# Hash和队列的高频算法题
## 用栈实现队列（LeetCode 232）
```Python
class MyQueue(object):
  def __init__(self):
      self.stkIn = []
      self.stkOut = []

  def push(self, x):
      self.stkIn.append(x)
      
  def pop(self):
      if self.empty(): 
          None 
      if self.stkOut: 
          return self.stkOut.pop()
      else: 
          for i in range(len(self.stkIn)): 
              self.stkOut.append(self.stkIn.pop())
          return self.stkOut.pop()

  def peek(self):
      ans = self.pop()
      self.stkOut.append(ans)
      return ans

  def empty(self):
      return not (self.stkIn or self.stkOut)
```
## 用队列实现栈（LeetCode 225）
```Python
class MyStack(object):
  def __init__(self):
      self.queue1 = collections.deque()
      self.queue2 = collections.deque()

  def push(self, x):
      """
      :type x: int
      :rtype: None
      """
      self.queue2.append(x)
      while self.queue1: 
          self.queue2.append(self.queue1.popleft())
      self.queue1, self.queue2 = self.queue2, self.queue1
      

  def pop(self):
      """
      :rtype: int
      """
      return self.queue1.popleft()

  def top(self):
      """
      :rtype: int
      """
      return self.queue1[0]

  def empty(self):
      """
      :rtype: bool
      """
      return not self.queue1
```
## 两数之和（LeetCode 1）
```Python
def twoSum(nums, target):
  hash_table = {}
  for i in range(len(nums)): 
      diff = target - nums[i]
      if diff in hash_table: 
          return [hash_table[diff], i]
      else: 
          hash_table[nums[i]] = i
  return None
```
## 三数之和（LeetCode 15）
```Python
def threeSum(nums):
  n = len(nums)
  ans = []
  nums.sort()
  for first in range(n): 
      if first > 0 and nums[first] == nums[first - 1]: 
          continue 
      third = n - 1
      target = -nums[first]
      for second in range(first + 1, n): 
          if second > first + 1 and nums[second] == nums[second - 1]: 
              continue
          elif second == third: 
              break 
          while second < third and nums[second] + nums[third] > target: 
              third -= 1
          if second < third and nums[second] + nums[third] == target: 
              ans.append([nums[first], nums[second], nums[third]])
  return ans
```
