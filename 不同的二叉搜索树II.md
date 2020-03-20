## 95. 不同的二叉搜索树II
给定一个整数 n，生成所有由 1 ... n 为节点所组成的二叉搜索树。

示例:

```
输入: 3
输出:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释:
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

**思路**
直接暴力搜索, 以i为根节点，以[1,i-1]生成左子树,[i+1, n]生成右子树

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
    map<pair<int, int>, vector<TreeNode*>> memo;
    vector<TreeNode*> generateTree(int s, int e){
        vector<TreeNode*> answer;
        if(s>e){
            return answer;
        }
        if(memo.find(make_pair(s,e))!=memo.end()){
            cout<<s<<" "<<e<<endl;
            return memo[make_pair(s,e)];
        }

        for(int i=s; i<=e; i++){
            vector<TreeNode*> lefts = generateTree(s, i-1);
            vector<TreeNode*> rights = generateTree(i+1, e);
            if(lefts.size()==0 && rights.size()==0){
                TreeNode* root = new TreeNode(i);
                answer.push_back(root);
            }else if(lefts.size()==0){
                for(int k=0; k<rights.size(); k++){
                    TreeNode* root = new TreeNode(i);
                    root->right = rights[k];
                    answer.push_back(root);
                }
            }else if(rights.size()==0){
                for(int j=0; j<lefts.size(); j++){
                    TreeNode* root = new TreeNode(i);
                    root->left = lefts[j];
                    answer.push_back(root);
                }
            }else{
                for(int j=0; j<lefts.size(); j++){
                    for(int k=0; k<rights.size(); k++){
                        TreeNode* root = new TreeNode(i);
                        root->left = lefts[j];
                        root->right = rights[k];
                        answer.push_back(root);
                    }
                }
            }
        }
        memo[make_pair(s, e)] = answer;
        return answer;
    }
    vector<TreeNode*> generateTrees(int n) {
        return generateTree(1, n);
    }
};
```
