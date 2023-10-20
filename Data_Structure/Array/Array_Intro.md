# 数组
## 数组的扩容
1. 线性增长，每次增加固定数目的存储位置。节省空间但是操作次数多
2. 每次增加一倍的存储空间。浪费空间但是操作次数少

## 数组的初始化
```Python
list = [0 for i in range(10)]
list = [1, 2, 3, 4, 5]
```

## 查找元素
```Python
def findElement(arr, size, key):
  for i in range(size):
    if arr[i] == key:
      return i
  return -1
```

## 增加元素
```Python
def addElement(arr, size, element):
  index = size
  for i in range(size):
    if arr[i] >= element:
      index = i
      break
  for i in range(size, index, -1):
    arr[i] = arr[i - 1]
  arr[index] = element
```

## 删除元素
```Python
def delElement(arr, size, element):
  index = -1
  for i in range(size):
    if arr[i] == element:
      index = i
      break
    if index != -1:
      for j in range(index + 1, size):
        arr[i - 1] = arr[i]
      size -= 1
```

## 数组算法热身体
判断数组是否为单调数组（LeetCode 896）
```Python
def isMonotonic(self, nums):
  increasing = True
  decreasing = True
  for i in range(len(nums) - 1): 
      if nums[i] < nums[i + 1]: 
          decreasing = False
      if nums[i] > nums[i + 1]: 
          increasing = False
  return increasing or decreasing
```
寻找插入位置（LeetCode 35）
```Python
def searchInsert(nums, target):
  left = 0 
  right = len(nums) - 1
  ans = len(nums)
  while left <= right: 
      mid = (right - left) // 2 + left
      if nums[mid] >= target: 
          ans = mid 
          right = mid - 1
      else: 
          left = mid + 1
  return ans
```
合并两个有序数组（LeetCode 88）
```Python
def merge(nums1, m, nums2, n):
  i = m - 1
  j = n - 1
  cur = len(nums1) - 1
  while j >= 0: 
      if i >= 0 and nums2[j] < nums1[i]: 
          nums1[cur] = nums1[i]
          i -= 1
      else: 
          nums1[cur] = nums2[j]
          j -= 1
      cur -= 1
  return nums1
```
