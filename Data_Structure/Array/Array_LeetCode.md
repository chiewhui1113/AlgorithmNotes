# 数组高频算法题
在数组的算法题里，双指针的思想特别重要且非常有用。以下的问题大多数基于双指针的思路做的。
## 移除所有数值等于val的元素（LeetCode 27）
1. 快慢指针<br>
slow之前的位置为有效部分，fast表示当前访问的元素。只要fast的值不会val，则把当前元素添加到arr[slow++]
```Python
def removeElement(nums, val):
  slow = fast = 0
  while fast < len(nums): 
      if nums[fast] != val: 
          nums[slow] = nums[fast]
          slow += 1
      fast += 1
  return slow
```
2. 对撞型双指针<br>
left指针从左边走起找到第一个等于val的元素，right指针从右边走起找到第一个不是val的元素，然后交换slow和fast
```Python
def removeElement(nums, val):
  left = 0
  right = len(nums) - 1
  while left <= right: 
      if nums[left] == val and nums[right] != val: 
          temp = nums[left]
          nums[left] = nums[right]
          nums[right] = temp 
      if nums[left] != val: 
          left += 1
      if nums[right] == val: 
          right -= 1
  return left
```
3. 对撞 + 覆盖<br>
```Python
def removeElement(nums, val):
  left = 0
  right = len(nums) - 1
  while left <= right: 
      if nums[left] == val: 
          nums[left] = nums[right]
          right -= 1
      else: 
          left += 1
  return left
```
## 删除有序数组中的重复项（LeetCode 26）
```Python
def removeDuplicates(nums):
  j = 1
  for i in range(1, len(nums)): 
      if nums[i] != nums[j - 1]: 
          nums[j] = nums[i]
  return j
```

## 删除有序数组中的重复项II（LeetCode 80）
```Python
def removeDuplicates(nums):
  i = 0
  for num in nums: 
      if i == 0 or i == 1 or nums[i - 2] != num: 
          nums[i] = num
          i += 1
  return i
```

## 按奇偶排序数组（LeetCode 805）
```Python
def sortArrayByParity(nums):
  left = 0
  right = len(nums) - 1
  while left < right: 
      if nums[left] % 2 == 1 and nums[right] % 2 == 0: 
          temp = nums[left]
          nums[left] = nums[right]
          nums[right] = temp
      if nums[left] % 2 == 0: 
          left += 1
      if nums[right] % 2 == 1: 
          right -= 1
  return nums
```

## 将数组的元素向右轮转k个位置（LeetCode 189）
```Python
def rotate(nums, k):
  length = len(nums)
  k %= length
  nums[:] = nums[::-1]
  nums[k:] = nums[k:][::-1]
  nums[:k] = nums[:k][::-1]
```

## 数组的区间（LeetCode 228）
```Python
def summaryRanges(nums):
  slow = fast = 0
  res = []
  n = len(nums)
  while fast < n:
      if fast < n - 1 and nums[fast] + 1 == nums[fast + 1]: 
          fast += 1
      else: 
          res.append([nums[slow], nums[fast]])
          slow = fast = fast + 1
  print(res)
  def p(x): 
      slow, fast = x
      if slow == fast: 
          return str(slow)
      else: 
          return str(slow) + "->" + str(fast)
  return list(map(p, res))
```

## 数组中只出现一次的数字（LeetCode 136）
1. 集合
```Python
def singleNumber(nums):
  num_set = set()
  for num in nums: 
      if num in num_set: 
          num_set.remove(num)
      else: 
          num_set.add(num)
  if num_set: 
      return list(num_set)[0]
  return None
```
2. 异或
```Python
def singleNumber(nums):
  flag = 0
  for num in nums: 
      flag ^= num
  return flag
```

## 荷兰国旗问题（LeetCode 75）
1. 快慢指针
```Python
def sortColors(nums):
  left = 0
  n = len(nums)
  for right in range(n): 
      if nums[right] == 0: 
          nums[left], nums[right] = nums[right], nums[left]
          left += 1
  for right in range(left, n): 
      if nums[right] == 1: 
          nums[left], nums[right] = nums[right], nums[left]
          left += 1
```
2. 三指针
```Python
def sortColors(self, nums):
  left = index = 0
  right = len(nums) - 1
  while index <= right: 
      if nums[index] == 0: 
          nums[index], nums[left] = nums[left], nums[index]
          left += 1
          index += 1
      elif nums[index] == 2: 
          nums[index], nums[right] = nums[right], nums[index]
          right -= 1
      else: 
          index += 1
```
