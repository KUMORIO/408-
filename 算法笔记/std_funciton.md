# std::function

## 用法1：在函数里定义一个函数

```c++  
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
```



## sort函数指定升序或者降序

```c++
std::sort(nums.begin(), nums.end(), descending); // 降序排序
bool descending(int a, int b) {
    return a > b;
}
sort(A,A+100,less<int>());//升序排列
sort(A,A+100,greater<int>());//降序排列
```









>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>
>



























