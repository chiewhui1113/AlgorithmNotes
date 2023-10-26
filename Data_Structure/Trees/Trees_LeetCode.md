# 树的高频算法题

## 二叉树的层序遍历（LeetCode 102）
```C++
vector<vector<int>> levelOrder(TreeNode* root) {
  vector<vector<int>> res;
  if (!root) return res;
  queue<TreeNode*> q;
  q.push(root);
  while(!q.empty()) {
      res.push_back(vector<int>());
      int curLevelSize = q.size();
      for (int i = 0; i < curLevelSize; i++) {
          auto node = q.front(); q.pop();
          res.back().push_back(node->val);
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
      }
  }
  return res;
}
```
## 二叉树的层序遍历 - 自底向上（LeetCode 107）
```C++
vector<vector<int>> levelOrderBottom(TreeNode* root) {
  vector<vector<int>> res;
  if (!root) return res;
  queue<TreeNode*> q;
  q.push(root);
  while(!q.empty()) {
      res.push_back(vector<int>());
      int curLevelSize = q.size();
      for (int i = 0; i < curLevelSize; i++) {
          auto node = q.front(); q.pop();
          res.back().push_back(node->val);
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
      }
  }
  reverse(res.begin(), res.end()); // 翻转一下就好了
  return res;
}
```
## 二叉树的层序遍历 - 锯齿形（LeetCode 103）
```C++
vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
  vector<vector<int>> res;
  if (!root) return res;
  deque<TreeNode*> deq;
  deq.push_back(root);
  bool zigzag = true;
  while (!deq.empty()) {
      int curLevelSize = deq.size();
      res.push_back(vector<int>());
      for (int i = 0; i < curLevelSize; i++) {
          if (zigzag) {
              auto node = deq.front(); deq.pop_front();
              res.back().push_back(node->val);
              if (node->left) deq.push_back(node->left);
              if (node->right) deq.push_back(node->right);
          } else {
              auto node = deq.back(); deq.pop_back();
              res.back().push_back(node->val);
              if (node->right) deq.push_front(node->right); // 这里left和right push的顺序倒转
              if (node->left) deq.push_front(node->left);
          }
      }
      zigzag = !zigzag;
  }
  return res;
}
```

## N叉树的层序遍历 （LeetCode 429）
```C++
vector<vector<int>> levelOrder(Node* root) {
  vector<vector<int>> res;
  if (!root) return res;
  queue<Node*> q;
  q.push(root);
  while (!q.empty()) {
      int curLevelSize = q.size();
      res.push_back(vector<int>());
      for (int i = 0; i < curLevelSize; i++) {
          auto node = q.front(); q.pop();
          res.back().push_back(node->val);
          for (Node* child : node->children) {
              q.push(child);
          }
      }
  }
  return res;
}
```

## 找出二叉树中每层的最大值（LeetCode 515）
```C++
vector<int> largestValues(TreeNode* root) {
  if (!root) return {};
  queue<TreeNode*> q;
  vector<int> res;
  q.push(root);
  while(!q.empty()) {
      int max = INT_MIN;
      int size = q.size();
      for (int i = 0; i < size; i++) {
          auto node = q.front(); q.pop();
          if (node->val > max) max = node->val;
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
      }
      res.push_back(max);
  }
  return res;
}
```

## 找出二叉树中每层的平均值（LeetCode 637）
```C++
vector<double> averageOfLevels(TreeNode* root) {
  if (!root) return {};
  vector<double> res;
  queue<TreeNode*> q;
  q.push(root);
  while(!q.empty()) {
      int size = q.size();
      double sum = 0;
      for (int i = 0; i < size; i++) {
          auto node = q.front(); q.pop();
          sum += node->val;
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
      }
      res.push_back(sum / size);
  }
  return res;
}
```

## 二叉树的右视图（LeetCode 199）
```C++
vector<int> rightSideView(TreeNode* root) {
  if (!root) return {};
  vector<int> res;
  queue<TreeNode*> q;
  q.push(root);
  while(!q.empty()) {
      int size = q.size();
      for (int i = 0; i < size; i++) {
          auto node = q.front(); q.pop();
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
          if (i == size - 1) res.push_back(node->val);
      }
  }
  return res;
}
```

## 最底层最左边（LeetCode 513）
```C++
int findBottomLeftValue(TreeNode* root) {
  if (!root) return root->val;
  queue<TreeNode*> q;
  q.push(root);
  TreeNode* tmp = new TreeNode(-100);
  while(!q.empty()) {
      tmp = q.front(); q.pop();
      if (tmp->right) q.push(tmp->right);
      if (tmp->left) q.push(tmp->left);
  }
  return tmp->val;
}
```

## 最近公共祖先（LeetCode 236）
<img width="420" alt="image" src="https://github.com/chiewhui1113/AlgorithmNotes/assets/75370269/adbbc974-106d-4755-bf9a-04a8dcb720ce"><br>
6的祖先节点为3和5，7的祖先节点为2，5和3。因此，他们的最近公共祖先为5。假如root是p和q的最近公共祖先：
1. p和q都在root的子树中，位于root的两侧
2. p = root，q在root的左或右子树
3. q = root，p在root的左或右子树

因此，我们需要递归判断：

1. 如果left和right都是NULL，代表p和q都不存在于root的子树中，返回NULL
2. 如果left和right都不为null，代表p和q在root的两侧，返回root
3. 如果left为空right不为空，需要判断root是否是p或q入，如果是说明一方是另一方的祖先。否则，说明left的子树没查到，需要递归去查right的子树里有没有
```C++
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
  if (!root || root == p || root == q) return root;
  TreeNode* left = lowestCommonAncestor(root->left, p, q);
  TreeNode* right = lowestCommonAncestor(root->right, p, q);
  if (!left && !right) return NULL;
  if (!left) return right;
  if (!right) return left;
  return root;
}
```
