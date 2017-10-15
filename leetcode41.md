## First Missing Positive
- When we find 5, then swap it with A[4].
- 把当前位置的数换到他自己的位置上，直到换来本位置想要的数

```
import java.util.Arrays;

class Solution {
    public int firstMissingPositive(int[] nums) {
        if (nums.length == 0)
            return 1;
        for (int i = 0; i < nums.length; i++){
            while (nums[i] - 1 >= 0 && nums[i] - 1 < nums.length && nums[i] != nums[nums[i] - 1]){
                swap(nums, i, nums[i] - 1);
            }
        }

        
        for (int i = 0; i < nums.length; i++){
            if (nums[i] != i + 1)
                return i + 1;
        }

        return nums.length + 1;
    }

    private void swap(int[] nums, int a, int b){
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```
