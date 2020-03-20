## 题目 面试题40. 最小的k个数(Easy)
输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

示例 1：
```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```
示例 2：
```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

**思路**： 用大根堆，维护k个最小值即可
```
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        priority_queue<int> my_heap; //默认大根对
        for(int i=0; i<arr.size(); i++){
            my_heap.push(arr[i]);
            if(my_heap.size() > k){
                my_heap.pop();
            }
        }
        vector<int> answer;
        while(!my_heap.empty()){
            answer.push_back(my_heap.top());
            my_heap.pop();
        }
        return answer;
    }
};
```
