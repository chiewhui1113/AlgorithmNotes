# 位运算
1. 算法右移 = 高位补最高位
2. 逻辑右移 = 高位补0

## 乘除法
1. 往左移k位 = ✖️2^k
2. 往右移k位 = ➗2^k
3. 整数除法向0取整，右移运算向下取整

## 获取
```C++
bool getBit(int num, int i) {
  return ((num & (1 << i)) != 0);
}
```

## 设置
```C++
int setBit(int num, int i) {
  return num | (1 << i);
}
```

## 清零
```C++
int clearBit(int num, int i) {
  int mask = ~(1 << i);
  return mask & num;
}
```

## 更新
```C++
int updateBit(int num, int i, int v) {
  int mask = ~(1 << i);
  return (mask & num) | (v << i);
}
```
