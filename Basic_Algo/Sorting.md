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
	if (l >= r) return; // 数组长度不大于1，返回
	int mid = l + r >> 1; // 确定分界点
	mergeSort(q, l, mid); // 根据分界点把数组一分为二
	mergeSort(q, mid + 1, r);
	int temp[r - l + 1]; // 创建临时数组
	int k = 0, i = l, j = mid + 1; // i和j是双指针，k是临时数组的指针
	while (q[i] != null && q[j] != null) { // 归并，合二为一
		if (q[i] <= q[j]) { // 先记录小的值
			temp[k++] = q[i++];
		} else {
			temp[k++] = q[j++];
		}
	}
	while (q[i] != null) temp[k++] = q[i++]; // 假如还有剩下的值
	while (q[j] != null) temp[k++] = q[j++];
	for (int i = l, k = 0; i <= r; i++, k++) q[i] = temp[k]; // 更新原数组
}
```
