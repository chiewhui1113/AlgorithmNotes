# 二叉树的遍历
深度优先遍历有前中后三种情况，三种可以用递归/来遍历，只需要调换顺序
## 递归
### 前序
```C++
void preOrder(TreeNode* root, vector<int>& res) {
  if (root == NULL) return;
  res.push_back(root->val);
  preOrder(root->left, res);
  preOrder(root->right, res);
}

vector<int> preorderTraversal(TreeNode* root) {
  vector<int> res;
  preOrder(root, res);
  return res;
}
```
### 中序
```C++
void inOrder(TreeNode* root, vector<int>& res) {
  if (root == NULL) return;
  inOrder(root->left, res);
  res.push_back(root->val);
  inOrder(root->right, res);
}

vector<int> inorderTraversal(TreeNode* root) {
  vector<int> res;
  inOrder(root, res);
  return res;
}
```
### 后序
```C++
void inOrder(TreeNode* root, vector<int>& res) {
  if (root == NULL) return;
  inOrder(root->left, res);
  inOrder(root->right, res);
  res.push_back(root->val);
}

vector<int> inorderTraversal(TreeNode* root) {
  vector<int> res;
  inOrder(root, res);
  return res;
}
```
## 迭代
### 前序
```C++
vector<int> preorderTraversal(TreeNode* root) {
  vector<int> res;
  if (root == nullptr) return res;
  stack<TreeNode*> stk;
  TreeNode* node = root;
  while (!stk.empty() || node != nullptr) {
      while (node != nullptr) {
          res.push_back(node->val);
          stk.push(node);
          node = node->left;
      }
      node = stk.top(); stk.pop();
      node = node->right;
  }
  return res;
}
```
### 中序
```C++
vector<int> inorderTraversal(TreeNode* root) {
  vector<int> res;
  if (root == nullptr) return res;
  stack<TreeNode*> stk;
  TreeNode* node = root;
  while (!stk.empty() || node != nullptr) {
      while (node != nullptr) {
          stk.push(node);
          node = node->left;
      }
      node = stk.top(); stk.pop();
      res.push_back(node->val);
      node = node->right;
  }
  return res;
}
```
### 后序
```C++
vector<int> postorderTraversal(TreeNode* root) {
  vector<int> res;
  if (root == nullptr) return res;
  stack<TreeNode*> stk;
  TreeNode* node = root;
  while (!stk.empty() || node != nullptr) {
      while (node != nullptr) {
          res.push_back(node->val);
          stk.push(node);
          node = node->right;
      }
      node = stk.top(); stk.pop();
      node = node->left;
  }
  reverse(res.begin(), res.end());
  return res;
    }
```
