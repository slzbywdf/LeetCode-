## 25. K 个一组翻转链表（Hard）
给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

 
```
示例：

给你这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5
```

```
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* first = head; //当前第一个节点
        ListNode* nextKfirst = head; //当前第k个节点
        ListNode* nextKfirst1;
        ListNode* pre = NULL;
        ListNode* next1;
        ListNode* root = NULL;
        while(first!=NULL){
            ListNode* temp = first;
            for(int i=0; i<k-1; i++){
                if(nextKfirst->next == NULL){
                    nextKfirst = NULL;
                    break;
                }
                nextKfirst = nextKfirst->next;
            }
            if(nextKfirst == NULL){
                break;
            }
            nextKfirst1 = nextKfirst->next;
            if(root==NULL){
                root = nextKfirst;
            }

            while(first != nextKfirst){
                next1 = first->next;
                first->next = nextKfirst->next;
                nextKfirst->next = first;
                first = next1;
            }
            if(pre!=NULL){
                pre->next = first;
            }
            pre = temp; //该轮第一个节点
            first = nextKfirst1; //下一轮要更换的k个数
            nextKfirst = first;
        }

        if(root==NULL){
            root = head;
        }
        return root;
    }
};
```
