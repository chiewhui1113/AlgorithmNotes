# 动态规划算法题

## 最少硬币数（LeetCode 322）
```C++
int coinChange(vector<int>& coins, int amount) {
  int max = amount + 1;
  vector<int> dp(max, max);
  dp[0] = 0;
  for (int i = 1; i <= amount; i++) {
      for (int coin : coins) {
          if (coin <= i) {
              dp[i] = min(dp[i], dp[i - coin] + 1);
          }
      }
  }
  return dp[amount] > amount ? -1 : dp[amount];
}
```

## 最长连续递增子序列（LeetCode 674）
```C++
int findLengthOfLCIS(vector<int>& nums) {
  if (nums.size() == 0) return 0;
  vector<int> dp(nums.size(), 1);
  int res = 1;
  for (int i = 1; i < nums.size(); i++) {
      if (nums[i] > nums[i - 1]) {
          dp[i] = dp[i - 1] + 1;
      }
      res = max(res, dp[i]);
  }
  return res;
}
```

## 最长递增子序列（LeetCode 300）
```C++
int lengthOfLIS(vector<int>& nums) {
  if (nums.size() == 0) return 0;
  vector<int> dp(nums.size(), 1);
  int res = 1;
  for (int i = 0; i < nums.size(); i++) {
      for (int j = i + 1; j < nums.size(); j++) {
          if (nums[j] > nums[i]) {
              dp[j] = max(dp[j], dp[i] + 1);
          }
      }
      res = max(res, dp[i]);
  }
  return res;
}
```

## 最少完全平方数（LeetCode 279）
```C++
int numSquares(int n) {
  vector<int> dp(n + 1, 10000);
  dp[0] = 0;
  for (int i = 1; i <= n; i++) {
      for (int j = 1; j * j <= i; j++) {
          dp[i] = min(dp[i], dp[i - j * j] + 1);
      }
  }
  return dp[n];
}
```

## 跳跃游戏（LeetCode 55）
```C++
bool canJump(vector<int>& nums) {
  // LeetCode上会超时
  vector<int> dp(nums.size(), false);
  dp[0] = true;
  for (int i = 1; i < nums.size(); i++) {
      for (int j = 0; j < i; j++) {
          if (dp[j] && nums[j] + j >= i) {
              dp[i] = true;
              break;
          }
      }
  }
  return dp[nums.size() - 1];
}
```

## 解码方法（LeetCode 91）
```C++
int numDecodings(string s) {
  int n = s.length();
  vector<int> f(n + 1, 0);
  f[0] = 1;
  for (int i = 1; i <= n; i++) {
      if (s[i - 1] != '0') {
          f[i] += f[i - 1];
      }
      if (i > 1 && check(s, i)) {
          f[i] += f[i - 2];
      }
  }
  return f[n];
}

bool check(string s, int i) {
  if (s[i - 2] == '0') return false;
  int num = (s[i - 2] - '0') * 10 + (s[i - 1] - '0');
  if (num > 26) return false;
  return true;
}
```

## 路径中存在障碍物（LeetCode 62）
```C++
int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
  int n = obstacleGrid.size();
  int m = obstacleGrid[0].size();
  vector<int> dp(m);
  dp[0] = obstacleGrid[0][0] == 0 ? 1 : 0;
  for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
          if (obstacleGrid[i][j] == 1) {
              dp[j] = 0;
              continue;
          }
          if (j - 1 >= 0 && obstacleGrid[i][j - 1] == 0) {
              dp[j] += dp[j - 1];
          }
      }
  }
  return dp[m - 1];
}
```

## 杨辉三角（LeetcCode 119）
```C++
vector<int> getRow(int rowIndex) {
  vector<int> res;
  for (int i = 0; i <= rowIndex; i++) {
      vector<int> cur;
      for (int j = 0; j <= i; j++) {
          if (j == 0 || j == i) {
              cur.push_back(1);
          } else {
              cur.push_back(res[j - 1] + res[j]);
          }
      }
      res = cur;
  }
  return res;
}
```

```C++
vector<int> getRow(int rowIndex) {
  vector<int> res;
  res.push_back(1);
  for (int i = 1; i <= rowIndex; i++) {
      res.push_back(0);
      for (int j = i; j > 0; j--) {
          res[j] += res[j - 1];
      }
  }
  return res;
}
```
