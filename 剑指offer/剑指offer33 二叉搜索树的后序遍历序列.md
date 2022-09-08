# 剑指offer33 二叉搜索树的后序遍历序列

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

## 思路1：递归

二叉搜索树的后序遍历根节点为最后一个数，通过二叉搜索树的性质，左子树比根节点小，右子树比根节点大，不断的划分左右区间进行递归。

```c++
class Solution {
public:
    bool dfs(vector<int>& postorder, int begin, int end) {
        if(begin >= end)
            return true;
        // 获取左子树的长度
        int cur = begin;
        while(postorder[cur] < postorder[end]) {
            cur++;
        }
        // 获取右子树的长度
        int middle = cur;
        while(postorder[cur] > postorder[end]) {
            cur++;
        }
        return cur == end && dfs(postorder,begin,middle-1) && dfs(postorder,middle, end-1);
    }
    bool verifyPostorder(vector<int>& postorder) {
        return dfs(postorder,0,postorder.size()-1); 
    }
};
```

