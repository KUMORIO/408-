# 宽度优先搜索

## 算法1:二叉树层次遍历

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        queue<TreeNode*> que;
        vector<vector<int>> res;
        if (root != nullptr) que.push(root);
        while (!que.empty()) {
            vector<int> tmp;
            for(int i = que.size(); i > 0; --i) {
                root = que.front();
                que.pop();
                tmp.push_back(root->val);
                if (root->left != nullptr) que.push(root->left);
                if (root->right != nullptr) que.push(root->right);
            }
            res.push_back(tmp);
        }
        return res;
    }
};
```

## 算法二2：锯齿形遍历

```c++
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        queue<TreeNode*> que;
        vector<vector<int>> res;
        if (root != nullptr) que.push(root);
        for (bool even = false; !que.empty(); even = !even)
        {
            vector<int> tmp;
            for(int i = que.size(); i > 0; --i) 
            {              
                    root = que.front();
                    que.pop();
                    tmp.push_back(root->val);
                    if (root->left != nullptr) que.push(root->left);
                    if (root->right != nullptr) que.push(root->right);
            }
            if(even) reverse(tmp.begin(),tmp.end());
			res.push_back(tmp);
        }
        return res;
    }
};
```

## 算法三：二叉树的最大深度

### 法1：层次遍历-广度优先

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        queue<TreeNode*> que;
        int res=0;
        if (root != nullptr) que.push(root);
        while (!que.empty())
        {
            vector<int> tmp;
            for(int i = que.size(); i > 0; --i) 
            {              
                    root = que.front();
                    que.pop();
                    if (root->left != nullptr) que.push(root->left);
                    if (root->right != nullptr) que.push(root->right);
            }
            res+=1;
        }
        return res;
    }
};
```

### 法2：后序遍历-深度优先

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```

## 算法四：二叉树最小深度

+ 最小深度是从根节点到最近叶子节点的最短路径上的节点数量
+ **说明：**叶子节点是指没有子节点的节点。

### 法1：层次遍历-广度优先

```c++
class Solution {
public:
    int minDepth(TreeNode* root) {
      queue<TreeNode*> que;
        int res = 0;
        if (root == nullptr) return res;
        else que.push(root);
        while (!que.empty()) {
            for(int i = que.size(); i > 0; --i) {
                root = que.front();
                que.pop();
                if (root->left == nullptr && root->right == nullptr) return res+1;
                if(root->left != nullptr)que.push(root->left);
                if(root->right != nullptr)que.push(root->right);
            }
            res++;
        }
        return -1;
    }
};
```

### 法2：后序遍历-深度优先

```c++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root==nullptr) return 0;
        if(root->left==nullptr&& root->right==nullptr) return 1;
        if(root->left==nullptr && root->right!=nullptr) return minDepth(root->right)+1;
        if(root->left!=nullptr && root->right==nullptr) return minDepth(root->left)+1;
        int leftDepth = minDepth(root->left);
        int rightDepth = minDepth(root->right);
        return min(leftDepth, rightDepth)+1;
    }
};
```

