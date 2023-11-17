# 贪心

## 什么是贪心
贪心算法是指在对问题求解时，每一步选择都采取最好或最优的选择。贪心算法不一定会得到最优解，
但是都是接近最优解的结果。贪心算法有很多应用场景，例如选择排序、拓扑排序、堆排序、Prim、
Fruskal、Dijkstra、硬币找零、分数背包、并查集等

## 分发饼干（LeetCode 455）
```C++
int findContentChildren(vector<int>& g, vector<int>& s) {
  sort(g.begin(), g.end());
  sort(s.begin(), s.end());
  int cookie = 0;
  int child = 0;
  while (cookie < s.size() && child < g.size()) {
      if (s[cookie] >= g[child]) child++;
      cookie++;
  }
  return child;
}
```

## 柠檬水找零（LeetCode 860）
```C++
bool lemonadeChange(vector<int>& bills) {
  int five = 0;
  int ten = 0;
  for (auto bill : bills) {
      if (bill == 5) {
          five++;
      } else if (bill == 10) {
          if (five == 0) return false;
          five--;
          ten++;
      } else if (bill == 20) {
          if (ten >= 1 && five >= 1) {
              ten--;
              five--;
          } else if (five >= 3) {
              five -= 3;
          } else {
              return false;
          }
      }
  }
  return true;
}
```

## 分发糖果（LeetCode 135）
```C++
int candy(vector<int>& ratings) {
  int n = ratings.size();
  vector<int> left(n, 1);
  for (int i = 1; i < n; i++) {
      if (ratings[i] > ratings[i - 1]) {
          left[i] = left[i - 1] + 1;
      } 
  }
  int right = 1, ret = 0;
  for (int i = n - 1; i >= 0; i--) {
      if (i < n - 1 && ratings[i] > ratings[i + 1]) {
          right++;
      } else {
          right = 1;
      }
      ret += max(left[i], right);
  }
  return ret;
}
```
