# 位运算的高频算法题
## 位1的个数（LeetCode 191）
每次往右移一位，然后+count
```C++
int hammingWeight(uint32_t n) {
  int count = 0;
  for (int i = 0; i < 32; i++) {
      count += (n >> i) & 1;
  }
  return count;
}
```

每次删除最后一位的1，然后+count
```C++
int hammingWeight(uint32_t n) {
  int count = 0;
  while (n != 0) {
      n = n & (n - 1);
      count++;
  }
  return count;
}
```

## 比特位计数（LeetCode 338）
```C++
vector<int> countBits(int n) {
  vector<int> bits(n + 1);
  for (int i = 0; i <= n; i++) {
      bits[i] = 0;
      for (int j = 0; j < 32; j++) {
          bits[i] += (i >> j) & 1;
      }
  }
  return bits;
}
```
```C++
int countOnes(int n) {
  int count = 0;
  while (n != 0) {
      n &= n - 1;
      count++;
  }
  return count;
}

vector<int> countBits(int n) {
  vector<int> bits(n + 1);
  for (int i = 0; i <= n; i++) {
      bits[i] = countOnes(i);
  }
  return bits;
}
```

## 颠倒无符号整数（LeetCode 190）
原始数据：1001 1111 0000 0110 <br>
第一步：获得n的最低位0，将其左移16-1=15位，得到：<br>
reversed：0*** **** **** **** <br>
n右移一位：0100 1111 1000 0011 <br>

第二步：获得n的最低位1，将其左移15-1=14位，并与reversed想加得到：<br>
reversed：01** **** **** **** <br>
n右移一位：0010 0111 1100 0001 <br>

重复直到n=0 <br>

```C++
uint32_t reverseBits(uint32_t n) {
  uint32_t reversed = 0, power = 31;
  while (n) {
      reversed += (n & 1) << power;
      power--;
      n >>= 1;
  }
  return reversed;
}
```

## 位运算实现加法（LeetCode 371）
查看是否有两个1，往右移（进位）然后异或
```C++
int getSum(int a, int b) {
  while (b) {
      int sign = (a & b) << 1;
      a ^= b;
      b = sign;
  }
  return a;
}
```

## 位运算实现乘法
```C++
int multiply(int a, int b) {
  int min = a < b : a ? b;
  int max = a > b : a ? b;
  int ans = 0;
  while (min) {
    if ((min & 1) == 1) {
      ans += max;
    }
    min >>= 1;
    max += max;
  }
  return ans;
}  
```
