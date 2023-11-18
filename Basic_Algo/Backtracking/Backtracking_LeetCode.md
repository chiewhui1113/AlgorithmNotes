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

## 括号生存问题（LeetCode 22）
```C++
void backtracking(vector<string>& res, string& s, int open, int close, int n) {
if (s.size() == n * 2) {
    res.push_back(s);
    return;
}
if (open < n) {
    s.push_back('(');
    backtracking(res, s, open + 1, close, n);
    s.pop_back();
}
if (close < open) {
    s.push_back(')');
    backtracking(res, s, open, close + 1, n);
    s.pop_back();
}
}

vector<string> generateParenthesis(int n) {
vector<string> res;
string s;
backtracking(res, s, 0, 0, n);
return res;
}
```

## 电话号码问题（LeetCode 17）
```C++
void backtracking(vector<string>& res, string& c, unordered_map<char, string>& phoneMap, int ind, string& digits) {
  if (ind == digits.length()) {
      res.push_back(c);
      return;
  } else {
      char digit = digits[ind];
      string letters = phoneMap.at(digit);
      for (char letter : letters) {
          c.push_back(letter);
          backtracking(res, c, phoneMap, ind + 1, digits);
          c.pop_back();
      }
  }
}

vector<string> letterCombinations(string digits) {
  vector<string> res;
  if (digits.empty()) return res;
  string c;
  unordered_map<char, string> phoneMap {
      {'2', "abc"}, 
      {'3', "def"}, 
      {'4', "ghi"}, 
      {'5', "jkl"}, 
      {'6', "mno"}, 
      {'7', "pqrs"}, 
      {'8', "tuv"}, 
      {'9', "wxyz"}
  };
  backtracking(res, c, phoneMap, 0, digits);
  return res;
} 
```

## 复原IP地址（LeetCode 93）
```C++
vector<string> res;

bool isValid(string& s, int start, int end) {
  if (start > end) return false;
  if (s[start] == '0' && start != end) return false;
  int num = 0;
  for (int i = start; i <= end; i++) {
      if (s[i] > '9' || s[i] < '0') return false;
      num = num * 10 + (s[i] - '0');
      if (num > 255) return false;
  }
  return true;
}

void backtracking(string& s, int start, int pointNum) {
  if (pointNum == 3) {
      if (isValid(s, start, s.size() - 1)) {
          res.push_back(s);
      }
      return;
  }
  for (int i = start; i < s.size(); i++) {
      if (isValid(s, start, i)) {
          s.insert(s.begin() + i + 1, '.');
          backtracking(s, i + 2, pointNum + 1);
          s.erase(s.begin() + i + 1);
      } else {
          break;
      }
  }
}

vector<string> restoreIpAddresses(string s) {
  res.clear();
  if (s.size() < 4 || s.size() > 12) return res;
  backtracking(s, 0, 0);
  return res;
}   
```
