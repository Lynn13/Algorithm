### Patching Array
- `reach` 表示 0 - i 的元素能够组合成的最大范围
- `reach + 1`就是现在队列中恰好缺少的数

```
class Solution {
    public int minPatches(int[] nums, int n) {
        int res = 0;
        long reach = 0;
        int i = 0;
        while(reach < n){
            // 下一个数比reach小，reach增加这个数
            // 下一个数恰好是缺少的数，reach更加美滋滋
            if(i < nums.length && (reach >= nums[i] || reach + 1 == nums[i])){
                reach += nums[i];
                i++;
            }
            else{
                reach += reach + 1;
                res++;
            }
        }
        return res;
    }
}
```
