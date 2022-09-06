# 剑指offer36 二叉搜索树与双向链表

[剑指 Offer 36. 二叉搜索树与双向链表 - 力扣（LeetCode）](https://leetcode.cn/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

问题： 输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

## 概念

二叉搜索树：按顺序的进行排序，左子树比根节点小，右子树比根节点大。

**关键点**：二叉搜索树的中序遍历是从小到大排序，后序遍历是从大到小排序

双向链表：链表节点前驱节点指向前一个结点，后驱节点指向后一个节点



## 思路：中序遍历+头尾结点



1. 排序链表： 节点应从小到大排序，因此应使用 中序遍历 “从小到大”访问树的节点。
2. 双向链表： 在构建相邻节点的引用关系时，设前驱节点 pre 和当前节点 cur ，不仅应构建 pre.right = cur ，也应构建 cur.left = pre 。
3. 循环链表： 设链表头节点 head 和尾节点 tail ，则应构建 head.left = tail 和 tail.right = head 。

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node() {}

    Node(int _val) {
        val = _val;
        left = NULL;
        right = NULL;
    }

    Node(int _val, Node* _left, Node* _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    /*
        dfs+原地进行修改，
    */
public:
    Node* pre, *head;
    void dfs(Node* cur) {
        if(cur == nullptr)
            return;
        // 中序遍历
        dfs(cur->left);
        if(pre != nullptr) {
            pre->right = cur;
        }else {
            // 如果没有前驱节点，则表示为第一个节点——头节点
            head = cur;
        }
        cur->left = pre;
        pre = cur;
        dfs(cur->right);

    }
    Node* treeToDoublyList(Node* root) {
        if(root == nullptr) return nullptr;
        dfs(root);
        // 最后特殊化处理，将头部的左指针指向尾节点，将尾部的右指针指向头节点
        head->left = pre;
        pre->right = head;
        return head;
    }
};
```

