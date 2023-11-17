# 回溯

## 模版
```C++
void backtracking(parameters) {
  if (end condition) {
    save result;
    return;
  }
  for () {
    handle node;
    backtracking();
    undo the previous result;
  }
}
```

## 输出二叉树的所有路径（LeetCode 257）
```C++
void traversal(TreeNode* cur, string path, vector<string>& res) {
    path += to_string(cur->val);
    if (cur->left == NULL && cur->right == NULL) {
        res.push_back(path);
        return;
    }
    if (cur->left) {
        path += "->";
        traversal(cur->left, path, res);
        path.pop_back(); // "-"
        path.pop_back(); // ">"
    }
    if (cur->right) {
        path += "->";
        traversal(cur->right, path, res);
        path.pop_back();
        path.pop_back();
    }
}

vector<string> binaryTreePaths(TreeNode* root) {
    vector<string> res;
    if (root == NULL) return res;
    string path = "";
    traversal(root, path, res);
    return res;
}
```

## 路径总和（LeetCode 113）
```C++
vector<vector<int>> res;
vector<int> path;

void traversal(TreeNode* cur, int count) {
  if (!cur->left && !cur->right && count == 0) {
      res.push_back(path);
      return;
  }
  if (cur->left) {
      path.push_back(cur->left->val);
      count -= cur->left->val;
      traversal(cur->left, count);
      count += cur->left->val;
      path.pop_back();
  }
  if (cur->right) {
      path.push_back(cur->right->val);
      count -= cur->right->val;
      traversal(cur->right, count);
      count += cur->right->val;
      path.pop_back();
  }
}

vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
  res.clear();
  path.clear();
  if (root == NULL) return res;
  path.push_back(root->val);
  traversal(root, targetSum - root->val);
  return res;
}
```
