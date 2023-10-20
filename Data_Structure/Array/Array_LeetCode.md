# 数组高频算法题
在数组的算法题里，双指针的思想特别重要且非常有用。以下的问题都是基于双指针的思路做的。
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
def removeDuplicates(self, nums):
  i = 0
  for num in nums: 
      if i == 0 or i == 1 or nums[i - 2] != num: 
          nums[i] = num
          i += 1
  return i
```

## 按奇偶排序数组（LeetCode 805）
```Python
def sortArrayByParity(self, nums):
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
def rotate(self, nums, k):
  length = len(nums)
  k %= length
  nums[:] = nums[::-1]
  nums[k:] = nums[k:][::-1]
  nums[:k] = nums[:k][::-1]
```

## 数组的区间（LeetCode 228）
```Python
def summaryRanges(self, nums):
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

