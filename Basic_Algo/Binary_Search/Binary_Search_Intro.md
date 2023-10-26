# 二分查找
分治法是计算机中最重要的算法之一，就是把一个复杂的问题分成两个或更多的子问题，再把子问题分成更小的子问题，到能简单求解且合并。
二分查找每次都会减半，所有时间复杂度是O（logn）
## 循环的方式
```C++
int search(vector<int>& nums, int target) {
  int low = 0, high = nums.size() - 1;
  while (low <= high) {
      // low和high太高的话，low + high会溢出
      int mid = low + ((high - low) >> 1); 
      if (nums[mid] == target) return mid;
      else if (nums[mid] > target) high = mid - 1;
      else low = mid + 1;
  }
  return -1;
}
```
## 递归的方式
```C++
int binarySearch(vector<int>& nums, int low, int high, int target) {
  if (low <= high) {
      int mid = low + ((high - low) >> 1);
      if (nums[mid] == target) return mid;
      else if (nums[mid] > target) return binarySearch(nums, low, mid - 1, target);
      else return binarySearch(nums, mid + 1, high, target);
  }
  return -1;
}

int search(vector<int>& nums, int target) {
  return binarySearch(nums, 0, nums.size() - 1, target);
}
```
## 找到左侧第一个元素
```C++
int binarySearch(vector<int>& nums, int target) {
  if (nums == NULL || nums.size() == 0) return -1;
  int left = 0;
  int right = nums.size() - 1;
  while (left <= right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] > target) right = mid - 1;
    else if (nums[mid] < target) left = mid + 1;
    else {
      while (mid != 0 && nums[mid] == target) {
        mid--; // 找左侧第一个
      }
      if (mid == 0 && nums[mid] == target) {
        return mid; // 假如0为第一个元素
      }
      return mid + 1; // 下一个元素才等于target，所以返回mid + 1
    }
  }
  return -1;
}
```
