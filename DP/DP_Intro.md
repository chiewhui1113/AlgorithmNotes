# 动态规划
## 什么是动态规划
“记忆化搜素“ 用递归计算斐波那契数列的时候，经常有很多重复的调用。因此可以把他们记录在一个
arr，这样就可以直接取值。

## 模版
```C++
dp[0][0] = base case
for ...:
  for ...:
    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
return dp[m - 1][n - 1]
```

## 统计路径总数（LeetCode 62）
1. 二维数组

![image](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/f6b592d4-3946-475b-9cff-1260d62b9383)

```C++
int uniquePaths(int m, int n) {
  vector<vector<int>> dp(m, vector<int>(n, 1));
  for (int i = 1; i < m; i++) {
      for (int j = 1; j < n; j++) {
          dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
      }
  }
  return dp[m - 1][n - 1];
}
```
2. 一维数组
```C++
int uniquePaths(int m, int n) {
  vector<int> dp(n, 1);
  for (int i = 1; i < m; i++) {
      for (int j = 1; j < n; j++) {
          dp[j] += dp[j - 1];
      }
  }
  return dp[n - 1];
}
```

## 最小路径和（LeetCode 64）
```C++
int minPathSum(vector<vector<int>>& grid) {
  int m = grid.size();
  int n = grid[0].size();
  vector<vector<int>> dp(m, vector<int>(n, 0));
  
  dp[0][0] = grid[0][0];
  for (int i = 1; i < m; i++) {
      dp[i][0] = dp[i - 1][0] + grid[i][0];
  }
  for (int i = 1; i < n; i++) {
      dp[0][i] = dp[0][i - 1] + grid[0][i];
  }
  
  for (int i = 1; i < m; i++) {
      for (int j = 1; j < n; j++) {
          int top = dp[i - 1][j] + grid[i][j];
          int right =  dp[i][j - 1] + grid[i][j];
          dp[i][j] = min(top, right);
      }
  }

  return dp[m - 1][n - 1];
}
```

## 三角形最小路径和（LeetCode 120）
```C++
int minimumTotal(vector<vector<int>>& triangle) {
  int n = triangle.size();
  vector<vector<int>> dp(n, vector<int>(n, 0));
  dp[0][0] = triangle[0][0];
  for (int i = 1; i < n; i++) {
      dp[i][0] = dp[i - 1][0] + triangle[i][0];
  }

  for (int i = 1; i < n; i++) {
      for (int j = 1; j <= i; j++) {
          int left = j - 1 >= 0 ? dp[i - 1][j - 1] : INT_MAX;
          int right = j < i ? dp[i - 1][j] : INT_MAX;
          dp[i][j] = min(left, right) + triangle[i][j];
      }
  }

  int min_total = dp[n - 1][0];
  for (int i = 1; i < n; i++) {
      min_total = min(min_total, dp[n - 1][i]);
  }
  return min_total;
}
```

