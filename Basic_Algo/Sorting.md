## 快速排序（Quick Sort）
快排是基于分治的一个排序算法：
1. 确定分界点：q[l], **q[(l + r) / 2]**, q[r]（任选其一，取中间值最佳）
2. 调整区间：让左边区间的所有值都小于等于分界点，右边区间的所有值都大于等于分界点
3. 递归处理左右两段

代码
```C++
void quickSort(int q[], int l, int r) {
  if (l >= r) return; // 数组长度不大于1，返回
  int mid = q[l + r >> 1], i = l - 1, j = r + 1; // 取分界点
  while (i < j) { // 调整区间
    do i++; while (q[i] < mid); 
    do j--; while (q[j] > mid);  
    if (i < j) swap(q[i], q[j]);
  }
  quickSort(q, l, j); // 递归处理左边段
  quickSort(q, j + 1, r); // 递归处理右边段
}
```
## 数组第k大（LeetCode 215）
在快速排序时，pivot每一轮排序结束都会在正确的位置上。假设当前pivot排序后索引为1，代表当前pivot第二小。
```C++
int quickSort(vector<int>& nums, int start, int end, int k) {
  if (start == end) return nums[k];
  int pivot = nums[start + (end - start) / 2], l = start - 1, r = end + 1;
  while (l < r) {
      do l++; while (nums[l] < pivot);
      do r--; while (nums[r] > pivot);
      if (l < r) swap(nums[l], nums[r]);
  }
  if (k <= r) return quickSort(nums, start, r, k); // r是pivot的前一个元素
  else return quickSort(nums, r + 1, end, k);
}

int findKthLargest(vector<int>& nums, int k) {  
  return quickSort(nums, 0, nums.size() - 1, nums.size() - k);
```


## 归并排序（Merge Sort）
归排是基于分治的一个排序算法：
1. 确定分界点：mid = (l + r) / 2
2. 根据分界点把数组一分为二
3. 归并，利用双指针算法合二为一
	第一个指针指向L
	第二个指针指向mid + 1

代码
```C++
void mergeSort(int q[], int l, int r) {
    if (l >= r) return;
    int mid = l + (r - l) / 2;
    mergeSort(q, l, mid);
    mergeSort(q, mid + 1, r);
    int temp[r - l + 1];
    int k = 0, i = l, j = mid + 1;
    while (i <= mid && j <= r) {
        if (q[i] <= q[j]) temp[k++] = q[i++];
        else temp[k++] = q[j++];
    }
    while (i <= mid) temp[k++] = q[i++];
    while (j <= r) temp[k++] = q[j++];
    for (int i = l, k = 0; i <= r; i++, k++) q[i] = temp[k];
}
```
