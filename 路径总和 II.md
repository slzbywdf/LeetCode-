### 113. 路径总和 II
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
```
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
 ```
返回:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

**思路**: 自顶向下，在叶子节点判断sum
```
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
    vector<vector<int>> answer;
    void dfs(TreeNode* root, int sum, vector<int>& temp){
        if(root->left==NULL && root->right==NULL){ //叶子节点
            if(sum==0){
                answer.push_back(temp);
            }
            return;
        }
        if(root->left!=NULL){
            temp.push_back(root->left->val);
            dfs(root->left, sum-root->left->val, temp);
            temp.pop_back(); 
        }
        if(root->right!=NULL){
            temp.push_back(root->right->val);
            dfs(root->right, sum-root->right->val, temp);
            temp.pop_back(); 
        }
    }
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        if(root==NULL){
            return answer;
        }
        vector<int> temp;
        temp.push_back(root->val);
        dfs(root, sum-root->val, temp);
        return answer;
    }
};
```
