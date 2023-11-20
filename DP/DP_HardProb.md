# DP题

## 最长回文串（LeetCode 5）
```C++
string longestPalindrome(string s) {
  int n = s.size();
  if (n < 2) return s;
  vector<vector<int>> dp(n, vector<int>(n, false));
  int start = 0, maxLen = 1;
  for (int i = 0; i < n; i++) {
      dp[i][i] = true;
  }

  for (int len = 2; len <= n; len++) {
      for (int i = 0; i <= n - len; i++) {
          int j = i + len - 1; 
          if (s[i] == s[j]) {
              if (len == 2 || dp[i + 1][j - 1]) {
                  dp[i][j] = true;
                  if (len > maxLen) {
                      start = i;
                      maxLen = len;
                  }
              }
          }
      }
  }

  return s.substr(start, maxLen);
}
```

