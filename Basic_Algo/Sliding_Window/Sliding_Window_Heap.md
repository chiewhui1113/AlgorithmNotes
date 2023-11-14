# 滑动窗口和堆的结合
由于最大堆的顶端一定是最大值，只要检查在不在滑动窗口的范围。在的话，就是目前的最大值

## 滑动窗口最大值（LeetCode 239）
```C++
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
  int n = nums.size();
  priority_queue<pair<int, int>> q;
  for (int i = 0; i < k; i++) {
      q.emplace(nums[i], i);
  }
  vector<int> ans = {q.top().first};
  for (int i = k; i < nums.size(); i++) {
      q.emplace(nums[i], i);
      while (q.top().second <= i - k) {
          q.pop();
      }
      ans.push_back(q.top().first);
  }
  return ans;
}
```
