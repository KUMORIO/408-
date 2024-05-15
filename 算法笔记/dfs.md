# 深度优先搜索

## 模板一：二叉树路径

### 模板1

+ **自顶而下**

```c++
//一般路径：
vector<vector<int>>res;
void dfs(TreeNode*root,vector<int>path)
{
    if(!root) return;  //根节点为空直接返回
    path.push_back(root->val);  //作出选择
    if(!root->left && !root->right) //如果到叶节点  
    { 
        res.push_back(path);
        return;
    }
    dfs(root->left,path);  //继续递归
    dfs(root->right,path);
}
```

```c++
//给定和的路径：
void dfs(TreeNode*root, int sum, vector<int> path)
{
    if (!root) return;
    sum -= root->val;
    path.push_back(root->val);
    if (!root->left && !root->right && sum == 0)
    {
        res.push_back(path);
        return;
    }
    dfs(root->left, sum, path);
    dfs(root->right, sum, path);
}
```

###  模板2

+ **非自顶而下**

```c++
int res=0;
int maxPath(TreeNode *root) //以root为路径起始点的最长路径
{
    if (!root) return 0;
    int left=maxPath(root->left);
    int right=maxPath(root->right);
    res = max(res, left + right + root->val); //更新全局变量  
    return max(left, right);   //返回左右路径较长者
}
```

## 算法一：[112. 路径总和](https://leetcode.cn/problems/path-sum/)

```c++
class Solution {
private:
    bool dfs(TreeNode* node, int targetSum){
        targetSum -= node->val;     // 累加当前节点值
        if(!node->left && !node->right&&targetSum==0)return true; // 当前节点为叶子节点，判断路径和是否等于目标值
        if(node->left && dfs(node->left, targetSum))return true;   // 当前节点左子节点存在且其左子树中存在满足目标的路径和，返回true
        if(node->right && dfs(node->right, targetSum))return true;   // 当前节点右子节点，返回其右子树的搜索结果
        return false;    // 没有满足条件的路径和，返回false
    }
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        return root ? dfs(root, targetSum) : false;  // 根节点为空直接返回false，否则从根节点开始搜索
    }
};
```

##  算法二：[257. 二叉树的所有路径](https://leetcode.cn/problems/binary-tree-paths/)

leetcode257-给你一个二叉树的根节点 `root` ，按 **任意顺序** ，返回所有从根节点到叶子节点的路径。

```c++
class Solution 
{
	public:
    vector<string> binaryTreePaths(TreeNode* root) 
    {
        vector<string> res;
        function<void(TreeNode*, string)>dfs =[&](TreeNode*root,string path)
        {
            if(!root) return;  //根节点为空直接返回
            path+= to_string(root->val);  //作出选择
            if(!root->left && !root->right) //如果到叶节点  
            {
                res.push_back(path);
                return;
            }
            dfs(root->left,path+"->");  //继续递归
            dfs(root->right,path+"->");
        };
        dfs(root, "");
        return res;
    }
};
```

## 算法三：[从叶结点开始的最小字符串](https://leetcode.cn/problems/smallest-string-starting-from-leaf/)

```c++
class Solution 
{
    public:
priority_queue<string, vector<string>, greater<string> > pq;

    string smallestFromLeaf(TreeNode *root)
    {
        dfs(root, "");
        return pq.top();
    }

    void dfs(TreeNode *root, string s)
    {
        if (!root)
            return;
        s += 'a' + root->val;
        if (!root->left && !root->right)
        {
            reverse(s.begin(), s.end()); //题目要求从根节点到叶节点，因此反转
            pq.push(s);
            return;
        }
        dfs(root->left, s);
        dfs(root->right, s);
    }

};
```

## 算法四：[687. 最长同值路径](https://leetcode.cn/problems/longest-univalue-path/)

```c++
class Solution {
public:
int res;
    int longestUnivaluePath(TreeNode *root)
    {

        if (!root)
            return 0;
        longestPath(root);
        return res;
    }
    
    int longestPath(TreeNode *root)
    {
        if (!root)
            return 0;
        int left = longestPath(root->left), right = longestPath(root->right);
        // 如果存在左子节点和根节点同值，更新左最长路径;否则左最长路径为0
        if (root->left && root->val == root->left->val)
            left++;
        else
            left = 0;
        if (root->right && root->val == root->right->val)
            right++;
        else
            right = 0;
        res = max(res, left + right);
        return max(left, right);
    }
};
```

## 算法五：[543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)

```c++
class Solution {
public:
int res = 0;  
int diameterOfBinaryTree(TreeNode *root)
{
    maxPath(root);
    return res;
}
int maxPath(TreeNode *root)
{
// 这里递归结束条件要特别注意：不能是!root(而且不需要判断root为空,因为只有非空才会进入递归)，因为单个节点路径长也是0
    if (!root->left && !root->right)  
        return 0;
    int left = root->left ? maxPath(root->left) + 1 : 0;  //判断左子节点是否为空，从而更新左边最长路径
    int right = root->right ? maxPath(root->right) + 1 : 0;
    res = max(res, left + right); //更新全局变量
    return max(left, right);  //返回左右路径较大者
}
};
```

## 算法六：[129. 求根节点到叶节点数字之和](https://leetcode.cn/problems/sum-root-to-leaf-numbers/)

```c++
class Solution {
public:
    vector<long long>res;
    int sumNumbers(TreeNode* root) {
        dfs(root,0);
        long long sum=0;
        for(long long i:res)
        {
            sum+=i;
        }
        return sum;
    }
    void dfs(TreeNode*root,long long path)
    {
        if(!root) return;  //根节点为空直接返回
        path=path*10+root->val;  //作出选择
        if(!root->left && !root->right) //如果到叶节点  
        { 
            res.push_back(path);
            return;
        }
        dfs(root->left,path);  //继续递归
        dfs(root->right,path);
    }
};
```

