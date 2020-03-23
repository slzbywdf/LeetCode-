117. 填充每个节点的下一个右侧节点指针 II(Middle)
给定一个二叉树

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。

**思路**： 利用next指针，在下一层寻找prev 及后一个node，然后用next

```
class Solution {
public:
    
    Node* connect(Node* root) {
        if(root==NULL){
            return NULL;
        }
        Node* leftmost = root; //维护每一层首节点
        Node* point; Node* next_point;
        while(leftmost!=NULL){
            point = leftmost;
            while(point!=NULL){
                //连接同一父亲的节点
                if(point->left!=NULL)
                    point->left->next = point->right;
                
                next_point = point->next;
                if((point->left!=NULL || point->right!=NULL) && next_point!=NULL){ //存在子节点
                    while(next_point!=NULL && next_point->left==NULL && next_point->right==NULL){ 
                        //找到下一个节点
                        next_point = next_point->next;
                    }
                    if(next_point == NULL) //无跨父节点情况
                        break;

                    if(point->right!=NULL){
                        if(next_point->left!=NULL){
                            point->right->next = next_point->left; //跨父亲节点连接
                        }else{
                            point->right->next = next_point->right;
                        }
                    }else{
                        if(next_point->left!=NULL){
                            point->left->next = next_point->left; //跨父亲节点连接
                        }else{
                            point->left->next = next_point->right;
                        }
                    }
                }
                point = next_point;
            } //一层结束
            while(leftmost!=NULL && leftmost->left==NULL && leftmost->right==NULL){ //找到下一个节点
                    leftmost = leftmost->next;
            }
            if(leftmost == NULL)
                break;
            if(leftmost->left!=NULL)
                leftmost = leftmost->left;
            else
                leftmost = leftmost->right;
        }
        return root;
    }
};

```
