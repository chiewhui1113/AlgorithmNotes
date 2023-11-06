# 数论
## 辗转相除法（Euclidean Algorithm）
![IMG_F96187AFF30E-1](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/7163ef4d-df27-4d31-9fcc-7665e1710a8b)
```C++
int gcd(int a, int b) {
  int k = -1;
  while (k != 0) {
    k = a % b;
    a = b;
    b = k;
  }
  return a;
}
```

## 素数和合数
![IMG_4C247CA5C4F6-1](https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/ad66d5d7-8083-4b54-9a03-b078e49592c0)
```C++
int isPrime(int x) {
  int max = (int) sqrt(x);
  for (int i = 2; i <= max; i++) {
    if (x % i == 0) return 0;
  }
  return 1;
}
```

## 埃式筛（LeetCode 204）
找到质数后把所有倍数删除
```C++
int countPrimes(int n) {
  vector<bool> seen(n, false);
  int ans = 0;
  for (int i = 2; i < n; i++) {
      if (seen[i]) continue;
      ans++;
      if ((long) i * i < n) {
          for (int j = i * i; j < n; j += i) {
              seen[j] = true;
          }
      }
  }
  return ans;
}
```

## 丑数
只包含质因子2，5，7的数位丑数
```C++
bool isUgly(int n) {
  if (n <= 0) return false;
  int factors[] = {2, 3, 5};
  for (int i = 0; i < 3; i++) {
    while (n % factors[i] == 0) {
      n /= factors[i];
    }
  }
  return n == 1;
}
```
