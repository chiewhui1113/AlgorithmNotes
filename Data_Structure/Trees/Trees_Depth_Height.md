# 二叉树的深度和高度问题
## 最大深度问题（LeetCode 104）
```C++
int maxDepth(TreeNode* root) {
  if (root == nullptr) return 0;
  return max(maxDepth(root->left), maxDepth(root->right)) + 1;
}
```
```C++
int maxDepth(TreeNode* root) {
  if (root == nullptr) return 0;
  queue<TreeNode*> que;
  int res = 0;
  que.push(root);
  while (!que.empty()) {
      int curSize = que.size();
      for (int i = 0; i < curSize; i++) {
          auto node = que.front(); que.pop();
          if (node->left) que.push(node->left);
          if (node->right) que.push(node->right);
      }
      res += 1;
  }
  return res;
}
```
## 判断平衡树（LeetCode 110）
```C++
int height(TreeNode* root) {
  if (root == nullptr) return 0;
  int leftHeight = height(root->left);
  int rightHeight = height(root->right);
  // 假如高度大于2 返回-1
  if (leftHeight == -1 || rightHeight == -1 || fabs(rightHeight - leftHeight) > 1) return -1;
  return fmax(leftHeight, rightHeight) + 1;
}

bool isBalanced(TreeNode* root) {
  return height(root) >= 0;
}
```

## 最小深度（LeetCode 111）
```C++
int minDepth(TreeNode* root) {
    if (root == nullptr) return 0;
    if (!root->left && !root->right) return 1;
    int res = INT_MAX;
    if (root->left) res = min(res, minDepth(root->left));
    if (root->right) res = min(res, minDepth(root->right));
    return res + 1;
}
```
```C++
int minDepth(TreeNode* root) {
  if (root == nullptr) return 0;
  queue<pair<TreeNode*, int>> que;
  que.emplace(root, 1);
  while (!que.empty()) {
      TreeNode* node = que.front().first;
      int curDepth = que.front().second;
      que.pop();
      if (!node->left && !node->right) return curDepth;
      if (node->left) que.emplace(node->left, curDepth + 1);
      if (node->right) que.emplace(node->right, curDepth + 1);
  }
  return 0;
}
```
## N叉树的最大深度（LeetCode 559）
```C++
int maxDepth(Node* root) {
  if (root == nullptr) return 0;
  int childMaxDepth = 0;
  vector<Node*> children = root->children;
  for (auto child : children) {
      int childDepth = maxDepth(child);
      childMaxDepth = max(childDepth, childMaxDepth);
  }
  return childMaxDepth + 1;
}
```
