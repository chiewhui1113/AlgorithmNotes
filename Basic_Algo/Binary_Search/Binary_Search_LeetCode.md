# 二分高频算法题
## 山脉数组的顶峰（LeetCode 852）
### 最简单的方法
```C++
int peakIndexInMountainArray(vector<int>& arr) {
  for (int i = 0; i < arr.size() - 1; i++) {
      if (arr[i] > arr[i + 1]) {
          return i;
      }
  }
  return -1;
}
```
### 二分
1. mid在上升阶段满足arr[mid - 1] < arr[mid] < arr[mid + 1]
2. mid在顶峰阶段满足arr[mid] > arr[mid - 1] && arr[mid] > arr[mid + 1]
3. mid在下降阶段满足arr[mid - 1] > arr[mid] > arr[mid + 1]
```C++
int peakIndexInMountainArray(vector<int>& arr) {
  int left = 1, right = arr.size() - 2, ans = 0;
  while (left <= right) {
      int mid = left + (right - left) / 2;
      if (arr[mid] > arr[mid + 1]) {
          ans = mid;
          right = mid - 1;
      } else {
          left = mid + 1;
      }
  }
  return ans;
}
```

## 旋转数字的最小数字（LeetCode 153）
最小值x的左侧肯定都严格大于x，右侧都肯定严格小于x。在二分查找的每一步中，左边界为low，右边界为high，区间的中点为pivot，
最小值就在这区间内。把nums[pivot]和nums[high]比较时，会出现两种情况：
1. nums[pivot] > nums[high]：说明可以忽略左半部分
2. nums[pivot] < nums[high]：说明可以忽略右半部分
```C++
int findMin(vector<int>& nums) {
  int low = 0, high = nums.size() - 1;
  while (low < high) {
      int pivot = low + (high - low) / 2;
      if (nums[pivot] < nums[high]) {
          high = pivot; // 由于边界情况不使用pivot - 1
      } else {
          low = pivot + 1;
      }
  }
  return nums[low];
}
```

## 找缺失数字
```C++
int findMissingNum(vector<int>& nums) {
  int low = 0, high = nums.size() - 1;
  while (low < high) {
    int mid = low + (high - low) / 2;
    if (nums[mid] == mid) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return low;
}
```

## 平方根（LeetCode 69）
```C++
int mySqrt(int x) {
  int left = 0, right = x, ans = 0;
  while (left <= right) {
      int mid = left + (right - left) / 2;
      if ((long) mid * mid <= x) {
          ans = mid;
          left = mid + 1;
      } else {
          right = mid - 1;
      }
  }
  return ans;
}
```

## 二叉搜索树中搜索特定值（LeetCode 700）
二叉搜索树的左子树孩子的值都小于当前节点，右子树孩子的值都大于当前节点
1. root的值等于val，返回root
2. root的值大于val，递归查root.left
3. root的值小于val，递归查root.right
### 递归方式
```C++
TreeNode* searchBST(TreeNode* root, int val) {
  if (!root) return root;
  if (root->val == val) return root;
  return searchBST(val < root->val ? root->left : root->right, val);
}
```
### 迭代方式
```C++
TreeNode* searchBST(TreeNode* root, int val) {
  while (root) {
      if (root->val == val) return root;
      root = root->val < val ? root->right : root->left;
  }
  return root;
}
```

## 验证二叉搜索树（LeetCode 98）
```C++
bool isValidBST(TreeNode* root) {
  return helper(root, LONG_MIN, LONG_MAX);
}

bool helper(TreeNode* root, long long low, long long high) {
  if (!root) return true;
  if (root->val <= low || root->val >= high) return false;
  return helper(root->left, low, root->val) && helper(root->right, root->val, high);
}
```

## 有序数组转二叉搜素树（LeetCode 108）
```C++
TreeNode* sortedArrayToBST(vector<int>& nums) {
  return helper(nums, 0, nums.size() - 1);
}

TreeNode* helper(vector<int>& nums, int left, int right) {
  if (left > right) return nullptr;
  int mid = left + (right - left) / 2;
  TreeNode* node = new TreeNode(nums[mid]);
  node->left = helper(nums, left, mid - 1);
  node->right = helper(nums, mid + 1, right);
  return node;
}
```

## 寻找两个正序数组中的中位数（LeetCode 4）
边界情况：
1. 两个数组的长度各位1，返回两个数组中更小的值即可
2. 如果LA[k/2-1] / LB[k/2-1]越界，选对应数组中的最后一个元素，根据排除个树减少k的值

正常情况：
1. LA[k/2-1] < LB[k/2-1]：比LA[k/2-1]小的最多只有LA的前k/2-1和LB的前k/2-1，加起来是k-2. 因此LA[0]到LA[k/2-1]都不可能是第k个树
2. LA[k/2-1] > LB[k/2-1]：排除LB[0]到LB[k/2-1]
3. LA[k/2-1] = LB[k/2-1]：用第一种情况处理
```C++
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
  int totalLen = nums1.size() + nums2.size();
  if (totalLen % 2 == 1) {
      return getKthElem(nums1, nums2, (totalLen + 1) / 2.0);
  } else {
      return (getKthElem(nums1, nums2, totalLen / 2) + getKthElem(nums1, nums2, totalLen / 2 + 1)) / 2.0;
  }
}

int getKthElem(const vector<int>& nums1, const vector<int>& nums2, int k) {
  int m = nums1.size();
  int n = nums2.size();
  int index1 = 0, index2 = 0;
  while (true) {
      if (index1 == m) {
          return nums2[index2 + k - 1];
      } else if (index2 == n) {
          return nums1[index1 + k - 1];
      } else if (k == 1) {
          return min(nums1[index1], nums2[index2]);
      }

      int newIndex1 = min(index1 + k / 2 - 1, m - 1);
      int newIndex2 = min(index2 + k / 2 - 1, n - 1);
      int pivot1 = nums1[newIndex1];
      int pivot2 = nums2[newIndex2];
      if (pivot1 <= pivot2) {
          k -= newIndex1 - index1 + 1;
          index1 = newIndex1 + 1;
      } else {
          k -= newIndex2 - index2 + 1;
          index2 = newIndex2 + 1;
      }
  }
}
```

