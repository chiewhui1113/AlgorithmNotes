# 数字与数学基础问题

## 符号统计（LeetCode 1822）
```C++
int arraySign(vector<int>& nums) {
  int sign = 1;
  for (int i = 0; i < nums.size(); i++) {
      if (nums[i] == 0) return 0;
      else if (nums[i] < 0) sign = -sign;
  }
  return sign;
}
```

## 阶乘0的个数（LeetCode 172）
```C++
int trailingZeroes(int n) {
  int zeroes = 0;
  while (n) {
      n /= 5;
      zeroes += n;
  }
  return zeroes;
}
```

## 整数反转（LeetCode 7）
```C++
int reverse(int x) {
  int res = 0;
  while (x) {
      if (res < INT_MIN / 10 || res > INT_MAX / 10) return 0;
      int digit = x % 10;
      x /= 10;
      res = res * 10 + digit;
  }
  return res;
}
```

## 回文数（LeetCode 8）
```C++
bool isPalindrome(int x) {
  if (x < 0 || ((x % 10 == 0) && x != 0)) {
      return false;
  }
  int reversed = 0;
  while (reversed < x) {
      reversed = reversed * 10 + x % 10;
      x /= 10;
  }
  return x == reversed || x == reversed / 10;
}
```

## 七进制数（LeetCode 504）
```C++
string convertToBase7(int num) {
  if (num == 0) return "0";
  int ori_num = num; 
  if (num < 0) {
      num *= -1;
  }
  string res = "";
  while (num) {
      int digit = num % 7;
      res = to_string(digit) + res;
      num /= 7;
  }
  if (ori_num < 0) {
      res = "-" + res;
  }
  return res;
}
```

## 进制转换
```Python
def convertToBaseX(M, N):
  if (M < 0):
    M = -M;
    sign = -1
  else:
    sign = 1

  digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 'A', 'B', 'C', 'D', 'E', 'F']
  res = []
  while M > 0:
    digit = M % N
    res.append(digits[digit])
    M = M // N
  if sign == -1:
    res.append("-")
  res.reverse()
  return ''.join(res)
```
