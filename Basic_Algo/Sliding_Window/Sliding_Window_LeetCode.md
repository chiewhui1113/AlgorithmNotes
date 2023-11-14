# 滑动窗口算法题

## 无重复字符的最长子串（LeetCode 3）
```C++
int lengthOfLongestSubstring(string s) {
  if (s.size() <= 0) return 0;
  unordered_map<char, int> mp;
  int res = 0;
  int left = 0;
  for (int right = 0; right < s.size(); right++) {
      if (mp.count(s[right]) > 0) {
          // abba的时候，第二次访问b left=2，访问第二个a left反而是1
          // 有可能倒退，所以要max
          left = max(left, mp[s[right]] + 1);
      }
      mp[s[right]] = right;
      res = max(res, right - left + 1);
  }
  return res;
}
```

## 至少包含两个不同字符的最长子串（LeetCode 159）
```C++
int lengthOfLongestSubstringTwoDistinct(string s) {
  int n = s.length();
  if (n < 3) return n;
  int left = 0, right = 0;
  unordered_map<char, int> hashmap;
  int max_len = 2;
  while (right < n) {
    if (hashmap.size() < 3) {
      hashmap[s[right]] = right;
      right++;
    } else {
      // 删除最左边的
      int del_idx = min_element(hashmap.begin(), hashmap.end());
      hashmap.erase(del_idx);
      left = del_idx + 1;
    }
    max_len = max(max_len, right - left + 1);
  }
  return max_len;
}  
```

## 至少包含K个不同字符的最长子串（LeetCode 159）
```C++
int lengthOfLongestSubstringKDistinct(string s, int k) {
  if (s.length() < k + 1) {
    return s.length();
  }
  int left = 0, right = 0;
  unordered_map<char, int> hashmap;
  int maxLen = k;
  while (right < s.length()) {
    if (hashmap.size() < k) {
      hashmap[s[right]] = right++;
    }
    if (hashmap.size() == k) {
      int del_idx = min_element(hashmap.begin(), hashmap.end());
      hashmap.erase(del_idx);
      left = del_idx + 1;
    }
    maxLen = max(maxLen, right - left);
  }
  return maxLen;
}
```

## 长度最小的子数组（LeetCode 209）
```C++
int minSubArrayLen(int target, vector<int>& nums) {
  int left = 0, right = 0, sum = 0, min = INT_MAX;
  while (right < nums.size()) {
      sum += nums[right++];
      while (sum >= target) {
          min = std::min(min, right - left);
          sum -= nums[left++];
      }
  }
  if (min == INT_MAX) return 0;
  return min;
}
```

## 盛水最多的容器（LeetCode 11）
```C++
int maxArea(vector<int>& height) {
  int left = 0, right = height.size() - 1, res = 0;
  while (left < right) {
      res = max(res, min(height[left], height[right]) * (right - left));
      if (height[left] < height[right]) {
          left++;
      } else {
          right--;
      }
  }
  return res;
}
```

## 字符串的排列（LeetCode 567）
```C++
bool checkInclusion(string s1, string s2) {
  int n = s1.length(), m = s2.length();
  if (n > m) return false;
  vector<int> cnt1(26), cnt2(26);
  for (int i = 0; i < n; i++) {
      cnt1[s1[i] - 'a']++;
      cnt2[s2[i] - 'a']++;
  }
  if (cnt1 == cnt2) return true;
  for (int i = n; i < m; i++) {
      cnt2[s2[i] - 'a']++;
      cnt2[s2[i - n] - 'a']--;
      if (cnt1 == cnt2) return true;
  }
  return false;
}
```

## 找到字符中所有字母异位（LeetCode 438）
```C++
vector<int> findAnagrams(string s, string p) {
  int sLen = s.size(), pLen = p.size();
  if (sLen < pLen) return vector<int>();
  vector<int> ans;
  vector<int> sCount(26);
  vector<int> pCount(26);
  for (int i = 0; i < pLen; i++) {
      sCount[s[i] - 'a']++;
      pCount[p[i] - 'a']++;
  }
  if (sCount == pCount) ans.emplace_back(0);
  for (int i = 0; i < sLen - pLen; i++) {
      sCount[s[i] - 'a']--;
      sCount[s[i + pLen] - 'a']++;
      if (sCount == pCount) ans.emplace_back(i + 1);
  }
  return ans;
}
```

