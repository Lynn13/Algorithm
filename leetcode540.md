```
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        while (low < high){
            //找到一个偶数的mid，使mid和mid左侧的元素个数加起来为奇数
            int mid = (low + high)/2;
            if (mid % 2 == 1)
                mid--;

            //左边如果都是一对一对的，那么nums[mid] == nums[mid + 1]
            if (nums[mid] != nums[mid + 1])
                high = mid;//一定要取mid，因为右侧都是一对一对的，而且个数为偶
            else
                low = mid+2;//取mid或者mid+2，因为左侧都是一对一对的，但是如果取mid会超时

        }
        return nums[low];
    }
}
```
