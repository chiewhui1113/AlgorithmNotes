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
      int del_idx = min_elemenet(hashmap.begin(), hashmap.end());
      hashmap.erase(del_idx);
      left = del_idx + 1;
    }
    max_len = max(max_len, right - left + 1);
  }
  return max_len;
}  
```
