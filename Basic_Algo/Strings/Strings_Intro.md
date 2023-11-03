# 字符串

## 转换成小写字母（LeetCode 709）
```C++
string toLowerCase(string s) {
  for (int i = 0; i < s.length(); i++) {
      if (s[i] >= 65 && s[i] <= 90) {
          s[i] += 32;
      }
  }
  return s;
}
```

## 字符串转换整数（LeetCode 8）
1. 去除前导空格
2. 记录正负
3. 溢出问题，范围为[-2^31, 2^31 - 1]
```C++
int myAtoi(string s) {
  int n = s.length();
  int index = 0;
  int res = 0;
  bool negative = false;
  // 去除前导空格
  while( index < n && s[index] == ' ') {
      index++;
  }
  // 假如s无字符
  if( index == n) {
      return 0;
  }
  // 记录正负
  if( s[index] == '-' ) {
      negative = true;
  }

  if( s[index] == '-' || s[index] == '+' ) {
      index++;
  }

  while( index < n && s[index] >= '0' && s[index] <= '9' ) {
      int lastNum = s[index] - 48;
      // 溢出问题
      if ( !negative && ( res > 214748364 || ( res == 214748364 && (lastNum == 8 || lastNum == 9 )))) {
          return 2147483647;
      }

      if ( negative && ( -res < -214748364 || ( -res == -214748364 && (lastNum == 8 || lastNum == 9 ) ))) {
          return -2147483648;
      }
      res = res * 10 + lastNum;
      index++;
  }
  return negative ? - res : res;
}
```
