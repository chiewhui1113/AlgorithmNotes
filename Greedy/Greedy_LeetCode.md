## 判断区间是否重叠（Leetcode 252）
```C++
bool canAttendMeetings(int[][] intervals) {
  sort(intervals, intervals + intervals.length, [](int v1, int v2) {
    return v1[0] < v2[0];
  });
  for (int i = 1; i < intervals.length; i++) {
    if (intervals[i][0] > intervals[i - 1][1]) return false;
  }
  return true;
}
```

## 区间合并（LeetCode 56）
```C++
vector<vector<int>> merge(vector<vector<int>>& intervals) {
  sort(intervals.begin(), intervals.end());
  int st = -2e9, ed = -2e9;
  vector<vector<int>> res;
  for (auto inter : intervals) {
      if (inter[0] > ed) {
          if (st != -2e9) res.push_back({st, ed});
          st = inter[0], ed = inter[1];
      } else {
          ed = max(ed, inter[1]);
      }
  }
  if (st != -2e9) res.push_back({st, ed});
  return res;
}
```

## 插入区间（LeetCode 57）
```C++
vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
  vector<vector<int>> res;
  int i = 0, n = intervals.size();
  while (i < n && intervals[i][1] < newInterval[0]) {
      res.push_back(intervals[i++]);
  }

  while (i < n && intervals[i][0] <= newInterval[1]) {
      newInterval[0] = min(newInterval[0], intervals[i][0]);
      newInterval[1] = max(newInterval[1], intervals[i][1]);
      i++;
  }
  res.push_back(newInterval);

  while (i < n) {
      res.push_back(intervals[i++]);
  }

  return res;
}
```

## 字符串分割（LeetCode 763）
```C++
vector<int> partitionLabels(string s) {
  int last[26];
  int length = s.size();
  for (int i = 0; i < length; i++) {
      last[s[i] - 'a'] = i;
  }
  int start = 0, end = 0;
  vector<int> partition;
  for (int i = 0; i < length; i++) {
      end = max(end, last[s[i] - 'a']);
      if (end == i) {
          partition.push_back(end - start + 1);
          start = end + 1;
      }
  }
  return partition;
}
```

## 加油站问题（LeetCode 134）
```C++
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
  int curSum = 0;
  int totalSum = 0;
  int start = 0;
  for (int i = 0; i < gas.size(); i++) {
      curSum += gas[i] - cost[i];
      totalSum += gas[i] - cost[i];
      if (curSum < 0) {
          start = i + 1;
          curSum = 0;
      }
  }
  if (totalSum < 0) return -1;
  return start;
}
```

## 跳跃游戏（LeetCode 55）
```C++
bool canJump(vector<int>& nums) {
  int n = nums.size();
  int rightmost = 0;
  for (int i = 0; i < n; i++) {
      if (i <= rightmost) {
          rightmost = max(rightmost, i + nums[i]);
          if (rightmost >= n - 1) {
              return true;
          }
      }
  }
  return false;
}
```

## 最短跳跃游戏（LeetCode 45）
```C++
int jump(vector<int>& nums) {
  int maxPos = 0, n = nums.size(), end = 0, steps = 0;
  for (int i = 0; i < n - 1; i++) {
      if (maxPos >= i) {
          maxPos = max(maxPos, nums[i] + i);
          if (i == end) {
              end = maxPos;
              steps++;
          }
      }
  }
  return steps;
}
```
