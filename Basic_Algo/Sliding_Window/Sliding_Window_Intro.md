# 滑动窗口

## 滑动窗口的基本思想
滑动窗口就是快慢指针的特例。在流量控制、熔断、限流超时等场景都会用滑动窗口来思考问题。
hystrix、sentinel等框架都用了这种思想。假如有一个大小为3的窗口，当有新的数据来并且
超过3的时候就把新的放入老的移走。<br><br>
<img width="644" alt="image" src="https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/8253dc4d-4c63-4989-a083-ff6ecfbcf25d">
<br><br>
滑动窗口一般会有两种类型的题：
1. 固定窗口：哪个窗口元素最大、最小、平均值
2. 不固定窗口：求一个序列里最大、最小窗口是什么

## 子数组最大平均数（LeetCode 643）
```C++
double findMaxAverage(vector<int>& nums, int k) {
  double sum = 0;
  for (int i = 0; i < k; i++) {
      sum += nums[i];
  }
  double maxSum = sum;
  for (int i = k; i < nums.size(); i++) {
      sum = sum - nums[i - k] + nums[i];
      maxSum = max(maxSum, sum);
  }
  return maxSum / k;
}
```

## 最长连续递增序列（LeetCode 674）
```C++
int findLengthOfLCIS(vector<int>& nums) {
  int left = 0, right = 0;
  int longest = 0;
  for (int i = 0; i < nums.size(); i++) {
      if (right > 0 && nums[i - 1] >= nums[i]) {
          left = right;
      }
      right++;
      longest = max(longest, right - left);
  }
  return longest;
}
```
```C++
int findLengthOfLCIS(vector<int>& nums) {
  int res = 1;
  int curLen = 1;
  for (int i = 1; i < nums.size(); i++) {
      if (nums[i] <= nums[i - 1]) {
          curLen = 1;
      } else {
          curLen++;
      }
      res = max(res, curLen);
  }
  return res;
}
```
