# 数学与数字高频算法题
## 加一（LeetCode 66）
```C++
vector<int> plusOne(vector<int>& digits) {
  int n = digits.size();
  for (int i = n - 1; i >= 0; i--) {
      if (digits[i] != 9) {
          digits[i] += 1;
          for (int j = i + 1; j < n; j++) {
              digits[j] = 0;
          }
          return digits;
      }
  }

  vector<int> res(n + 1);
  res[0] = 1;
  return res;
}
```

## 字符串加法
```C++
string addString(string num1, string num2) {
  int i = num1.size() - 1;
  int j = num2.size() - 1;
  int add = 0;
  string ans = "";
  while (i >= 0 || j >= 0 || add != 0) {
    int x = i >= 0 ? num1[i] : 0;
    int y = j >= 0 ? num2[j] : 0;
    int res = x + y + add;
    ans = (res % 10) + ans;
    add = res / 10;
    i--;
    j--;
  }
  return ans;
}
```

## 二进制加法（LeetCode 67） 
```C++
string addBinary(string a, string b) {    
  int carry = 0;
  string res = "";
  for (int i = a.size() - 1, j = b.size() - 1; i >= 0 || j >= 0; i--, j--) {
      int sum = carry;
      sum += i >= 0 ? a[i] - '0' : 0;
      sum += j >= 0 ? b[j] - '0' : 0;
      res += (sum % 2) + '0';
      carry = sum / 2;
  }
  if (carry) res += '1';
  reverse(res.begin(), res.end());
  return res;
}
```

## 求2的幂（LeetCode 231）
```C++
bool isPowerOfTwo(int n) {
  if (n <= 0) return false;
  while (n > 1) {
      if (n % 2 != 0) return false;
      n /= 2;
  }
  return true;
}
```

## 求3的幂（LeetCode 326）
```C++
bool isPowerOfThree(int n) {
  if (n <= 0) return false;
  while (n > 1) {
      if (n % 3 != 0) return false;
      n /= 3;
  }
  return true;
}
```
拓展：不超过2^31-1的最大3的幂是3^19（1162261467）
```C++
bool isPowerOfThree(int n) {
  return n > 0 && 1162261467 % n == 0;
}
```

## 求4的幂（LeetCode 342）
```C++
bool isPowerOfFour(int n) {
  if (n <= 0) return false;
  while (n > 1) {
      if (n % 4 != 0) return false;
      n /= 4;
  }
  return true;
}
```
