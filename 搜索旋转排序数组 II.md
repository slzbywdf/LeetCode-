## 81. 搜索旋转排序数组 II(Midium)
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 ```[0,0,1,2,2,5,6]``` 可能变为 ```[2,5,6,0,0,1,2]``` )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false。

示例 1:
```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true
```

**思路：** 同搜索旋转排序数组I, 对于middle==left 即无法区分中点在旋转点前后的情况，进行线性缩减

```
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size(); //取不到
        int middle;
        while(left < right){
            middle = left + ((right-left)>>1);
            cout<<nums[middle]<<endl;
            if(nums[middle] == target){
                return true;
            }
            if(target >= nums[left]){ //目标值在旋转点前
                if(nums[middle] > nums[left]){ //中点在旋转点前
                    if(target > nums[middle]){
                        left = middle + 1;
                    }else{
                        right = middle;
                    }
                }else if(nums[middle] == nums[left]){
                    left++;
                }else{ //中点在旋转点之后
                    right = middle;
                }
            }else{ //目标值在旋转点后
                if(nums[middle] > nums[right-1]){ //中点在旋转点前
                        left = middle+1;
                } else if(nums[middle] == nums[right-1]){
                    right--;
                }else{ //中点在旋转点后，正常二分
                    if(target > nums[middle]){
                        left = middle + 1;
                    }else{
                        right = middle;
                    }
                }
            }
        }
        return false;
    }
};
```
