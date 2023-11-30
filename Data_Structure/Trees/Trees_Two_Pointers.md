# 二叉树里的双指针
## 判断两棵树是否相同（LeetCode 100）
```C++
bool isSameTree(TreeNode* p, TreeNode* q) {
  if (!p && !q) return true;
  else if (!p || !q) return false;
  else if (p->val != q->val) return false;
  # 左边右边查看是否相等
  return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
}
```
## 判断二叉树是否对称（LeetCode 101）
```C++
bool check(TreeNode* q, TreeNode* p) {
  if (!q && !p) return true;
  else if (!q || !p) return false;
  else if (q->val != p->val) return false;
  else return check(q->left, p->right) && check(q->right, p->left);
}

bool isSymmetric(TreeNode* root) {
  return check(root, root);
}
```
## 合并二叉树（LeetCode 617）
```C++
TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
  if (root1 == nullptr) return root2;
  if (root2 == nullptr) return root1;
  # 创建新节点把当前两个值加起来
  TreeNode* node = new TreeNode(root1->val + root2->val);
  # 左边右边的子节点也+起来
  node->left = mergeTrees(root1->left, root2->left);
  node->right = mergeTrees(root1->right, root2->right);
  return node;
}
```
## 二叉树的所有路径（LeetCode 257）
```C++
void findPath(TreeNode* root, string path, vector<string>& paths) {
  if (root != nullptr) {
      path += to_string(root->val);
      if (!root->left && !root->right) {
          paths.push_back(path);
      } else {
          path += "->";
          findPath(root->left, path, paths);
          findPath(root->right, path, paths);
      }
  }
}

vector<string> binaryTreePaths(TreeNode* root) {
  vector<string> paths;
  findPath(root, "", paths);
  return paths;
}
```
## 路径总和（LeetCode 112）
```C++
bool hasPathSum(TreeNode* root, int targetSum) {
  if (root == nullptr) return false;
  if (!root->left && !root->right) return root->val == targetSum;
  return hasPathSum(root->left, targetSum - root->val) || 
         hasPathSum(root->right, targetSum - root->val);
}
```
## 反转二叉树（LeetCode 226）
### 前序
```C++
TreeNode* invertTree(TreeNode* root) {
  if (root == nullptr) return NULL;
  # 平常交换的三个步骤
  TreeNode* temp = root->left;
  root->left = root->right;
  root->right = temp;
  invertTree(root->left);
  invertTree(root->right);
  return root;
}
```
### 后序
```C++
TreeNode* invertTree(TreeNode* root) {
  if (root == nullptr) return NULL;
  TreeNode* left = invertTree(root->left);
  TreeNode* right = invertTree(root->right);
  root->left = right;
  root->right = left;
  return root;
}
```
### 层次遍历
```C++
# 每一层交换
TreeNode* invertTree(TreeNode* root) {
  queue<TreeNode*> que;
  if (root != NULL) que.push(root);
  while (!que.empty()) {
      auto node = que.front(); que.pop();
      swap(node->left, node->right);
      if (node->left) que.push(node->left);
      if (node->right) que.push(node->right);
  }
  return root;
}
```
