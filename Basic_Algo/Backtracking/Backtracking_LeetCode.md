# 回溯算法题

## 组合总和问题（LeetCode 39）
```C++
void dfs(vector<int>& c, int u, int target, vector<vector<int>>& res, vector<int>& path) {
  if (target < 0) return;
  if (target == 0) {
      res.push_back(path);
      return;
  }
  for (int i = u; i < c.size(); i++) {
      if (c[i] <= target) {
          path.push_back(c[i]);
          dfs(c, i, target - c[i], res, path);
          path.pop_back();
      }
  }
}

vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
  vector<vector<int>> res;
  vector<int> path;
  dfs(candidates, 0, target, res, path);
  return res;
}
```

## 分割回文串（LeetCode 131）
```C++
bool isPalindrome(string s, int start, int end) {
  for (int i = start, j = end; i < j; i++, j--) {
      if (s[i] != s[j]) return false;
  }
  return true;
}

void backtracking(string s, int start, vector<vector<string>>& res, stack<string>& stk) {
  // 到尾了，加进res
  if (start >= s.length()) {
      vector<string> path;
      stack<string> tempStk = stk;
      while (!tempStk.empty()) {
          path.insert(path.begin(), tempStk.top());
          tempStk.pop(); 
      }
      res.push_back(path);
      return;
  }
  for (int i = start; i < s.length(); i++) {
      if (isPalindrome(s, start, i)) {
          string str = s.substr(start, i - start + 1);
          stk.push(str);
          backtracking(s, i + 1, res, stk);
          stk.pop(); // 回溯
      }
  }
}

vector<vector<string>> partition(string s) {
  vector<vector<string>> res;
  stack<string> stk;
  backtracking(s, 0, res, stk);
  return res;
}
```

## 子集问题（LeetCode 78）
```C++
vector<vector<int>> res;
vector<int> path;

void backtracking(vector<int>& nums, int start) {
  res.push_back(path);
  if (start >= nums.size()) return;
  for (int i = start; i < nums.size(); i++) {
      path.push_back(nums[i]);
      backtracking(nums, i + 1);
      path.pop_back();
  }
}

vector<vector<int>> subsets(vector<int>& nums) {
  res.clear();
  path.clear();
  backtracking(nums, 0);
  return res;
}
```

## 排列问题（LeetCode 46）
```C++
vector<vector<int>> res;
vector<int> path;

void backtracking(vector<int>& nums, vector<bool>& used) {
  if (nums.size() == path.size()) {
      res.push_back(path);
      return;
  }
  for (int i = 0; i < nums.size(); i++) {
      if (used[i]) continue;
      used[i] = true;
      path.push_back(nums[i]);
      backtracking(nums, used);
      path.pop_back();
      used[i] = false;
  }
}

vector<vector<int>> permute(vector<int>& nums) {
  res.clear();
  path.clear();
  vector<bool> used(nums.size(), false);
  backtracking(nums, used);
  return res;
}
```

## 字母大小写排序（LeetCode 784）
```C++
void backtracking(string s, int pos, vector<string>& res) {
  while (pos < s.length() && isdigit(s[pos])) pos++;
  if (pos == s.size()) {
      res.push_back(s);
      return;
  }
  s[pos] ^= 32;
  backtracking(s, pos + 1, res);
  s[pos] ^= 32;
  backtracking(s, pos + 1, res);
}

vector<string> letterCasePermutation(string s) {
  vector<string> res;
  backtracking(s, 0, res);
  return res;
}
```

## 单词搜索（LeetCode 79）
```C++
class Solution {
public:
  bool exist(vector<vector<char>>& board, string word) {
      rows = board.size();
      cols = board[0].size();
      for (int i = 0; i < rows; i++) {
          for (int j = 0; j < cols; j++) {
              if (dfs(board, word, i, j, 0)) return true;
          }
      }
      return false;
  }

private: 
  int rows, cols;
  bool dfs(vector<vector<char>>& board, string word, int i, int j, int k) {
      if (i >= rows || i < 0 || j >= cols || j < 0 || board[i][j] != word[k]) return false;
      if (k == word.size() - 1) return true;
      board[i][j] = '\0';
      bool res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) ||
                 dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i, j - 1, k + 1);
      board[i][j] = word[k];
      return res;
  }

};
```
