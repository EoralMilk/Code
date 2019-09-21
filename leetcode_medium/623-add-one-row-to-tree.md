## 623 add-one-row-to-tree
##### 2019年9月20日
##### 二叉树基本操作
***

## 题目

给定一个二叉树，根节点为第1层，深度为 1。在其第 d 层追加一行值为 v 的节点。

添加规则：给定一个深度值 d （正整数），针对深度为 d-1 层的每一非空节点 N，为 N 创建两个值为 v 的左子树和右子树。

将 N 原先的左子树，连接为新节点 v 的左子树；将 N 原先的右子树，连接为新节点 v 的右子树。

如果 d 的值为 1，深度 d - 1 不存在，则创建一个新的根节点 v，原先的整棵树将作为 v 的左子树。

```
示例 1:

输入: 
二叉树如下所示:
       4
     /   \
    2     6
   / \   / 
  3   1 5   

v = 1

d = 2

输出: 
       4
      / \
     1   1
    /     \
   2       6
  / \     / 
 3   1   5   

示例 2:

输入: 
二叉树如下所示:
      4
     /   
    2    
   / \   
  3   1    

v = 1

d = 3

输出: 
      4
     /   
    2
   / \    
  1   1
 /     \  
3       1
```

注意:
输入的深度值 d 的范围是：[1，二叉树最大深度 + 1]。
输入的二叉树至少有一个节点。

>来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-one-row-to-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 分析

题目关于新一层的添加规则已经说得很清楚，了解如何添加之后便可按照指定规则进行插入。插入到第一层需要做特殊处理，其他层则需要注意要对上一层节点创建两个孩子。不能只创建一个孩子。即，除了插入到第一层的特殊情况外，其他层必是成对插入。

实现方式：对于d为1进行特殊处理，其他情况则从根节点向下遍历，记录当前的层数，层数需要从2开始，每遍历一层，层数加一。当层数和d相同时意味着需要在此处进行插入节点。新建两个节点，判断原有节点左右子树的情况，如果有左孩子，则将左孩子连接到新的左孩子的左边；若有右孩子，则将右孩子连接到新的右孩子的右边。完成这个操作之后再把新建立的左右孩子和根节点进行连接。👌

## 代码

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* addOneRow(TreeNode* root, int v, int d) {
        if(d == 1){
            TreeNode* tmp = new TreeNode(v);
            tmp->left = root;
            root = tmp;   
        }
        else{
            //从第二层开始判断
            helper(root, v, d, 2);
        }
        return root;
    }
    void helper(TreeNode* root, int v, int d, int l){
        //l表示层数
        if(l == d){
            TreeNode* tmp1 = new TreeNode(v);
            TreeNode* tmp2 = new TreeNode(v);
            if(root -> left){
                tmp1 -> left = root -> left;
            }
            if(root -> right){
                tmp2 -> right = root -> right;
            }
            root -> left = tmp1;
            root -> right = tmp2;
            //return  ;
        }
        else{
            if(root -> left)
                helper(root->left, v, d, l+1);
            if(root -> right)
                helper(root->right, v, d, l+1);
        }
        return ;
    }
};
```