# 字符串经典算法题
## 反转字符串（LeetCode 344）
```C++
void reverseString(vector<char>& s) {
  int left = 0;
  int right = s.size() - 1;
  while (left < right) {
      swap(s[left], s[right]);
      left++;
      right--;
  }
}
```

## K个一组反转（LeetCode 541）
```C++
string reverseStr(string s, int k) {
  for (int i = 0; i < s.size(); i += 2 * k) {
      if (i + k < s.size()) {
          reverse(s.begin() + i, s.begin() + i + k);
      } else {
          reverse(s.begin() + i, s.end());
      }
  }
  return s;
}
```

## 仅仅反转字母（LeetCode 917）
栈
```C++
string reverseOnlyLetters(string s) {
  stack<char> stk;
  for (char ch : s) {
      if (isalpha(ch)) {
          stk.push(ch);
      }
  }
  string ans = "";
  for (char ch : s) {
      if (isalpha(ch)) {
          ans += stk.top();
          stk.pop();
      } else {
          ans += ch;
      }
  }
  return ans;
}
```
双指针
```C++
string reverseOnlyLetters(string s) {
  int j = s.size() - 1;
  string res = s;
  for (int i = 0; i < s.size(); i++) {
      if (isalpha(s[i])) {
          while (!isalpha(s[j])) {
              j--;
          }
          res[i] = s[j--];
      } else {
          res[i] = s[i];
      }
  }
  return res;
}
```

## 反转字符串里的单词（LeetCode 151）
```C++
string reverseWords(string s) {
  reverse(s.begin(), s.end());
  int idx = 0;
  int n = s.size();
  for (int start = 0; start < n; start++) {
      if (idx != 0) s[idx++] = ' ';
      int end = start;
      while (end < n && s[end] != ' ') s[idx++] = s[end++];
      reverse(s.begin() + idx - (end - start), s.begin() + idx);
      start = end;
  }
  s.erase(s.begin() + idx, s.end());
  return s;
}
```

## 验证回文串（LeetCode 125）
```C++
bool isPalindrome(string s) {
  string temp;
  for (char ch : s) {
      if (isalnum(ch)) temp += tolower(ch);
  }
  int left = 0, right = temp.size() - 1;
  while (left < right) {
      if (temp[left] != temp[right]) {
          return false;
      }
      left++;
      right--;
  }
  return true;
}
```

## 字符串中第一个唯一字符（LeetCode 387）
```C++
int firstUniqChar(string s) {
  unordered_map<int, int> freq;
  for (char ch : s) {
      freq[ch]++;
  }
  for (int i = 0; i < s.size(); i++) {
      if (freq[s[i]] == 1) return i;
  }
  return -1;
}
```

## 判定是否为字符重排（LeetCode 242）
```C++
bool isAnagram(string s, string t) {
  if (s.length() != t.length()) return false;
  sort(s.begin(), s.end());
  sort(t.begin(), t.end());
  return s == t;
}
```
```C++
bool isAnagram(string s, string t) {
  if (s.length() != t.length()) return false;
  vector<int> table(26, 0);
  for (int i = 0; i < s.size(); i++) {
      table[s[i] - 'a']++;
  }
  for (int i = 0; i < t.size(); i++) {
      table[t[i] - 'a']--;
      if (table[t[i] - 'a'] < 0) {
          return false;
      }
  }
  return true;
}
```
