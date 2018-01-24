# Find the Duplicate Number

给n+1个数，都在1-n范围内，仅有一个数会重复x次，x>=2,不能改变数组，找到这个数。

### 解法1

排序。时间nlgn，空间1，但是改变了数组。或者时间nlgn，空间n，没改变数组。

### 解法2

hashset。空间n，时间n。

### 解法3

我自创的。不改变数组的情况下空间n，时间n。下面的代码改变了数组。

```
class Solution {
    public int findDuplicate(int[] nums) {
        int res = -1;
        for (int i = 0; i < nums.length; i++){
            int index = Math.abs(nums[i]);
            if (nums[index - 1] > 0)
                nums[index - 1] *= -1;
            else
                return index;
        }

        return res;
    }
}
```

### 解法4

快慢指针的Floyd's 算法。时间n，空间1，无敌。

首先，想象一下，nums[4] = 8代表着4->8的有向图。也就是说num[i]和num[j]重复，一定存在环，并且环的入口就是num[i] or num[j]。



       // Find the intersection point of the two runners.
       int tortoise = nums[0];
        int hare = nums[0];
        do {
            tortoise = nums[tortoise];
            hare = nums[nums[hare]];
        } while (tortoise != hare);


        // Find the "entrance" to the cycle.
        int ptr1 = nums[0];
        int ptr2 = tortoise;
        while (ptr1 != ptr2) {
            ptr1 = nums[ptr1];
            ptr2 = nums[ptr2];
        }